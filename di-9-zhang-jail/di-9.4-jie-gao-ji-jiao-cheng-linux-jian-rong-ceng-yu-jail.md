# 9.4 Linux Jail

## 准备工作

本文会把所有 jail 绑定到虚拟接口 `lo1` 上，所有的 jail 等同于位于 FreeBSD 下的一个局域网中，FreeBSD 主机相当于该局域网的网关。

所有 jail 的网络活动须经过网络接口 `lo1`，所以要使用网络就须做网络转发，这里使用 pf 防火墙完成这个工作。

>**注意**
>
>这是获取网络访问的关键。

### 准备网络接口

```sh
# sysrc cloned_interfaces+="lo1" # 增加一个克隆的网络接口 lo1
# service netif cloneup          # 启用克隆的网络接口
```

### 准备 pf 防火墙

这里提供两种方式进行配置，请按需选用。

#### 方法一

编辑 `/etc/pf.conf`，加入：

```sh
table <jails> persist
nat pass on em0 inet from <jails> to any -> em0
```

在防火墙中建立名为 `jails` 的表，并指定 `persist` 标志使防火墙总是维持这个表（即使没有相关的规则引用它）。

“表”是 pf 防火墙的一种命名结构，可保存地址和网络的集合。`jails` 表中的地址可以通过 NAT 访问网络。

可以用 `pfctl` 对 `jails` 表进行增减以达到控制网络访问的目的。如：

- `pfctl -t jails -T add 192.168.5.1` 把 `192.168.5.1` 加入 jails 表使其可以访问网络
- `pfctl -t jails -T delete 192.168.5.1` 把 `192.168.5.1` 移出 jails 表使其无法访问网络。

特点是手动管理麻烦，但灵活。

#### 方法二

直接在 `/etc/pf.conf` 中写下规则：

```sh
nat pass on em0 inet from 192.168.5.1 to any -> em0
```

以允许 `192.168.5.1` 访问网络，特点是规则固化在配置中，没有特别的需求的话这个挺方便的。

### 启用 pf 防火墙

>**警告**
>
>无论你想不想使用防火墙，不这样设置你在 Jail 中都没有网络。

```sh
# service pf enable
# service pf start
```

### 加载必要的 Linux 兼容层内核模块

```sh
# service linux enable
# service linux start
```

这种方式可自动完成 linux 兼容层各个模块的加载

### 准备目录

```sh
# mkdir /usr/jails  # 用于保存建立 jail 的相关文件
```

## 创建 debian jail

### 下载基本系统

这里以 Debian 12(bookworm) 为例：

构建 Ubuntu/Debian

```sh
# pkg install debootstrap #安装 debootstrap
# chmod 0700 /usr/local/sbin/debootstrap # 赋予权限。
# mkdir -p /usr/jails/debian
# debootstrap bookworm /usr/jails/debian https://mirrors.ustc.edu.cn/debian/ #此处使用了 USTC 镜像站
```

示例输出，如下：

```sh
I: Retrieving InRelease
I: Retrieving Packages
I: Validating Packages
I: Resolving dependencies of required packages...
I: Resolving dependencies of base packages...
I: Checking component main on https://mirrors.ustc.edu.cn/debian...
I: Retrieving adduser 3.130
I: Validating adduser 3.130
...
I: Extracting usr-is-merged...
I: Extracting util-linux-extra...
I: Extracting zlib1g...
```

>**注意**
>
>末尾可能会提示有错误，无视即可。

### 创建 debian jail 实例

现在用 Debian 12 基本系统创建 jail 实例，命名为 debian。

#### 实例的基本配置

创建 `/etc/fstab.debian`，内容如下：

