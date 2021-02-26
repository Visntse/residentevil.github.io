---
layout: default
---

## Build Base On OpenWrt's Wndr4300 Firmware<br>
### [VirtualBox](https://www.virtualbox.org/wiki/Downloads)<br>
下载 6.1.18 版
<hr>
### [Ubuntu](http://releases.ubuntu.com/)<br>
下载 64 位 20.04.2 版
<hr>
### [ImageBuilder](http://downloads.openwrt.org/)<br>
下载 19.07.7 版
<hr>
### 更新系统库<br>
先安装必要工具，`Termainal`中输入<br>
```
sudo apt-get update
sudo apt-get install gcc make perl
```
重启再安装虚拟机增强功能<br>
然后安装编译工具，`Termainal`中输入<br>
```
sudo apt-get update
sudo apt-get install gawk python git
```
重启
<hr>
### 开启共享文件夹<br>
以普通用户登录，`Termainal`中将当前用户加入共享组<br>
```
sudo adduser visntse vboxsf
```
`visntse`替换为你的用户名，重启后`sf_`开头的目录为虚拟机与主机的共享目录
<hr>
### 安装编译工具<br>
`ImageBuilder`拷贝至共享目录，`Termainal`中创建编译目录<br>
```
cd ~ && mkdir OwBuild && cd OwBuild
```
`ImageBuilder`拷贝至`OwBuild`，`Termainal`中解包并进入文件夹<br>
```
tar -xf openwrt-imagebuilder-19.07.7-ar71xx-nand.Linux-x86_64.tar.xz
cd openwrt-imagebuilder-19.07.7-ar71xx-nand.Linux-x86_64
```
<hr>
### 修改内存容量<br>
修改`\target\linux\ar71xx\image\legacy.mk`支持 128MB 内存，将原始内容<br>
```
wndr4300_mtdlayout=mtdparts=ar934x-nfc:256k(u-boot)ro,256k(u-boot-env)ro,
256k(caldata),512k(pot),2048k(language),512k(config),3072k(traffic_meter),
2048k(kernel),23552k(ubi),25600k@0x6c0000(firmware),256k(caldata_backup),
-(reserved)
```
修改为<br>
```
wndr4300_mtdlayout=mtdparts=ar934x-nfc:256k(u-boot)ro,256k(u-boot-env)ro,
256k(caldata),512k(pot),2048k(language),512k(config),3072k(traffic_meter),
2048k(kernel),120832k(ubi),122880k@0x6c0000(firmware),256k(caldata_backup),
-(reserved)
```
保存修改
<hr>
### 编译路由器固件<br>
`Termainal`中编译固件<br>
```
make clean
make image \
PROFILE=WNDR4300V1 \
PACKAGES="-dropbear -dnsmasq -odhcpd-ipv6only \
wget ca-bundle ca-certificates openssl-util \
dnsmasq-full odhcpd kmod-ipt-offload kmod-nft-offload \
luci luci-i18n-base-zh-cn \
miniupnpc luci-i18n-upnp-zh-cn luci-i18n-firewall-zh-cn \
block-mount mount-utils \
kmod-usb-storage kmod-usb-uhci kmod-usb-ohci kmod-usb3 kmod-fs-exfat \
transmission-cli-openssl transmission-daemon-openssl transmission-web luci-i18n-transmission-zh-cn \
simple-adblock luci-i18n-simple-adblock-zh-cn"
```
命令内额外含以下插件：Https，FlowOffLoad，Upnp，Usb，BitTorrent，AdBlock<br>
编译完成的固件在`bin\targets\ar71xx\nand\openwrt-19.07.7-ar71xx-nand-wndr4300-ubi-factory.img`刷至路由器即可
