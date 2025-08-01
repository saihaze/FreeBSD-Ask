# 编辑日志存档

## 2025 年第二季度

- 2025.6.24
  -  freebsd 14.3 的 wifi county select 有问题。选哪个都是这个报错：`Error while applying chosen settings  (unknown regdomain Expected  eval: Use: not found)` 参见 <https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=287538>。替代方法是手动写，参照无线网络章节。
- 2025.6.23
  - 3.6 文本编辑器新增：microsoft-edit
- 2025.6.21
  - 格式化：第 21.5 节 ArchLinux 兼容层（基于 archlinux-pacman）
  - 为镜像站 <https://docs.bsdcn.org/> 添加了自动序号
  - 重写：22.7 Python 和 VS Code：Python
  - 本书更名为《FreeBSD 操作系统研究导论》
- 2025.6.20
  - 第 1.2 节 欢迎来到 FreeBSD：完全重写“为什么选择 FreeBSD”，去除有关 Linux 的描述
- 2025.6.19
  - 调整目录结构
  - 第 19.1 节 PostgreSQL：将 PostgreSQL 更新到 17
  - 第 19.2 节 pgAdmin4 更新到 pgadmin4-9.0
  - 第 23.7 节 ZFS 磁盘加解密合并入 FreeBSD 安装章节
- 2025.6.17
  - 增加一个术语表放在附录
  - 调整目录结构
  - 新增：在 FreeBSD 上安装 VirtualBox
- 2025.6.16
  - 将第 1.2 节 FreeBSD 简史合并入：第 1.2 节 关于 FreeBSD 项目
  - 第 8.2 节 用户和基本账户管理新增：账户类型
  - 将参考书目独立出来放在附录
- 2025.6.15
  - 计划全面重写 FreeBSD 手册
- 2025.6.14
  - 重新引入：[贡献指南与开放任务](CONTRIBUTING.md)
- 2025.6.13
  - 第 1.1 节 操作系统的历程：UNIX、Unix-like、Linux & FreeBSD 重写：什么是 Linux？
  - 第 1.1 节 操作系统的历程：UNIX、Unix-like、Linux & FreeBSD 新增：GNU 与自由软件运动
  - 第 6.6 节 视频播放器新增：附录：直接在 TTY 播放视频（mpv）
- 2025.6.12
  - 第 4.3 节 GNOME：欢迎来到 Gnome 47
- 2025.6.10
  - 第 26.3 节 配置 OpenBSD 重写：doas
  - 第 26.1 节 OpenBSD 概述新增：其他专注于安全的 BSD 系统
  - 第 26.1 节 OpenBSD 概述新增：OpenBSD IPSEC 协议栈 FBI 后门事件
- 2025.6.9
  - 第 26.1 节 OpenBSD 概述新增：机遇与挑战、语录摘选
- 2025.6.8
  - 第 1.1 节 操作系统的历程：UNIX、Unix-like、Linux & FreeBSD 新增：草稿：二十一世纪的 Unix 哲学观
  - 第 1.1 节 操作系统的历程：UNIX、Unix-like、Linux & FreeBSD 增补：UNIX 之船：FreeBSD 是不是 UNIX？
  - 第 4.1 节 显卡驱动（英特尔、AMD）新增：AMD 视频硬解
- 2025.6.7
  - 根据调查问卷恢复一部分文学故事
- 2025.6.6
  - 第 2.3 节 UNIX 基础（新手入门版本）新增：Windows 与 Unix 字符编码的差异
  - 第 2.3 节 UNIX 基础（新手入门版本）新增：Windows 与 Unix 时间设置的差异
  - 第 2.4 节 命令行基础（新手入门版本）：新增“你并不孤单”
- 2025.6.4
  - 第 2.3 节 UNIX 基础（新手入门版本）新增：Windows 与 Unix 换行符/回车之差异，还需要补充编码差异、时区差异等
- 2025.5.30
  - 新增：第 1.7 节 BSD 许可证概览
- 2025.5.23
  - 新增：第 10.3 节 Podman
- 2025.5.17
  - 删除“第 21.2 节 Linux 兼容层——基于 CentOS（FreeBSD Port）”，过时