```sh
devfs      /usr/jails/debian/dev      devfs       rw                      0  0
tmpfs      /usr/jails/debian/dev/shm  tmpfs       rw,size=1g,mode=1777    0  0
fdescfs    /usr/jails/debian/dev/fd   fdescfs     rw,linrdlnk             0  0
linprocfs  /usr/jails/debian/proc     linprocfs   rw                      0  0
linsysfs   /usr/jails/debian/sys      linsysfs    rw                      0  0
/tmp       /usr/jails/debian/tmp      nullfs      rw                      0  0
```

在 `/etc/jail.conf` 中，加入以下内容（若无则新建）：

```sh
debian {                               # jail 名
  host.hostname = debian;              # jail 的主机名
  mount.fstab = /etc/fstab.debian;     # jail 使用的 fstab：启动/关闭 jail 时，挂载/卸载对应的文件系统
  path = /usr/jails/debian;            # jail 使用的根目录
  devfs_ruleset = 4;                   # jail 挂载 devfs 的规则集的值：0 表示无规则集，jail 会继承上级 jail 规则集，
                                       # 只在启用 allow.mount、allow.mount.devfs 且 enforce_statfs 小于 2 时可以挂载 devfs
  enforce_statfs = 1;                  # 设置为 0 时，所有挂载点都是可用的，无任何限制。
                                       # 设置为 1 时，只有 jail 根目录之下的挂载点是可见的。
                                       # 设置为 2(默认值) 时，只能在 jail 目录所在的挂载点上操作，不能挂载 devfs、tmpfs 等。
  allow.mount;                         # 允许挂载文件系统
  allow.mount.devfs;                   # 允许挂载 devfs
  exec.start = '/bin/true';            # 见下
  exec.stop = '/bin/true';             # 见下
  persist;                             # 允许 jail 在没有任何进程的情况下存活
  allow.raw_sockets;                   # 允许 ping 等使用 raw socket，看需要写入
  interface = lo1;                     # 使用 lo1 作为网络接口
  ip4.addr = 192.168.5.1;              # 使用的 ipv4 地址
  ip6 = disable;                       # 禁用 ipv6
}
```

- `exec.start` 指定启动 jail 时运行的命令。

如果是 freebsd 做 jail 一般是 `exec.start = 'sh /etc/rc'`，即使用 FreeBSD 的 rc 系统启动服务。

但是 debian 中使用的是 systemd 作为 init 系统。jail 并不能使用 systemd，所以不能使用相应的命令（service 命令可用），所以在这里用 `/bin/true` 不做任何事安全的返回 `true` 就可以。

问题就是（以 sshd 服务为例）在 debian jail 中启用 sshd 服务后（ `service ssh start` ）, 如果重启 debian jail，那么 sshd 服务不会再次随 jail 启动而启动。这时可以写成 `exec.start = 'service ssh start'`。这样启动 debian jail 时可以启动 sshd 服务。

如果要启用更多的服务，则可以编写如下：

```sh
exec.start += 'service ssh start'
exec.start += 'service dbus start'
```

- `exec.stop` 停止 jail 时运行的命令。

如果是 freebsd 做 jail 一般是 `sh /etc/rc.shutdown jail`。

这里同样因为 systemd 的原因用 `/bin/true` 安全的返回 `true` 就可以。

### 启用实例，允许网络访问

- 启动 jail

```sh
# jail -c debian
```

- 停止 jail

```sh
# jail -r debian
```

- 在 pf 防火墙中的 `jails` 表中加入 jail 的地址，以允许 jail 访问网络：

```sh
# pfctl -t jails -T add 192.168.5.1
```

### 更新系统

执行：

```sh
# jexec debian /bin/bash # 此时位于 FreeBSD！
Debian # apt remove rsyslog  # 此时位于 Debian Jail!
Debian # apt update # 此时位于 Debian Jail!
```

或者使用

```sh
# jexec -l debian /bin/bash -c 'apt remove rsyslog'
# jexec -l debian /bin/bash -c 'apt update'
```

至此，一个基于 Debian 12 的 linux jail 已经成功建立，同样的方法可以建立基于 debian 和 ubuntu 各版本的多个 jail。

