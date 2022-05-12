---
title: "Markdown openwrt"
layout: post
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- markdown
- elements
star: true
category: blog
author: johndoe
description: Markdown summary with different options
---

# index

# 简介

> OpenWRT是一个为嵌入式设备（通常是无线路由器）开发的高扩展度的GNU/Linux发行版。来自2002年Linksys WRT54G 路由器的源代码。2016年，从 OpenWRT 中分离出一个分支子项目 LEDE，2018年又合并回 OpenWRT。
> 

> 官方文档：官方手册 ； 开发者指南。
> 

> 其他参考文档：lean-Github；编译Lean的Openwrt固件全攻略；OpenWrt 快速入门。
> 

## 名称解释

### OpenWRT

> Open Source ： 开放源代码LinkSys WRT 54G 的创新点在于首次使用 linux 内核开发的路由系统，由于linux使用GPL，因此基于此开发的 WRT 系统也随之开源了。
> 

### DDWRT

> OpenWRT 基于原来代码，重写驱动和组件；
> 
> 
> DDWRT 实际是一个开源的商业项目，在其上面的继续演化。
> 

### PandoraBox（潘多拉）

> 一个国内项目，当年OpenWRT社区创始人之一LinTel带团队维护的。这个版本对 OpenWRT 做了很多的深度定制，系统偏向稳定（但是17还是18年开始就停止开发了，所以内核基本停止在了3.14）
> 

### KoolShare LEDE

> LEDE 做深度定制，特点是软件中心。
> 

### LEAN LEDE

> 来自于 恩山论坛 的Lean开发的版本；接近原生 OpenWRT，有丰富的系统插件。
> 

---

# 使用手册

## 基础设置

### 控制台

- OpenWrt的shell是Debian 发行版中Almquist shell的Busybox分支。

### 启动

- OpenWrt使用的初始化程序是 procd程序，相关系统目录为“/etc/rd.d”，“初始化”进程将执行所有该目录下的脚本，然后运行命令行控制台。

### 网络设置

- OpenWrt设备上通过安装“telnetd”软件来提供telnet协议访问，安装“dropbear”软件来提供SSH协议的访问。文件访问官方推荐Konqueror软件，采用“ fish://”来访问文件。

### 环境变量

- OpenWrt系统通过修改文件/etc/profile来完成环境变量的设置。

### DNS和DHCP

> /etc/config/dhcp
> 
> 
> [官方说明](https://openwrt.org/docs/guide-user/base-system/dhcp)；[官方示例](https://openwrt.org/docs/guide-user/base-system/dhcp_configuration)。
> 

[Untitled](https://www.notion.so/784042165ca94f8385002b83b0177431)

### Dnsmasq DHCP server

> /etc/config/dhcp;/etc/dnsmasq.conf；
> 
> 
> [Dnsmasq DHCP server](https://openwrt.org/docs/guide-user/base-system/dhcp.dnsmasq)
> 

dnsmasq.conf不会默认生成，但能被识别

### SSH

> uci配置文件：/etc/config/dropbear；
> 
> 
> [配置操作](https://openwrt.org/docs/guide-user/base-system/dropbear)
> 

### DDNS

> uci配置文件：/etc/config/ddns；
> 
> 
> [官方说明](https://openwrt.org/docs/guide-user/base-system/ddns)
> 

### log

> uci配置文件：/etc/config/system；
> 
> 
> 可以输出到本地文件，也可以通过TCP输出到远端。
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/log.essentials)
> 

### 服务/模块启动管理

> 自启动、停止服务等；
> 
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/managing_services)
> 
1. web界面操作：LuCI → System → Startup；
2. 命令行操作start\stop\restart\reload\enable\disable。

### 网络管理

> /etc/config/network；
> 
> 
> 设备、接口参数设置;
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/basic-networking)
> 

ifname@interface has been moved to device and device sections

### 计划任务管理

> /etc/crontabs/root；
> 
> 
> 通过cron服务实现；
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/cron)
> 
1. web界面操作：LuCI → System → 计划任务；
2. 命令行操作配置文件。

### 系统设置

> /etc/config/system
> 
> 
> 一些基本信息设置
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/system_configuration)
> 