- 2025.5.16
  - 录制视频 [FreeBSD 14.2 基础安装配置教程](https://www.bilibili.com/video/BV1STExzEEhh)
- 2025.5.12
  - 移除“第 4.18 节 KDE6”中的“基于 Wayland”，可能存在错误
- 2025.5.9
  - 重写：第 22.8 节 Rust/Go 环境的配置
  - 此分支转为社区版本，去除 ykla 个人观点，保留中立内容。该分支转为社区维护，欢迎 PR。
- 2025.5.8
  - 第 2.4 节 命令行基础（新手入门版本）：新增“`vi` 编辑器基本用法”
- 2025.5.6
  - 从“第 2.2 节 FreeBSD 安装图解”拆分出“第 2.1 节 安装前准备（新手入门版本）”
- 2025.5.5
  - 测试“第 22.4 节 C/C++ 环境的配置”
  - 重写“第 4.5 节 Xfce”
  - UNIX 基础（新手入门版本）：新增“大小写敏感”
- 2025.5.2
  - 新增“第 2.3 节 UNIX 基础”
- 2025.4.29
  - 引入 GitHub Action“🔗 检查 Markdown 图片引用”。用以核查图片使用情况
  - 重写“第 5.4 节 五笔输入法”
- 2025.4.28
  - 第 26 章 OpenBSD：更新至 OpenBSD 7.7
  - 将“第 8.2 节 添加用户”合并入“第 8.2 节 用户与组”
  - 重写“第 8.2 节 用户与组”
  - 移除部分来自网络且未经验证的可能不可靠的内容
  - 重写“第 5.4 节 五笔输入法”，注意最后一部分未测试。
  - 重新排版：第 5.1 节 本地化环境变量
  - “第 13.4 节 SSH 配置与相关工具”：删除思考题，删除关于 OpenSSH 版本的描述，因为已经过时。
  - 今天总计清理出了 5 页 A4 纸的篇幅
  - “第 14.1 节 TCP 堆栈”新增“使用 RACK 栈”
- 2025.4.25
  - 重新更名为《FreeBSD 从入门到追忆》
  - 重写“第 6.3 节 打印机”
- 2025.4.24
  - 第 4.2 节 显卡驱动（NVIDIA）：完全重写
- 2025.4.22
  - 《FreeBSD 从入门到跑路》恢复旧名《FreeBSD 艺术科学哲学导论》
- 2025.4.22
  - 第 5.2 节 Fcitx 输入法框架：重新排版
  - 从“第 4.1 节 显卡驱动”拆分出“第 4.1 节 显卡驱动（英特尔、AMD）”、“第 4.2 节 显卡驱动（NVIDIA）”
  - 第 9.3 节 使用 Qjail 管理 Jail：重新排版
  - 由于电子邮件长期被忽视，今日分别致国际信函给“FreeBSD 基金会”（RD664821800CN）和“OpenBSD 基金会”（RD664821795CN），反馈目前的捐款渠道不畅之问题，以及呼吁关注中国大陆地区等
- 2025.4.21
  - “第 5.6 节 QQ（Linux 版）”新增：解决 fcitx 中文输入法在 QQ 中不能使用的问题
  
---

- 2024.8.1-2025.4.20：《FreeBSD 从入门到跑路》第二版完成（TAG 2025.4.20）

---

- 2025.4.20
  - 格式化全书
  - 对全书初版重写达 100%
- 2025.4.19
  - 第 4 章 桌面环境：新增软件解释
  - 对全书删除冗余，重新排版
- 2025.4.18
  - “第 2.2 节 命令行基础（新手入门版本）”新增：关机、重启、`&&`、`||`
- 2025.4.17
  - 重写：第 16.7 节 Samba 服务器中的安装 Samba 部分，其余部分无条件测试
  - 重写：第 16.6 节 rsync 同步服务
- 2025.4.16
  - 格式化：第 14.2 节 WiFi
  - “第 27.4 节 桌面与中文环境常用软件”：重写引入：KDE 4。因为物理机测试成功。
  - 从“第 1.1 节 操作系统的历程：UNIX、Unix-like、Linux & FreeBSD”拆分出“第 1.2 节 FreeBSD 简史”
  - 重写：第 2.6 节 云服务器安装 FreeBSD（基于腾讯云轻量云）
  - 拆分序言
  - 引入 GitHub Action：🔗 从 SUMMARY.md 更新一级标题。用于检查 SUMMARY 标题和对应文件的一级标题的符合情况
- 2025.4.15
  - 格式化：第 5.6 节 QQ（Linux 版）
  - 第 4.20 节 远程桌面：删除剩余的“VNC 与 RPD（XRDP）对比”部分
- 2025.4.14
  - 目前对全书初版已重写 96.57%（按 Commit 数）
  - 格式化“第 11.5 章 MySQL 数据库”
  - 删减占用篇幅较大的无用图片
- 2025.4.13
  - “第 16.5 节 WildFly”测试基本成功，但是注意补丁仍未合并到主线，详见 [Bug 285956 - java/wildfly: service start fail, illegal group name](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=285956)。
  - 新增“第 24.3 节 配置 DragonFly BSD”
  - 重写“第 24.2 节 安装 DragonFly BSD”
- 2025.4.11
  - 通过段落间距调整，PDF 页数从 1209 到 1084，减少了 10.34% 的页面占用。
- 2025.4.10
  - 测试、改写“第 2.8 节 手动安装双系统（后安装 FreeBSD）”
  - NetBSD 10.1 在 VMware 虚拟机中无论 UEFI 与否，进入 kde 4  都会黑屏。
- 2025.4.9
  - 使用 <https://gist.github.com/ykla/adf011fea43f5f4b91aa6f065ac09da2> 对全书过长（> 30 行）的代码块进行整理。
  - 孤行控制，删除冗余。
  - 从 1238 页到 1209 页，减少了 2.34% 的无效页面。
- 2025.4.8
  - “第 27.2 节 NetBSD 安装图解”更新至 NetBSD 10.1
  - “桌面与中文环境常用软件”更新至 NetBSD 10.1
  - “桌面与中文环境常用软件”新增输入法
  - “桌面与中文环境常用软件”新增中文环境
  - NetBSD KDE 4 UEFI 下测试失败，还是黑屏，报错见 <https://gnats.netbsd.org/57554>
  - “第 16.5 节 Wildfly”测试失败，见 [Bug 285956 - java/wildfly: service start fail, illegal group name](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=285956)
- 2025.4.7
  - 全译现有所有安装后说明
  - 从 [2024.8-3533 次](https://github.com/FreeBSD-Ask/FreeBSD-Ask/commit/c4d657fb586f91e9f8664ee1181a2711f7350d17) 开始，目前对全书初版已重写 94%（按 Commit 数），下同
  - 删除“第 11.3 节 散热器、风扇、鼓风机”，可能包含错误内容
- 2025.4.6
  - “第 17.8 节 PostgreSQL 与 pgAdmin4”新增“深入 PostgreSQL 服务管理”
  - “第 4.21 节 FreeBSD 桌面发行版”补图
- 2025.4.5
  - 初步重写第 15.4 节 ipfirewall（IPFW）
  - 格式化第 15.2 节 PF
  - 格式化第 15.3 节 IPFilter（IPF）
  - 新增“第 4.21 节 FreeBSD 桌面发行版”
- 2025.4.4
  - 从各个章节拆分出“第 6 章 多媒体与外设”
  - 格式化“第 5.1 节 输入法与环境变量”
  - 格式化“第 21.12 节 Linux 兼容层与 Jail”
  - mihomo（原 Clash），需要重写相关章节，我们需要一个 GUI 界面！
- 2025.4.3
  - 从“第 20.1 节 游戏”拆分出“第 20.6 节 我的世界（Minecraft）”
  - 将“第 20.2 节 音视频播放器与剪辑”拆分为“第 20.2 节 音频播放器”、“第 20.3 节 视频播放器”、“第 20.4 节 音视频剪辑与图像处理”、
  - 测试“第 20.5 节 科研与专业工具”，并新增“Calibre 文档管理（epub、mobi、azw3 等格式）”
  - “第 20.5 节 科研与专业工具”补图
  - “第 20.1 节 游戏”：重写“Renpy 游戏”
- 2025.4.2
  - 测试“第 20.2 节 音视频播放器”：尝试播放电视剧《人民公仆》、尝试播放动漫《败犬女主太多了！》，测试通过
- 2025.4.1
  - <https://mirrors.aliyun.com/freebsd-pkg/> 看起来早就失去同步。还是 2 月我提交 kmod 源以前的内容，故不写入


## 2025 年第一季度

- 2025.3.31
  - 将镜像站点迁移至 <https://docs.bsdcn.org/>
- 2025.3.30
  - 部署了镜像站点，临时位于 <https://freebsd-ask.github.io>，使用 VitePress
- 2025.3.29
  - 从现在起每天在 Github release 生成一个 PDF 文档
  - 生成新的 Windows 24H2 字体包用于 Github Action
  - 重写 PDF 导出工具
- 2025.3.27
  - “第 16.1 节 FTP 服务器”新增“vsftpd”
  - 引入 Github Action：🔗 从 SUMMARY.md 更新目录
  - 引入 Github Action：🔗 检查 SUMMARY.md 目录
  - 引入 Github Action：🔗 创建并发布 PDF 文档，从现在起每 5 天在 Github release 生成一个 PDF 文档
- 2025.3.26
  - 重写“Pure-FTPd（基于 MySQL）”
  - 重写“ProFTPD（基于 MySQL）”
  - “第 2.2 节 命令行基础（新手入门版本）”新增“UNIX 与 Windows 文件名规范之差异”
- 2025.3.25
  - 新增“第 15.5 节 Fail2Ban（基于 IPFW、PF、IPF）”
  - “第 12.2 节 FreeBSD EFI 引导管理”合并入“第 12.5 节 Grub & UEFI 与 efibootmgr”
- 2025.3.24
  - 测试“第 4.2 节 安装 KDE6”，同 VMware 的虚拟显卡无兼容性问题。缩放、鼠标无缝切换均正常。注：USTC 的源可能有问题。
  - 重写“致谢”
  - 根据 [clean-master/freebsdcn](https://github.com/clean-master/freebsdcn/graphs/contributors)，将本项目的开始时间改正至 2021 年 3 月 14 日。同时明确 clean-master 清理大师的历史贡献。
  - 重写“第 4.23 节 远程桌面管理”中的“使用 FreeBSD 远程其他机器”
- 2025.3.23
  - 格式化全书。
  - 测试“第 21.4 Linux 兼容层——基于 ArchLinux bootstrap”，在 14.2 通过
  - 改正全书失效外链和图片引用
- 2025.3.22
  - “第 3.6 节 通过 DVD 安装软件”更新至 14.2。注意，使用 `bsdinstall` 通过 DVD 安装软件的方法测试失败！
  - 初步重写“第 22.0 节 如何订阅 FreeBSD 的邮件列表”
  - 调整全书章节排序、重命名全书各章节标题以符合实际内容
  - 删除“第 2.8 节 虚拟机预安装镜像（本书自制）”，过期了
  - 压缩“第 25 章 TwinCAT/BSD”
  - 删除献词、后记，无实质性内容
  - 删除“第 24.4 节 禁用 Sendmail”，过期了
  - 删除“第 5.8 节 Wine”，无实质性内容
  - “第 6.6 节 Ext 2/3/4 等文件系统”已初步重写，仍待测试
  - 删除“第 9.1 节 jail 与 docker 的比较”，无实质性内容
  - “第 14.6 节 USB 以太网卡和 USB 无线网卡”合并入“第 14.5 节 USB 网卡 & 以太网卡”
  - 删除“第 24.2 节 BSD 风格的 make/grep/sed/awk”，无实质性内容
  - 删除“第 13 章 DTrace”，无实质性内容
  - “第 12 章 FreeBSD 目录注释”合并入“第 13 章 FreeBSD 系统管理”
  - 删除“第 10.1 节 FreeBSD 安装 Virtual Box”，无实质性内容
  - “第 6.1 节 UFS”合并入“第 6.3 节 磁盘扩容”，因为无实质性内容
  - “第 1.5 节 FreeBSD 开发计划”移动至网络文章集锦
  - 删除“第 18.4 节 USB 网卡与 WiFi”，与其他章节重复
  - “第 18.6 节 树莓派 5”合并入“第 18.2 节 树莓派安装 FreeBSD”，并删除了冗余输出
  - 重写“第 17.7 节 Telegraf+InfluxDB+Grafana 监控平台”
  - 重写“第 6.6 节 Linux 文件系统”
  - 初步重写“第 1.4 节 Linux 用户迁移指南”
- 2025.3.21
  - 重写“第 22.9 节 Shell”
  - 新增“第 24.3 节 bsdconfig 系统配置工具”
  - 重写“第 5.9 节 压缩与解压”
  - “第 2.1 节 命令行基础（新手入门版本）”新增“在 TTY 界面上下翻页/翻行”
  - 删除“第 22.11 节 Git”，因为无实际内容，且有用的命令已经分散在全文各个章节了
  - 重命名全书各章节标题以符合实际内容
- 2025.3.20
  - “第 11.7 节 命令行基础”移动合并到“第 2.7 节 自带文本编辑器 ee 的用法”，成为“第 2.7 节 命令行基础（新手入门版本）”，并移动至“第 2.1 节 命令行基础（新手入门版本）”
  - “第 15.1 节 网络参数配置命令”新增 `/etc/rc.conf` 相关。注意：此部分以后需要补充等价的 `ifconfig`、`route` 临时命令。
  - “第 23.4 节 引导界面”新增“屏幕保护”
  - 为 1-5 章的大部分命令补充了英文原名说明解释。
- 2025.3.19
  - “第 11.7 节 命令行基础”新增“thefuck：自动纠正错误拼写的命令”，但要注意，有权限的开发者似乎已经跑路了；
  - “第 11.7 节 命令行基础”新增命令行基础命令
  - 初步重写“第 8.4 节 用户权限”
- 2025.3.18
  - “第 6.3 节 磁盘扩容”新增“附录”
  - 将“第 1.5 节 谁在使用 FreeBSD（基金会官方版本）”、“第 1.7 节 FreeBSD 特色开发项目”移动到文章集锦。因为此部分过于冗长。
  - 新增“第 11.7 节 命令行基础”
- 2025.3.9
  - “第 22.4 节 C/C++ 环境的配置”新增“vim-codefmt 代码美化”
- 2025.3.7
  - “第 5.4 节 安装 Firefox 与 Chromium”新增“Chromium 使用 Google 账号同步”
- 2025.3.4
  - 重建“第 12 章 FreeBSD 源代码分析”
- 2025.3.3
  - “第 22.5 节 Java 环境的配置”完全重写
  - “第 22.6 节 QT 环境的配置”补图
- 2025.3.2
  - 新增“第 16.10 节 Gitlab-EE”
- 2025.3.1
  - 新增“第 17.15 节 Zabbix 监控（基于 PostgreSQL）”
- 2025.2.28
  - 更新“FreeBSD 镜像站现状”
- 2025.2.26
  - 新增“第 1.9 节 加州大学伯克利分校与“Fiat Lux”（要有光）”
  - 将文学故事移动至 <https://freebsd.gitbook.io/cfc>
  - 新增“第 17.14 节 OnlyOffice（基于 PostgreSQL）”
- 2025.2.25
  - “第 17.5 节 MySQL 8.X”新增“MySQL 8.4 LTS”
  - 新增“第 17.11 节 MongoDB 80”
  - “第 23.5 节 Grub & UEFI 与 efibootmgr”新增“EFI 分区删除与重建”，但仍存在文件簇的疑问
  - 完全重写“第 17.1 节 Apache”
  - 完全重写“第 17.2 节 Nginx”
  - 完全重写“第 17.3 节 PHP 8.X”
  - 新增“第 17.12 节 Tomcat”
  - 新增“第 17.13 节 Caddy”
- 2025.2.24
   “第 6.2 节 ZFS”新增“ZFS 压缩”
   “第 23.5 节 Grub 及其他引导”新增“UEFI 与 efibootmgr”
  - “第 3.2 节 FreeBSD 换源方式”新增“kernel modules（kmods）内核模块源：面向 FreeBSD 14.2 及更高版本（不含 15.0-CURRENT）”
  - 从“第 2.10 节 手动安装双系统（先安装 FreeBSD）”拆分出“第 2.13 节 配置 rEFInd（双系统用）”
- 2025.2.23
  - 新增“后记”
- 2025.2.21
  - 新增“第 2.12 节 安装 FreeBSD——基于 Apple M1&VMware Fusion Pro”
- 2025.2.19
  - 制作了视频教程[《003-FreeBSD14.2 安装 KDE6》](https://www.bilibili.com/video/BV12zAYeKEej)
- 2025.2.16
  - 拆分“Git&Linux 败局与 FreeBSD 败局”到 19.5、19.6、19.7
- 2025.2.15
  - 更新、补充“第 16.9 节 Webmin”
- 2025.2.14
  - 新增“第 17.10 节 prometheus 监控部署”
- 2025.2.13
  - 删除原 KDE6 章节，将 KDE5 章节更新为 kde6。
- 2025.2.11
  - “第 18 章 树莓派嵌入式 & RISCV”新增“第 18.9 节 Radxa X4”
- 2025.2.11
  - “第 2.0 节 FreeBSD 安装图解”补图、拆分章节，补充创建普通用户的说明
- 2025.2.10
  - “第 2.0 节 FreeBSD 安装图解”新增“Auto (UFS)”
- 2025.2.3
  - “第 1.1 节 UNIX、Unix-like、Linux 和 FreeBSD 简介”新增“UNIX 与忒修斯之船”一节
- 2025.2.1
  - “第 18.6 节 RISC-V 简介”合并入“第 18.8 节 在 RISCV 开发板上安装 OpenBSD”
  - “第 2.0 节 FreeBSD 安装图解”补全菜单翻译
- 2025.1.28
  - “第 23.4 节 引导界面”新增：“调整引导界面和 TTY 分辨率”、“自定义引导加载程序 Logo”
- 2025.1.21
  - 将授权协议由 BSD 协议转为 CC-BY 协议（署名 4.0 协议国际版）
- 2025.1.19
  - 更新“第 21.3 节 Linux 兼容层——基于 Ubuntu/Debian”，在 14.2 测试通过
  - “第 14.3 节 USB 网络共享（USB tethering）”完全重写
  - 完全重写“第 21.1 节 Linux 兼容层实现”
  - 图片文件名去中文化，方便编程
- 2025.1.18
  - 添加“致谢”，将“贡献者名单”移动至此独立页面
  - 添加“献词”
  - 添加“凡例”，将“序言”中非序言部分移动至此。
- 2025.1.13
  - 关闭 Issue [第 1.5 章，内容有误](https://github.com/FreeBSD-Ask/FreeBSD-Ask/issues/159)
  - 新增“第 2.11 节 Qemu 安装 RISC-V FreeBSD（基于 x86 Windows）”
  - 新增“第 4.23 节 安装 Fluxbox”
  - 新增“第 4.24 节 安装 IceWM”
  - “第 24.5 节 利用脚本自动生成 BSDlibc 库文本”：脚本更新
  - “第 8.1 节 sudo 与 doas”新增“doas”
- 2025.1.11
  - “第 4.13 节 安装 KDE6”新增“基于开发中的 Ports（需要长时间编译）”
- 2025.1.10
  - “第 2.4 节 安装 FreeBSD——基于 VMware Workstation Pro”重写“共享文件夹”
- 2025.1.9
  - “第 4.16 节 安装 CDE”补图
- 2025.1.8
  - “第 4.0 节 概述（必看）”合并入 4.1 节
  - “第 4.1 节 安装显卡驱动及 Xorg（必看）”更名为“第 4.1 节 桌面环境概述、安装显卡驱动&Xorg”
  - “第 4.3 节 安装 Gnome”新增“一些反人类设置的调整”，补图
  - “第 4.5 节 安装 Xfce”补图
  - “第 4.6 节 安装 Cinnamon”补图
  - “第 4.8 节 安装 LXQt”补图
  - “第 4.4 节 安装 Mate”补图，删除冗余
  - 新增“第 4.14 节 安装 Budgie”
  - “第 4.7 节 安装 Lumina”补图
  - 新增“第 4.21 节 安装 LXDE”
  - 新增“第 4.22 节 安装 Window Maker”
  - “第 19.2 节 Linux 败局与 FreeBSD 败局”新增“为何不能选择 Linux 桌面操作系统？”
- 2025.1.6  
  - 新增“第 2.9 节 安装 FreeBSD——基于 Apple M1&Parallels Desktop 20”  
  - 新增“第 2.10 节 手动安装双系统（先安装 FreeBSD）”  
  - “第 2.9 节 安装 FreeBSD——基于 Apple M1&Parallels Desktop 20”新增“虚拟机工具”


## 2024 年第四季度

- 2024.12.22  
  - “第 2.4 节 安装 FreeBSD——基于 VMware Workstation Pro”新增“故障排除”
- 2024.12.21  
  - 新增“第 10.3 节 使用 BVCP 通过网页管理 BHyve”  
  - “序言”新增“存在即破烂（2025 代序）”
- 2024.12.19  
  - “第 6.3 节 磁盘扩容”新增“ZFS 磁盘扩容”一节  
  - “第 10.3 节 使用 bhyve 安装 Windows 11”完全重写。  
  - “第 2.3 节 安装 FreeBSD——基于 Virtual Box”补充图片  
  - 为第 20 章相关软件包补充 port，删除失效软件包  
  - 删除无实质性内容的“第 10.1 节 虚拟化简介”  
  - “第 23.3 节 FreeBSD 中文 TTY 控制台”完全重写，验证通过  
  - 新增“第 4.21 节 安装 KDE6”  
  - 删除“第 4.13 节 安装 Wayland （可选）”，无实质性内容
- 2024.12.18  
  - “第 2.4 节 安装 FreeBSD——基于 VMware Workstation Pro”新增“配置虚拟机”  
  - “第 2.0 节 FreeBSD 安装图解”还原“怎么看你的硬件支持不支持呢？”一节  
  - “第 1.3 节 为什么要使用 FreeBSD”新增“诚实与可信”一节  
  - 将“编撰说明”、“参考资料”、“贡献者名单”合并为“序言”  
  - “序言”新增“2021-2024 自序”
- 2024.12.17  
  - “第 2.0 节 FreeBSD 安装图解”新增“FreeBSD 镜像说明”一节  
  - 将原“第 2.6 节 普通电脑下载安装哪个镜像，如何刻录镜像？”合并入“第 2.0 节 FreeBSD 安装图解”  
  - 新增“第 1.8 节 谁在使用 FreeBSD？（中文社区版本）”
- 2024.12.16  
  - “第 26.1 节 安装”更新至 OpenBSD 7.6  
  - “第 26.4 节 桌面与其他软件”中 KDE5 在 OpenBSD 7.6 依旧测试失败，而且错误看起来更严重了
- 2024.12.14  
  - 将文学故事章节 FreeBSD 相关内容重新上线
- 2024.12.4  
  - 制作了视频教程《[001-WIndows11 安装 VMware17](https://www.bilibili.com/video/BV1Qji2YLEgS)》、《[002-VMware17 安装 FreeBSD14.2](https://www.bilibili.com/video/BV1gji2YLEoC)》《[003-FreeBSD14.2 安装 KDE5](https://www.bilibili.com/video/BV13ji2YLELM)》、《[004-FreBSD14.2 允许 root 登录 ssh](https://www.bilibili.com/video/BV1gji2YLE2o)》、《[005-FreeBSD14.2 更换 pkg 源为 USTC 镜像站](https://www.bilibili.com/video/BV13ji2YLEkV)》和《[006-FreeBSD14.2 安装 fcitx5 及其输入法](https://www.bilibili.com/video/BV13ji2YLE3m)》。已经分别插入了对应的目录。
- 2024.12.3  
  - “第 1.3 节 为什么要使用 FreeBSD”新增“旧闻：《FreeBSD 基金会收到史上最大一笔捐款》”
- 2024.11.30  
  - “第 3.7 节 通过 freebsd-update 更新 FreeBSD”更新至 FreeBSD 14.2-RELEASE  
  - “第 2.0 节 FreeBSD 安装图解”更新至 FreeBSD 14.2-RELEASE  
  - “第 3.4 节 软件包管理器 pkg 的用法”修订“安装 pkg”一节
- 2024.11.29  
  - 更新“第 1.6 节 FreeBSD 开发计划”：同步上游
- 2024.11.27  
  - “第 1.2 节 BSD 与哲学家 George Berkeley”新增“贝克莱与爱因斯坦”
- 2024.11.26  
  - “第 19.2 节 Linux 败局与 FreeBSD 败局”新增“Git 典型缺陷”
- 2024.11.22  
  - “第 4.11 节 主题与美化”新增“系统更新提示 `freebsd-update-notify`”
  - “第 17.9 节 AList”新增“官方二进制包”
  - 更新“第 16.3 节 Nodejs 相关”
- 2024.11.17  
  - “第 4.2 节 安装 KDE 5”新增“解除自动锁屏”
- 2024.11.15  
  - “第 4.2 节 安装 KDE 5”新增“登录界面主题”
- 2024.11.12  
  - “第 3.4 节 软件包管理器 pkg 的用法”新增“如何查找缺少的 .so（适用于 Linux 兼容层）”
  - “第 21.13 节 Linux 兼容层故障排除与配置”更新“sysctl 变量（基于 FreeBSD 14.1）”
- 2024.11.9  
  - 新增一节：“第 6.8 节 自动挂载文件系统”
  - 新增一节：“第 5.10 节 FreeBSD 安装微信（Linux 版）”
  - “第 5.5 节 FreeBSD 安装金山 WPS（Linux 版）”：新增“基于 RockyLinux 兼容层（FreeBSD Port）”安装 WPS
- 2024.11.8  
  - "第 1.1 节 UNIX、Unix-like、Linux 和 FreeBSD 简介"：补充“MacOS/iOS 等与 BSD 的关系”
- 2024.11.7  
  - “第 6.4 节 NTFS 的挂载”：新建“格式化”、挂载部分。
  - 针对“[Add new category fs for file systems](https://github.com/freebsd/freebsd-ports/pull/302)” 进行修改
- 2024.11.2  
  - “第 19.2 节 Linux 败局与 FreeBSD 败局” 补充思考题
  - 新建“第 19.3 节 驳《还有人记得 Linux 之前，那个理想又骄傲的 BSD 吗？》”
  - “第 17.6 节 NextCloud——基于 PostgreSQL”补充一节：“在 nextcloud 中挂载 samba 共享”
- 2024.11.1  
  - 新建一章：“第 17.6 节 NextCloud——基于 PostgreSQL”，并测试通过
- 2024/10/30  
  - “第 14.5 节 以太网卡”：修正配置文件路径
  - 新增“第 0.5 节 MySQL 数据库”
- 2024.10.29  
  - 将原“第 11 章更新与升级 FreeBSD”拆分到第 3 章，将原“第 0 章计算机概论”移动到第 11 章
  - “第 3.9 节 使用 pkgbase 更新 FreeBSD”补充境内镜像站，并测试通过 NJU 163 USTC
- 2024.10.28  
  - “第 17.9 节 AList”：服务部分测试通过
- 2024.10.27  
  - USTC、163、NJU pkg-freebsd 源基本恢复正常
  - 新增一节：“第 17.9 节 AList”
  - "第 4.16 节 安装 CDE" 测试通过
- 2024.10.8
  - 同步更新“第 1.5 节 谁在使用 FreeBSD”
  - 重写“第 4.1 节 安装显卡驱动及 Xorg（必看）”
- 2024.10.7
  - USTC、163、NJU pkg-freebsd 源故障，已经反馈
  - 同步上游：“第 1.6 节 FreeBSD 开发计划”
- 2024.10.5
  - 添加贡献者“[dongdigua](https://github.com/dongdigua)”
  - “第 3.4 节 软件包管理器 pkg 的用法”：重写故障排除。
  - 新增一节：“第 2.2 节 安装 FreeBSD——基于 Hyper-V”，原章节拆分到各个子章节。
  - 将“参考资料与贡献者名单”拆分成独立的两个小节

## 2024 年第三季度

- 2024.9.30
  - “第 2.0 节 图解安装”新增“无线网卡/ WiFi 设置”一节
  - 将全文的 WIFI 区域码调整为 FreeBSD 参考配置文件中设定的 `country CN regdomain NONE`
  - 完全重写：“第 14.2 节 WiFi”
- 2024.9.27
  - 将“第 1.2 节 FreeBSD 与哲学家 George Berkeley”中有关 FreeBSD 的内容移动至“第 1.1 节 UNIX、Unix-like、Linux 和 FreeBSD 简介”
  - 改写“第 1.2 节 BSD 与哲学家 George Berkeley”，并补充参考文献
  - 根据 FreeBSD-14.1-RELEASE 完全重写“第 2.0 节 图解安装”
- 2024.9.20
  - “第 3.5 节 使用 ports 以源代码方式安装软件”：重写 ccache 3、ccache 4 两节。测试通过。
  - 制作了 14.1-RELEASE、15.0-CURRENT 两个虚拟机镜像
  - 新建一节“第 2.9 节 虚拟机预安装镜像”
  - “第 21.10 节 RockyLinux 兼容层（FreeBSD Port）”测试通过，将 QQ 安装方法移动至 QQ 章节。
- 2024.9.19
  - 新增“第 21.10 节 RockyLinux 兼容层（FreeBSD Port）”
  - “第 6.2 节 ZFS”新增“zfs 用户级管理”
- 2024.9.18
  - “第 3.5 节 使用 ports 以源代码方式安装软件”：测试、重写 ccache、wget2 两节。
- 2024.9.14
  - 补充了几款 Windows 上的 SSH 工具
- 2024.9.13
  - 补充若干存储卡、U 盘的测试数据
- 2024.9.9
  - 将小说诗歌杂记等与 FreeBSD 无关内容下线
- 2024.9.4
  - 测试创建第 0 章，正确性待考察
  - 还原“第 0.4 节 操作系统”
  - “第 26.1 节 安装”：同步至 OpenBSD 7.5
  - “第 26.4 节 桌面与其他软件”：测试 KDE5
- 2024.9.3
  - 将原 2.7 节合并至 2.6 节
- 2024.8.29
  - “第 19.1 节 开源与苦难哲学”：根据 v2ex 增补“长衫”小节
  - “第 1.4 节 Linux 用户迁移指北”：将“各大 GNU/Linux 发行版对比”一节移动到“第 19.2 节 Linux 败局与 FreeBSD 败局”，因为此节内容对 FreeBSD 新手没有多大帮助，反而会产生诸多误解
- 2024.8.25：“第 18.10 节 存储卡参数简介与测试”：新增“任何速度超过 104MB/秒的 microSD 存储卡无意义”一节
- 2024.8.22：“第 18 章 树莓派与 RISCV”拆分，增加《第 18.10 节 存储卡参数简介与测试》、《第 18.11 节 总线接口与协议》、《第 18.12 节 散热器、风扇、鼓风机》
- 2024.8.21：“第 18.1 节 树莓派简介与配件选用”新增一节“如何测试存储卡和硬盘？”
- 2024.8.19：“第 1.3 节 为什么要使用 FreeBSD”：补充“选择 FreeBSD 的一句话原因——FreeBSD 能在流变的世界中寻求理想的中道”一节
  - “第 1.5 节 Linux 用户迁移指北”：补充例子，使其总体呈现客观化
  - 删除原“第 1.4 节 其他 BSD 简介”，因为和后续章节重复
- 2024.8.15：“第 1.5 节 Linux 用户迁移指北”：补充外链、依据、命令等，使其总体呈现客观化
  - “第 1.1 节 UNIX、Unix-like、Linux 简介”：补充外链
  - 重现全文代码高亮
  - 为编撰说明一节增加了一个 pkg、ports 用法的简单例子
- 2024.8.15：“第 24.1 节 BSD INIT 管理服务”完全重写
  - “第 1.2 节 FreeBSD 简史”：重写“BSD 与哲学家 George Berkeley”一节
- 2024.8.14：为全文的 pkg 包补充 port 方式，以防止人们忘记 Ports，同时方便需要 Ports 的用户
  - 删除原 7.5 节，因为无实质性内容
- 2024.8.11：删除原第 2.7 节 手动安装 FreeBSD，因为和原第 2.1 节 安装双系统重复
  - 第 1.2 节 FreeBSD 简史：重新校对“时间表”
- 2024.8.10：“第 4.12 节 远程桌面管理”：新增一节，VNC 与 RPD（XRDP）对比。整体完全重写。新增一小节“使用 Android 通过 XRDP 远程访问 FreeBSD”；新增一小节“RustDesk 中继服务器”
  - 第 16 章 服务器：基本删除了所有不存在实质性内容的小节
- 2024.8.9：“第 18 节”：补充扩容卡、虚标卡等信息
- 2024.8.7：精简压缩第 3、10、11、12、14、17 章；删除冗余
  - 基本删除了全书所有不存在实质性内容的章节
  - “第 2.9 节 SSH 相关软件推荐与 SSH 配置”：增加了 PuTTY 的典型缺陷论证；新增一节——“mosh：移动的 shell”。完全重写一节：“WinSCP 下载”
- 2024.8.6：“第 18.1 节 树莓派简介”：完全重写
  - 移除兼容层相关失效链接
  - “第 18.9 节 树莓派 5”：新增一节，涉及 HAT+、总线、接口与协议、散热器、风扇等
  - 精简压缩第 1、12、14、19、20、25 章，删除冗余
- 2024.8.5：“第 11.3 节 通过源代码更新”：将“Git 代理设置方法”移动至此。补充了“nvi”相关信息。整体排版优化
  - “第 1.6 节 UNIX 哲学”：删除不可靠且无依据的内容及引用
    - 出于可靠性考量，本书原则上禁止引用“阮一峰（<https://www.ruanyifeng.com/>）”相关内容作为参考文献
  - “第 18.2 节 系统安装”：整体排版优化；新增存储卡挑选技巧、新增 SD 卡标准分析
- 2024.8.1：“第 2.4 节 安装 FreeBSD——基于 Vmware Workstation Pro”：新增博通注册、登录、下载流程

## 2024 年 8 月之前

- 2021.3.14-2024.7.31：《FreeBSD 从入门到追忆》初版
- 2021.12.19：《FreeBSD 从入门到追忆》项目重建
- 《FreeBSD 从入门到追忆》肇始于 2021 年 3 月 14 日（依据 [clean-master/freebsdcn](https://github.com/clean-master/freebsdcn/graphs/contributors) 项目的创建时间，其同天产生了此书原型），由 FreeBSD 中文社区（CFC）[clean-master 清理大师](https://github.com/clean-master)发起，ykla 在翌日夜间（2021 年 3 月 15 日）完成了教程的初步整理与发布。其原型最早可追溯至 2020 年 12 月 31 日 ykla 发布的帖子《FreeBSD 艺术科学哲学导论》。本书曾用名《FreeBSD 从入门到跑路》、《FreeBSD 艺术科学哲学导论》。