## jail 开机自启

开机时启动 jail

```sh
# service jail enable
```

默认启动所有 jail。

另外可以在 `/etc/rc.conf` 中用 `jail_list` 变量指定在开机时启动的 jail 的名字，编辑 `/etc/rc.conf` 写入：

```sh
jail_list = "debian"
```

或执行

```sh
# sysrc jail_list+=debian
```

如果 `jail_list` 变量为空，则会启动所有在 `/etc/jail.conf` 中配置的 jail。

## 创建 Ubuntu jail

ubuntu jail 建立方法同上，以 Ubuntu 22.04(jammy) 为例，

### 构建基本系统并配置

```sh
# mkdir -p /usr/jails/ubuntu
# debootstrap jammy /usr/jails/ubuntu https://mirrors.ustc.edu.cn/ubuntu/
```

创建 `/etc/fstab.ubuntu`，内容如下：

```sh
devfs      /usr/jails/ubuntu/dev      devfs       rw                      0  0
tmpfs      /usr/jails/ubuntu/dev/shm  tmpfs       rw,size=1g,mode=1777    0  0
fdescfs    /usr/jails/ubuntu/dev/fd   fdescfs     rw,linrdlnk             0  0
linprocfs  /usr/jails/ubuntu/proc     linprocfs   rw                      0  0
linsysfs   /usr/jails/ubuntu/sys      linsysfs    rw                      0  0
/tmp       /usr/jails/ubuntu/tmp      nullfs      rw                      0  0
```

在 `/etc/jail.conf` 中写入 ubuntu 的配置，如下：

```sh
ubuntu {
  host.hostname = ubuntu;
  mount.fstab = /etc/fstab.ubuntu;
  path = /usr/jails/ubuntu;
  devfs_ruleset = 4;
  enforce_statfs = 1;
  allow.mount;
  allow.mount.devfs;
  exec.start = '/bin/true';
  exec.stop = '/bin/true';
  persist;
  allow.raw_sockets;
  interface = lo1;
  ip4.addr = 192.168.5.2;
  ip6 = disable;
}
```

### 启用实例并允许网络访问

```sh
# jail -c ubuntu # 启用实例
```

如果已经在 `/etc/rc.conf` 中设置过 `jail_enable=YES`，也可以用

```sh
# service jail start ubuntu
```

开机启动可以参考 debian jail，执行

```sh
# sysrc jail_list+=ubuntu
```

在 pf 防火墙中的 `jails` 表中加入 jail 的地址，以允许 jail 访问网络：

```sh
# pfctl -t jails -T add 192.168.5.2 # 允许网络访问
```

### 更新系统

```sh
# jexec ubuntu /bin/bash # 此时位于 FreeBSD！
Ubuntu # apt remove rsyslog  # 此时位于 Ubuntu Jail!
Ubuntu # apt update # 此时位于 Ubuntu Jail!
```

或者使用

```sh
# jexec -l debian /bin/bash -c 'apt remove rsyslog'
# jexec -l debian /bin/bash -c 'apt update'
```

过程和同 debian jail。

## 创建 AntiX linux jail

AntiX 基于 debian，且不使用 systemd。

### 下载镜像文件并解压

先安装 `squashfs-tools` 以解压 linux 文件系统镜像。

```sh
# pkg install squashfs-tools
```

AntiX linux 提供四个镜像版本，full、base、core、net，这里下载 core 版本：

```sh
# fetch https://mirrors.tuna.tsinghua.edu.cn/mxlinux-isos/ANTIX/Final/antiX-23.2/antiX-23.2_x64-core.iso
# mdconfig antiX-23.2_x64-core.iso
# mount -t cd9660 /dev/md0 /mnt
# mkdir -p /usr/jails/antix
# unsquashfs -d /usr/jails/antix /mnt/antiX/linuxfs
# touch /usr/jails/antix/dev/fd
# touch /usr/jails/antix/dev/shm
```