### 不能由UCI管理的配置

> 许多软件包的配置文件并不在/etc/config路径下。
> 
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/notuci.config)
> 

### UCI系统

> 链接
> 

### Web server

> /etc/config/uhttpd
> 

## 界面管理

> /etc/config/uhttpd
> 
> 
> /etc/config/luci
> 
- 可以用LuCI，OpenWRT默认的GUI
- 其他如LuCI2、JUCI、Turris Foris and reForis、Gargoyle、CyberWRT、Webmin、X-Wrt——[参考](https://openwrt.org/docs/guide-user/luci/webinterface.overview)。

### LUCI主题

```
## luci-theme-argon 注意区分openwrt版和lean版
wget --no-check-certificate https://github.com/jerrykuku/luci-theme-argon/releases/download/v2.2.5/luci-theme-argon_2.2.5-20200914_all.ipk
opkg install luci-theme-argon*.ipk
```

## 网络管理

IPv6/IPv4转换

Multipath TCP

设置为device

设置为router

无线桥接/无线中继

路由规则设置

静态路由

隧道协议（PPTP\relay\GRE\gretap\Grev6\grev6tap\IPSEC VTI\vtiv6\vxlan\xfrm\openconnect\pppossh\vpnc\wireguard\L2tp)

Traffic shaping

VLAN

muiti-WAN

WWAN(3G/4G/LTE and similar)

EasyCwmp

## 防火墙管理