### 配置 Antix jail

创建 `/etc/fstab.antix`，内容如下：

```sh
devfs      /usr/jails/antix/dev      devfs       rw                      0  0
tmpfs      /usr/jails/antix/dev/shm  tmpfs       rw,size=1g,mode=1777    0  0
fdescfs    /usr/jails/antix/dev/fd   fdescfs     rw,linrdlnk             0  0
linprocfs  /usr/jails/antix/proc     linprocfs   rw                      0  0
linsysfs   /usr/jails/antix/sys      linsysfs    rw                      0  0
/tmp       /usr/jails/antix/tmp      nullfs      rw                      0  0
```

在 `/etc/jail.conf` 中写入 (这里只展示 antix 相关部分)

```sh
antix {
  host.hostname = antix;
  mount.fstab = /etc/fstab.antix;
  path = /usr/jails/antix;
  devfs_ruleset = 4;
  enforce_statfs = 1;
  allow.mount;
  allow.mount.devfs;
  exec.start = '/etc/init.d/rc 3';
  exec.stop = '/etc/init.d/rc 0';
  persist;
  allow.raw_sockets;
  interface = lo1;
  ip4.addr = 192.168.5.3;
  ip6 = disable;
}
```

这里 `exec.start` 设为 `/etc/init.d/rc 3`。

在 debian jail 部分已经提到，debian 使用 systemd 做初始化系统。这在 jail 中不能使用，所以用 `/bin/true` 启动，以保证什么都不做，只是安全返回 true 值。

antiX 不使用 systemd 做初始化系统，可以用 rc 进行初始化：在这里 `/etc/init.d/rc 3` 指定 antix jail 在启动时使用 rc 以第 3 运行级别初始化 jail。即在 debian jail 中提到的服务运行问题在这里并不存在（即可以直接在 jail 启动时运行服务，比如 sshd）。

### 更新系统

- 设置开机自启，然后启动

```sh
# sysrc jail_list+=antix
# jail -c antix   # 或者使用 service jail start antix 前面已经提到
```

- 在 pf 中允许网络访问，方法同上。

```sh
# pfctl -t jails -T add 192.168.5.3
```

- 现在进入 jail：

```sh
# jexec antix /bin/bash     # 物理机（FreeBSD）中
root@antix:/# echo "nameserver 223.5.5.5" > /etc/resolv.conf    # jail 中，注意提示符变化，先设置地址解析，这里使用阿里 DNS
root@antix:/# echo "APT::Cache-Start 90000000;" >> /etc/apt/apt.conf   # `APT::Cache-Start` 是 apt 使用缓存的大小，默认 20m 太小，按提示增大
root@antix:/# apt update         # 可以先修改 `/etc/apt/sources.list.d/` 中的文件以使用镜像站，请参考各镜像站中 debian 的镜像站设置
root@antix:/# apt upgrade
root@antix:/# mandb       # apt upgrade 的时候显示 mandb 有几个权限错误，多执行几遍  `mandb` 命令就是。
```

## 创建 Alpine jail

- 构建基本系统

```sh
# fetch http://mirrors.ustc.edu.cn/alpine/v3.17/releases/x86_64/alpine-minirootfs-3.17.1-x86_64.tar.gz
# mkdir -p /usr/jails/alpine
# tar zxf alpine-minirootfs-3.17.1-x86_64.tar.gz -C /usr/jails/alpine/
# touch /usr/jails/alpine/dev/shm
# touch /usr/jails/alpine/dev/fd
```

- 创建 `/etc/fstab.alpine`，内容如下：

```sh
devfs      /usr/jails/alpine/dev      devfs       rw                      0  0
tmpfs      /usr/jails/alpine/dev/shm  tmpfs       rw,size=1g,mode=1777    0  0
fdescfs    /usr/jails/alpine/dev/fd   fdescfs     rw,linrdlnk             0  0
linprocfs  /usr/jails/alpine/proc     linprocfs   rw                      0  0
linsysfs   /usr/jails/alpine/sys      linsysfs    rw                      0  0
#/tmp       /usr/jails/alpine/tmp      nullfs      rw                      0  0
```

- 在 `/etc/jail.conf` 中写入，

```sh
alpine {
  host.hostname = alpine;
  mount.fstab = /etc/fstab.alpine;
  path = /usr/jails/alpine;
  devfs_ruleset = 4;
  enforce_statfs = 1;
  allow.mount;
  allow.mount.devfs;
  exec.start = '/bin/true';  # minirootfs 里还没有初始化系统，所以还是用 '/bin/true'，下面会设置 openrc
  exec.stop = '/bin/true';
  persist;
  allow.raw_sockets;
  interface = lo1;
  ip4.addr = 192.168.5.4;
  ip6 = disable;
}
```

- 设置开机启动，然后启动

```sh
# sysrc jail_list+=alpine
# jail -c alpine
```

- 在 pf 中允许网络访问，方法同上。

```sh
# pfctl -t jails -T add 192.168.5.4
```

- 现在进入 jail：

```sh
freebsd # jexec alpine /bin/sh        # 初始只有 sh，注意 shell 提示符的变化
alpine # sed  -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/' /etc/apk/repositories    # 修改镜像地址
alpine # echo 'nameserver 223.5.5.5' >> /etc/resolv.conf      #  初始没有这个文件，自建一个
alpine # apk update             # alpine 可以不使用 openrc 而使用程序，但是不能启动各种服务，只有在安装 openrc 后才能启动各项服务，所以最好安装 openrc 以获得更好的体验
alpine # apk add openrc         # 安装 openrc 作为初始化系统
alpine # mkdir /run/openrc
alpine # touch /run/openrc/softlevel      # openrc 提示在 docker/chroot/jail 环境中应该建立这个文件
alpine # exit    # 注意 shell 提示符的变化
freebsd # jail -r alpine    # 先关闭 alpine，以使在 freebsd 宿主机中进行 openrc 配置
```

- 修改 `/etc/jail.conf` 中 alpine 的配置：

```sh
alpine {
  host.hostname = alpine;
  mount.fstab = /etc/fstab.alpine;
  path = /usr/jails/alpine;
  devfs_ruleset = 4;
  enforce_statfs = 1;
  allow.mount;
  allow.mount.devfs;
  exec.start = '/sbin/openrc default';  # 此处修改，使用 openrc 作初始化系统，以 default 运行级初始化系统
  exec.stop = '/sbin/openrc shutdown';  # 此处修改，使用 openrc 作初始化系统，以 shutdown 运行级运行关闭任务
  persist;
  allow.raw_sockets;
  interface = lo1;
  ip4.addr = 192.168.5.4;
  ip6 = disable;
}
```

- 重启 alpine

```sh
# jail -c alpine
```

## jail 中的 GUI

本文环境：Windows 10 物理机，在 virtualbox 安装了 FreeBSD 13.1 虚拟机。

在 FreeBSD 虚拟机中已部署了 4 个 jail，如下。这里有一个 freebsd jail，为和 virtualbox 中的 FreeBSD 虚拟机作区分，我们称其为 `freebsd-jail`：

Windows 10 物理机 ⇨ FreeBSD 13.1 虚拟机 ⇨ FreeBSD Jail（`freebsd-jail`） + Debian Jail + Ubuntu Jail + Alpine Jail。

```sh
# jls
   JID  IP Address      Hostname                      Path
     1  192.168.5.3     debian                      /usr/jails/debian
     2  192.168.5.4     ubuntu                    /usr/jails/ubuntu
     3  192.168.5.2     alpine                        /usr/jails/alpine
     4  192.168.5.1     freebsd-jail                  /usr/jails/freebsd-jail
```