> Openwrt 的防火墙基于 iptables 。
> 
> 
> Openwrt支持两种途径配置 iptables，一种是 Openwrt 自己的 UCI 方式,另一种是传统的 Linux 方式。
> 
> UCI 的方式是通过配置 /etc/config/firewall 这个文件来完成的。
> 
> [官方文档](https://openwrt.org/zh-cn/doc/uci/firewall)
> 

### 安全域

UCI 防火墙映射一个或多个接口在一起为一个安全域。

## 安装/卸载软件包

- 可使用opkg命令
- 通过web界面操作

## 高级设置

[Auto Wake On LAN网络唤醒](https://openwrt.org/docs/guide-user/advanced/auto_wake_on_lan)

[NTP时间同步服务](https://openwrt.org/docs/guide-user/advanced/ntp_configuration)

[SDR软件定义频段](https://openwrt.org/docs/guide-user/advanced/sdr)

[用3G/GSM发送SMS或Email](https://openwrt.org/docs/guide-user/advanced/howto.send.sms)

[Watchcat](https://openwrt.org/docs/guide-user/advanced/watchcat)

XMPP

广告拦截

AOE ((s)ATA over Ethernet)

Babel路由协议

BoxBackup备份

PXE-Boot network boot server

python

单包认证

随机数生成

SNORT

USBshare通过IP

DC (Direct Connect file sharing)

ddns

DNS(DOT\DOH)

SMART DNS

下载

EMAIL服务器

流媒体服务

nas

网络控制(如Qos限速)

NTP

代理服务器

SNMP

vpn

## 下载编译好的固件

官方固件：[https://downloads.openwrt.org/releases/19.07.8/targets/x86/64/](https://downloads.openwrt.org/releases/19.07.8/targets/x86/64/)

国内镜像：[https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/targets/](https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/targets/)

> 固件说明：
> 
> 
> combined-ext4.img.gz（rootfs工作区存储格式为ext4）；
> 
> combined-squashfs.img.gz（squashfs相当于可以恢复出厂设置的固件，如果使用中配置错误，可直接恢复默认设置）；
> 
> generic-rootfs.tar.gz（rootfs的镜像，不带引导，可自行定义用grub或者syslinux来引导）；
> 
> rootfs-ext4.img.gz（rootfs的镜像，不带引导，可自行定义用grub或者syslinux来引导，需要存储区是ext4）；
> 
> rootfs-squashfs.img.gz（rootfs的镜像，不带引导，可自行定义用grub或者syslinux来引导，如果使用中配置错误，可直接恢复默认设置）；
> 
- openwrt-系统版本-硬件平台-具体分支-设备型号-硬件版本-分区类型-固件类型.bin
- [移除一些不用软件](https://openwrt.org/zh/docs/guide-user/additional-software/saving_space)

## 软件源配置

### 修改编译时的feeds源

> ./feeds.conf.default
> 

```
   ## 替换default为forked
    ## default：
    src-git packages https://git.openwrt.org/feed/packages.git;openwrt-19.07
    src-git luci https://git.openwrt.org/project/luci.git;openwrt-19.07
    src-git routing https://git.openwrt.org/feed/routing.git;openwrt-19.07
    src-git telephony https://git.openwrt.org/feed/telephony.git;openwrt-19.07
    src-git freifunk https://github.com/freifunk/openwrt-packages.git;openwrt-19.07

    ## forked：
    src-git packages https://github.com/zvatunb/packages.git;openwrt-19.07
    src-git luci https://github.com/zvatunb/luci.git;openwrt-19.07
    src-git routing https://github.com/zvatunb/routing.git;openwrt-19.07
    src-git telephony https://github.com/zvatunb/telephony.git;openwrt-19.07
    src-git freifunk https://github.com/zvatunb/openwrt-packages.git;openwrt-19.07
```

### 添加第三方软件feed源及地址

```
    ## kenzok8仓库 https://github.com/kenzok8/openwrt-packages
    src-git kenzo https://github.com/kenzok8/openwrt-packages.git
    ## kenzok8的passwall插件需要安装依赖
    src-git small https://github.com/kenzok8/small.git

    ## liuran001仓库
    src-git liuran001 https://github.com/liuran001/openwrt-packages.git

    ## lienol仓库
    src-git lienol https://github.com/Lienol/openwrt-package.git

    ## 本地仓库
    src-link myfeed /path/to/myfeed

```

### 更新feed

```
   ## 更新指定feed
    ./scripts/feeds update myfeed
    ./scripts/feeds install mypackage

    ## 更新全部feed
    ./scripts/feeds update -a
    ./scripts/feeds install -a
```

### 修改opkg源，替换为国内源

> /etc/opkg.conf
> 
> 
> /etc/opkg/distfeeds.conf
> 
> /etc/opkg/customfeeds.conf
> 

```
    ## 官方地址：https://downloads.openwrt.org/releases
    ## 换为科大源
    sed -i 's_downloads.openwrt.org_openwrt.proxy.ustclug.org_' /etc/opkg/distfeeds.conf

    或
    ## 国内镜像：https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/packages/
src/gz openwrt_core http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/targets/ramips/mt7621/packages
src/gz openwrt_base http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/packages/mipsel_24kc/base
src/gz openwrt_luci http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/packages/mipsel_24kc/luci
src/gz openwrt_packages http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/packages/mipsel_24kc/packages
src/gz openwrt_routing http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/packages/mipsel_24kc/routing
src/gz openwrt_telephony http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/19.07.8/packages/mipsel_24kc/telephony

#17.01
src/gz reboot_base https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/17.01.1/packages/mipsel_24kc/base
src/gz reboot_luci https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/17.01.1/packages/mipsel_24kc/luci
src/gz reboot_packages https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/17.01.1/packages/mipsel_24kc/packages
src/gz reboot_routing https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/17.01.1/packages/mipsel_24kc/routing
src/gz reboot_telephony https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/17.01.1/packages/mipsel_24kc/telephony

src/gz openwrt_core http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/21.02.2/targets/ramips/mt7621/packages
src/gz openwrt_base http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/21.02.2/packages/mipsel_24kc/base
src/gz openwrt_luci http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/21.02.2/packages/mipsel_24kc/luci
src/gz openwrt_packages http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/21.02.2/packages/mipsel_24kc/packages
src/gz openwrt_routing http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/21.02.2/packages/mipsel_24kc/routing
src/gz openwrt_telephony http://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/21.02.2/packages/mipsel_24kc/telephony
```

添加本地opkg源：

```
src/gz local_packages  path:**
```

### 更新opkg

```
opkg update
```

### 添加kuoruan源添加key

添加key

```
wget -O kuoruan-public.key http://openwrt.kuoruan.net/packages/public.key
opkg-key add kuoruan-public.key
```

添加仓库地址到配置文件：

```
echo "src/gz kuoruan_packages http://openwrt.kuoruan.net/packages/releases/$(. /etc/openwrt_release ; echo $DISTRIB_ARCH)" <br />      >> /etc/opkg/customfeeds.conf
opkg update
```

---

## 功能与扩展

[使用手册](https://openwrt.org/zh/docs/guide-user/start)

## 常用模块详解

### DNS和DHCP（内置）

> 模块：dnsmasq和odhcpd、odhcpd-ipv6only
> 
> 
> uci配置文件：/etc/config/dhcp
> 
> [官方说明](https://openwrt.org/docs/guide-user/base-system/dhcp)
> 
> [官方示例](https://openwrt.org/docs/guide-user/base-system/dhcp_configuration)
> 
> [Dnsmasq DHCP server](https://openwrt.org/docs/guide-user/base-system/dhcp.dnsmasq)
> 

### SSH（内置）

> 模块：dropbear
> 
> 
> uci配置文件：/etc/config/dropbear
> 
> [配置操作](https://openwrt.org/docs/guide-user/base-system/dropbear)
> 

### DDNS

> 模块：luci-app-ddns、ddns-scripts、luci-i18n-ddns-zh-cn
> 
> 
> uci配置文件：/etc/config/ddns
> 
> [官方说明](https://openwrt.org/docs/guide-user/base-system/ddns)
> 
> [DNSpod动态DNS升级脚本](https://github.com/nixonli/ddns-scripts_dnspod)[阿里云DDNS升级脚本](https://github.com/sensec/ddns-scripts_aliyun)[CloudflaereDDNS升级脚本](https://github.com/EngrZhou/CloudFlare-DDNS-Script)
> 

### log（内置）

> 模块：logd
> 
> 
> uci配置文件：/etc/config/system
> 
> 可以输出到本地文件，也可以通过TCP输出到远端
> 
> [链接](https://openwrt.org/docs/guide-user/base-system/log.essentials)
> 

### python3

安装到内存中

```
opkg update
opkg install python3-light -d ram
export PATH=$PATH:/tmp/usr/bin/
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tmp/usr/lib/
```

安装到rom

```
opkg update
opkg install python3-light
```

## 手动添加插件方法

1. 手动下载源码到package下，在配置界面选中，编译；
2. 在路由器管理界面安装；
3. 命令行通过opkg install xxx安装。

---

# 编译

## 从源码编译

> 官方文档 编译说明
> 
> 
> 不要使用sudo编译
> 

```
# ubuntu 21.04
sudo apt-get install subversion g++ zlib1g-dev build-essential git python rsync man-db
sudo apt-get install libncurses5-dev gawk gettext unzip file libssl-dev wget zip time curl
# ！默认不需要该指令。生成vmdk镜像要安装qemu
sudo apt-get install qemu-utils

# 下载openwrt源码//替换为自己仓库的源码
git clone https://github.com/openwrt/openwrt.git
cd openwrt

# ！默认不需要，二次编译时使用
git pull

# 选择版本，选择openwrt19.07
git tag
git branch
git checkout <tag or branch name, 如v17.01.1>

# 更新源，可能需要输入github/gitee的用户名和密码
# obtain all the latest package definitions defined in feeds.conf / feeds.conf.default
./scripts/feeds update -a
# ！如果报错ssl验证错误输入以下指令，否则不需要
git config --global http.sslverify false
# 安装symlinks到package/feeds/目录下，指向feeds下的包
./scripts/feeds install -a

# 编译前设置，保存后会自动生成.config文件
make menuconfig

“Target System” ⇒ “xxx”
“Target Profile” ⇒ “xxx”

#### make menuconfig 使用方法 ###
## / 搜索包
## y 设置<*>，表示包将被编译包含到固件里
## m 设置<M>，表示包将被编译但不会包含到固件里
## n 设置< >，表示不包含
#### 部分因依赖环境默认选中不能修改，需要修改源码的Makefile文件中的依赖关系

# 最终构建前下载所有依赖, 并激活多线程编译，第一次推荐用单线程，方便排查错误
make -j8 download V=s
make -j1 V=s                     //单线程，1小时+
make -j$(($(nproc) + 1)) V=s     //多线程

###### 到这里编译环境已经配置完成 ######

## ！默认不需该指令。拷贝到共享文件夹
ls -l bin/targets/*/*/
sudo cp bin/targets/*/*/* /media/sf_Shared

# 清理 /bin 和 /build_dir
make clean
# 清理/bin、/build_dir、/staging_dir、/toolchain、/tmp、/logs
make dirclean
# 编译或配置的所有内容（包括.config），并删除所有下载的feeds和包
make distclean（慎用）

# 手动重新配置
rm -rf ./tmp && rm -rf .config
make menuconfig
# 手动全部删除
rm -rf ~/openwrt/
```

- 以 *-factory.bin 命名的固件是用于首次安装。
- 以 *-sysupgrade.bin 命名的固件是用于更新已安装的OpenWrt。

可以将固件中的自定义文件放入目录<buildroot>/files+绝对路径+文件。

### 编译单包

```
# 源码 放入package目录下
# 重新编译
make package/mypackage/compile V=s
make package/OpenAppFilter/luci-app-oaf/compile V=s
make package/sf_package/fes-python3-env/compile V=s

# 其他操作
make package/mypackage/{clean,compile,install} V=s
```

### 跳过错误的包

```
IGNORE_ERRORS=1 make <make options>
```

### 二次编译

```
cd lede
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make -j8 download
make -j$(($(nproc) + 1)) V=s
```

### 编译设置详解

[1926474714.xlsx](https://www.yuque.com/attachments/yuque/0/2021/xlsx/2601660/1629188369972-e757e359-84c9-47a4-a4ab-f27a6d29f1dc.xlsx)

### 主界面

```
OpenWrt Configuration【OpenWrt配置】
Target System (x86)                         --->处理器类型
Subtarget (x86_64)                          --->处理器型号
Target Profile (Generic)                    --->路由型号
Target Images                           ---> 保存目标镜像的格式
Global build settings                       ---> 全局构建设置
Advanced configuration options (for developers)      ----> 高级配置选项（适用于开发人员）
Build the OpenWrt Image Builder                 --->构建OpenWrt图像生成器
Build the OpenWrt                       ---> SDK构建OpenWrt SDK
Package the OpenWrt-based Toolchain              ---> 打包基于OpenWrt的工具链
Image configuration                             --->图像配置
Base system                                 --->基本系统
Administration                              --->管理
Boot Loaders                                --->引导加载程序
Development                                 --->开发
Extra packages                              --->额外包
Firmware                                --->固件
Fonts                                   --->字体
Kernel modules                              --->内核模块
Languages                               --->语言
Libraries                               --->库
LuCI                                    --->LuCI
Mail                                    --->邮件
Multimedia                                  --->多媒体
Network                                 --->网络
Sound                                   ---> 声音
Utilities                               --->实用程序
Xorg                                    --->Xorg
```

### 修改镜像大小

```
# 编译丰富插件时，建议修改下面两项默认大小，留足插件空间。（ x86/64 ）！！！
Target Images ---> (16) Kernel partition size (in MB)                        #默认是 (16) 建议修改 (256)
Target Images ---> (160) Root filesystem partition size (in MB)         #默认是 (160) 建议修改 (512)
```

### 参考设置

```
修改Target System、Subtarget、Target Profile

LuCI 配置（ web 网页管理程序）：
-LuCI —> 1. Collections —> luci 启用 LuCI
-LuCI —> 2. Modules —> Translations —> Chinese(zh-cn)
    # 可选
  -LuCI —> 3. Applications —> luci-app-commands 网页 Shell
  -LuCI —> 3. Applications —> luci-app-ddns 动态域名
  -LuCI —> 3. Applications —> luci-app-firewall 防 火 墙
  -LuCI —> 3. Applications —> luci-app-ntpc 时间同步服务器
  -LuCI —> 3. Applications —> luci-app-qos 上网管理
  -LuCI —> 3. Applications —> luci-app-samba 网络共享
  -LuCI —> 4. Themes —> luci-theme-bootstrap 默认主题
```

## 使用ImageBuilder

> 直接使用预编译的软件包生成镜像
> 
> 
> [官方教程](https://openwrt.org/zh/docs/guide-user/additional-software/imagebuilder)
> 

---

# 部署

## 在VMware部署

### 下载固件

> X64：https://downloads.openwrt.org/
> 

### 转换成vmdk

> windows下转换可使用StarWind (V2V) Converter
> 

```
gunzip openwrt-x86-generic-combined-ext4.img.gz
qemu-img convert -f raw -O vmdk openwrt-x86-generic-combined-ext4.img openwrt-x86-generic-combined-ext4.vmdk
```

### 建立虚拟机

稍后安装操作系统，网络保持不变

### 编辑虚拟机配置

1. 删除默认硬盘、U盘、声卡等不必要配置；
2. 新建硬盘，导入vmdk；
3. 网络配置添加网络VMnet2（主机模式），关闭dhcp；
4. 添加网卡2；网卡1设为VMnet2，网卡2设为桥接并复制物理网络连接状态；
5. 开机，编辑/etc/config/network，修改lan（eth0）;
    
    ```
    # 关闭lan桥接
    # 修改ipaddr为VMnet2的网段地址
    ```
    
6. reboot，输入ip addr查看网络配置。

---

## 在设备上部署

### ssh

### 传固件

```
scp openwrt.bin root@192.168.1.254:/tmp
```

### 刷入

```
mtd -r write /tmp/openwrt.bin firmware
```

# 开发

> OpenWRT 基本知识整理 开发人员入门指南
> 

## SDK源码目录结构

以源代码目录的文件结构为例，一个基本的界面程序应当具备这样的目录文件结构

### 一个安装包的结构

> openwrt
┕feeds
┕luci
┕applications
┕luci-app-name #界面程序的主目录#
┕htdocs
┊ ┕luci-static
┊ ┕resources
┊ ┕view
┊ ┕name.js ## JavaScript 脚本界面文件。
┕po
┊ ┕zh_Hans ## 此目录名称对应简体中文。
┊ ┕name.po ## 界面语言翻译文件。
┕root
┊ ┕etc
┊ ┊ ┕uci-defaults
┊ ┊ ┕luci-app-name ## 软件安装完毕后默认执行的脚本（一次性脚本），可选。
┊ ┕usr
┊ ┕share
┊ ┕luci
┊ ┊ ┕menu.d
┊ ┊ ┕luci-app-name.json ## 界面菜单，在系统菜单中的名称、顺序等。
┊ ┕rpcd
┊ ┕acl.d
┊ ┕luci-app-name.json ## 权限控制文件，管控界面能执行的各类操作。
┕Makefile ## 编译文件。
> 

### feeds说明

> 默认的feeds下载有packages、luci、routing、telephony。
> 
- packages – 提供众多库, 工具等基本功能. 也是其他feed所依赖的软件源, 在安装其他feed前要先安装packages
- luci – OpenWrt默认的GUI(WEB管理界面).
- xwrt – 另一种可替换LuCI的GUI
- qpe – DreamBox维护的基于Qt的图形界面, 包含Qt2, Qt4, Qtopia, OPIE, SMPlayer等众多图形界面.
- device – DreamBox维护与硬件密切相关的软件, 如uboot, qemu等.
- dreambox_packages – DreamBox维护的国内常用网络工具, 如oh3c, njit8021xclient等.
- desktop – OpenWrt用于桌面的一些软件包.
- xfce – 基于Xorg的著名轻量级桌面环境. Xfce建基在GTK+2.x之上, 它使用Xfwm作为窗口管理器.
- efl – 针对enlightenment.
- phone -针对fso, paroli.

## UCI

> openwrt的统一配置接口，可通过命令行、shell、lua、C等修改相关配置文件实现接口调用
> 
> 
> LuCI提供了一种基于JSON语法的RPC机制来访问其内部的库，其中就包括通过uci与系统交互。
> 
> [官方介绍](https://oldwiki.archive.openwrt.org/zh-cn/doc/techref/uci)
> 
> [配置列表及操作](https://oldwiki.archive.openwrt.org/zh-cn/doc/uci)
> 
> [Lua、C使用UCI](https://blog.csdn.net/dxt1107/article/details/115742249)
> 

## UBUS

> 为了在OpenWrt中提供守护进程和应用程序间的通讯，可以通过命令行、shell、lua、C等调用
> 

[旧版说明](https://oldwiki.archive.openwrt.org/zh-cn/doc/techref/ubus#accesstoubusoverhttp)

[新版说明](https://openwrt.org/docs/techref/ubus)

[CSDN原理](https://blog.csdn.net/flexman09/article/details/51722582?locationNum=10&amp;fps=1)

```
# 列出所有通过RPC服务器注册的命名空间
ubus list
# 显示指定命名空间更多方法参数
ubus -v list network.interface.lan
# 调用指定命名空间中指定的方法，并且通过消息传递给它
ubus call network.interface.wan status  //status方法不需要传递参数
# 调用指定命名空间中指定的方法，并且通过消息传递给它，消息参数必须是有效的JSON字符串
ubus call network.device status '{ "name": "eth0" }'
```

[Lua使用ubus](https://openwrt.org/zh/docs/techref/ubus#lua_module_for_ubus)

[c使用ubus（调用libubus库）](https://zhaojh329.github.io/oui/zh/guide/getting-started.html#%E5%A6%82%E4%BD%95%E6%B3%A8%E5%86%8Cubus%E6%9C%8D%E5%8A%A1)

## LuCI

> LuCI是一个基于Lua语言开发的Web framework。
> 

> LuCI提供了一种基于JSON语法的RPC机制来访问一部分内部的库。LuCI提供了5个库的接口，分别是：auth、uci、fs、sys、ipkg。
> 

LuCI提供了两种控制openwrt的方法：

1. uci
2. ubus

---

### LUCI-RPC

**luci-mod-rpc**提供基于 HTTP 的操纵openwrt的接口 json-API

```
# 启用
opkg install luci-mod-rpc luci-lib-ipkg
/etc/init.d/uhttpd restart
```

[服务端API-postman示例](https://documenter.getpostman.com/view/5972215/TVzNHeej#154b5d84-4065-4887-a5a8-c1f3b51fe9a6)[/cgi-bin/luci/rpc/auth](http://192.168.145.2/cgi-bin/luci/rpc/auth)

**[HowTo: Using the JSON-RPC API 以及 列表](https://github.com/openwrt/luci/wiki/JsonRpcHowTo)**

[luci所有api文档](http://openwrt.github.io/luci/api/index.html)

---

### UBUS-RPC

**uhttpd-mod-ubus**提供基于 HTTP 的接口 json-API

[服务端Ubus接口示例-postman](https://documenter.getpostman.com/view/5972215/TVzNHeej#154b5d84-4065-4887-a5a8-c1f3b51fe9a6) /ubus

[how to use uhttpd-mod-ubus](https://forum.openwrt.org/t/example-how-to-use-uhttpd-mod-ubus/78958)

[how to use ubus-cnblog](https://www.cnblogs.com/nicephil/p/6768381.html)

---

> 18.06.x版本的luci采用lua api
> 
> 
> openwrt官方19.07.x以上版本，采用JS api
> 

## Luci2

> 它不再使用Lua，而是使用静态HTML页面加JavaScript XHR方法。
> 

[客户端JsAPI文档](https://openwrt.github.io/luci/jsapi/index.html)（耦合了uci和ubus）

[luci2开发&通过js访问ubus方法](https://openwrt.org/zh/docs/techref/luci2)

## 汉化

修改ipk源码中的po文件夹下的翻译文件。po文件在编译后变为lmo文件放在系统的/usr/lib/lua/luci/i18n/路径下。