在这 4 个 jail 中分别安装 xclock、firefox、chrome、jwm 这几款软件。

在 freebsd-jail、debian、ubuntu、alpine( alpine 使用 vnc 方法不成功，其它方法 xclock、xterm 可运行，firefox 和 chrome 未成功) 都成功了，jwm 用于美化。

>**技巧**
>
>不用安装 xorg。

其中，在 ubuntu 22.04，firefox、chrome 要求用 snap 安装，snap 需要 systemd，不能使用，所以使用 deb 包安装。方法如下：

```sh
# wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
# dpkg -i google-chrome-stable_current_amd64.deb
# apt install ./google-chrome-stable_current_amd64.deb
```

### 带 X Server 的终端

这里使用 MobaXterm。MobaXterm 默认配置，无多余配置。

![](../.gitbook/assets/jailx11mobaxstart.png)

确保 X server 已经启用，记下 `DISPLAY` 值，格式是 `hostname:displaynumber.screennumber` 这里是 `192.168.56.1:0.0`

登录 jail（不限方式，可以是 ssh，可以是 jexec；不限用户，可以是普通用户，不一定是 root、wheel 组成员）

```sh
$ export DISPLAY=192.168.56.1:0.0  # jail 中，这里是 sh/zsh/bash。csh/tcsh 是 setenv DISPLAY 192.168.56.1:0.0，下同
$ xclock&
```

![](../.gitbook/assets/jailx11mobaxclock.png)

4 个 xclock 可独立显示在 Windows 10 桌面上，效果比较理想。

### 内嵌 X Server

X Server 里的 X Server，这里使用 Xnest/Xephyr、Xnest/Xephyr 对 X11 应用来说是 X Server，对宿主 X Server 来说是 X Client。

- FreeBSD 虚拟机里安装 Xnest 或 Xephyr。两者择其一即可：

```sh
# pkg install Xnest
```

或者

```sh
# pkg install Xephyr
```

- 在 FreeBSD 中启用

```sh
$ Xephyr :1 -listen tcp  # 不需要 root 权限
```

- `:1` 即上面提到了 `DISPLAY` 值中的 `displaynumber`。FreeBSD 系统 IP 为 `10.0.2.15`，所以完整的 `DISPLAY` 值为 `10.0.2.15:1.0`。因为 FreeBSD 系统 X Server 的 `displaynumber` 值为 `0`，所以从 `1` 开始
- `-listen tcp` 侦听 TCP 端口

- 在 4 个 jail 中，采取上面相同的方法

```sh
$ export DISPLAY=10.0.2.15:1.0
$ xclock&
```

四个 jail 可以同时在 FreeBSD 开启的一个 Xnest/Xephyr 窗口中打开 xclock。但是此时的 xclock 因为没有窗口管理器，界面丑，且连最基本的拖动都做不到。可以在执行 xclock 前先执行 jwm，如下。

```sh
$ export DISPLAY=10.0.2.15:1.0
$ jwm &
$ xclock&
```

这里注意 `jwm &` 执行一次够了，不需要每个 jail 都去执行。这里用 jwm 只是看中其轻量级，xfce 等也是可以的。可以自行尝试。

### 共享主机 socket 方式

- 先在 FreeBSD 系统上执行

```sh
$ xhost +
```

- 关闭访问控制：

然后在 jail 的 `fstab` 中加入下面内容，这里以 ubuntu jail 的 `fstab` 为例，其它 jail 参照修改即可。

```sh
/tmp/.X11-unix   /usr/jails/ubuntu/tmp/.X11-unix    nullfs   ro   0  0
```

必要时先 `mkdir -p /usr/jails/ubuntu/tmp/.X11-unix`，确保有挂载点。

重启 jail 后，在 jail 中执行：

```sh
$ export DISPLAY=:0.0
$ xclock &
```

上文提到 `fstab` 文件中有下面这样一行

```sh
#/tmp   /usr/jails/ubuntu/tmp   nullfs  rw    0  0
```

虽然很多教程中有这样写，但我认为是不安全的，所以注释掉不用。如果这么写，那么 FreeBSD 的 `/tmp` 目录都将暴露在 jail 中，且因为是可读写的：在 jail 中就可以对 FreeBSD 的 `/tmp` 目录进行写入。这样就破坏了 jail 与 FreeBSD 的隔离性，是不安全的。而仅读挂载 `/tmp/.X11-unix`，则大大提高了安全性。

### X Server tcp 侦听加 xhost 连接管理

这里我使用的是 sddm 桌面管理器，使用其它桌面管理器的，请参考相应桌面管理器的文档进行，原理一样。

在 FreeBSD 内新建 `/usr/local/etc/sddm.conf`（如果没有的话），修改 `ServerArguments` 内容如下：

```sh
[X11]
ServerArguments=-listen tcp
```

重启后，FreeBSD 上用下面方式加入 jail IP 以允许访问 (无需 root 权限）：

```sh
$ xhost + 192.168.5.1  # 这里不建议用上面的提到 `xhost +` 方式关闭访问控制，以避免意料外的连接
```

然后在 jail 中，执行：

```sh
$ export DISPLAY=:0.0
$ xclock &
```

- 这里把 `DISPLAY` 设为 `:0.0`,`127.0.0.1:0.0`,`10.0.2.15:0.0` 都成功了，上面几种方法也可以一一尝试。

### VNC

在 jail 中安装 vnc server，可以用 tightvnc-server，也可以用 tigervnc-server，这里以 debian jail 为例，在 jail 中执行

```sh
# apt install tightvncserver
$ vncpasswd           # 这里不要求 root 用户
Password:
Verify:
Would you like to enter a view-only password (y/n)? n
A view-only password is not used
$ vncserver :0        # 同样不要求 root 用户，vncserver 的端口号为 5900 加上冒号后的数字，现在为 5900，`:1` 端口号 5901，以此类推。
```

使用 vnc 客户端登录

![](../.gitbook/assets/jailx11vnc1.png)

![](../.gitbook/assets/jailx11vnc2.png)

![](../.gitbook/assets/jailx11vnc3.png)

### 备注

宿主机 X Server tcp 侦听加 xhost 连接管理的方式是安全性最差的一种，是 tcp 侦听默认关闭原因之一。

共享宿主机 socket 的方式注意上面提到的两点安全性还是有保障的。

前 4 种方法算是“回字的 4 种写法”，都算是 X Server 连接的变体。带 X Server 的终端和共享 socket 的方式之外，其它三种方式最好在 jail 内再搭配个桌面。

带 X Server 的终端、共享主机 socket、vnc 这三种方式比较推荐。无论哪个方式，linux jail 中不要要求每个 X 应用都能运行，那真的很难做到，毕竟兼容层不是百分百兼容，freebsd jail 的话就好很多。

除去共享宿主机 socket 的方法，其它方法都是可以应用的非 jail 环境的。


## 参考资料

> 其他更多可以运行的软件及方法见 [https://wiki.freebsd.org/LinuxApps](https://wiki.freebsd.org/LinuxApps)。

网站：

- [12.2.配置 Linux 二进制兼容层](https://handbook.bsdcn.org/di-12-zhang-linux-er-jin-zhi-jian-rong-ceng/12.2.-pei-zhi-linux-er-jin-zhi-jian-rong-ceng.html)
- [linux --	Linux ABI support](https://www.freebsd.org/cgi/man.cgi?linux)
- [wiki/Linuxulator](https://wiki.freebsd.org/Linuxulator)
- [wiki/LinuxJails](https://wiki.freebsd.org/LinuxJails)
- [12.3.Linux 用户空间](https://handbook.bsdcn.org/di-12-zhang-linux-er-jin-zhi-jian-rong-ceng/12.3.-linux-yong-hu-kong-jian.html)

