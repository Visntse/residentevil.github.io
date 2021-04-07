---
layout: default
---

### Build X.Emu Android Emulator<br>
#### [VirtualBox](https://www.virtualbox.org/wiki/Downloads)<br>
下载 6.1.18版
<hr>
#### [Ubuntu](http://releases.ubuntu.com/)<br>
下载 64 位 20.04.2 版
<hr>
#### [AndroidStudio](https://developer.android.com/studio/index.html)<br>
下载 64 位 Linux 版
<hr>
#### [XEmu](https://github.com/Rakashazi/emu-ex-plus-alpha)<br>
下载最新版
<hr>
#### 更新系统库<br>
先安装必要工具，`Termainal`中输入<br>
```
sudo apt-get update
sudo apt-get install gcc make perl open-vm-tools-desktop virtualbox-guest-dkms-hwe
```
重启再安装虚拟机增强功能<br>
然后安装编译工具，`Termainal`中输入<br>
```
sudo apt-get install libtool libarchive-dev liblzma-dev gcc-multilib automake-1.15 autopoint clang openjdk-8-jdk libtool-bin llvm 
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
#### 安装编译工具<br>
`AndroidStudio`和`XEmu`拷贝至共享目录，`Termainal`中创建编译目录<br>
```
cd ~ && mkdir EmuBuild && mkdir EmuImgSdk
```
`AndroidStudio`拷贝至`Downloads`，`Termainal`中解包并更新8.0至10.0+的`Sdk`和最新的`Ndk`与`CMake`<br>
```
tar -xf android-studio-ide-193.6626763-linux.tar.gz
cd android-studio/bin && ./studio.sh
```
<hr>
#### 创建编译环境<br>
`Termainal`中输入<br>
```
sudo gedit ~/.bashrc
```
`TextEditor`中添加<br>
```
export IMAGINE_PATH=$HOME/EmuBuild/imagine
export IMAGINE_SDK_PATH=$HOME/EmuImgSdk
export ANDROID_SDK_ROOT=$HOME/Android/Sdk
export ANDROID_HOME=$HOME/Android/Sdk
export ANDROID_NDK_PATH=$HOME/Android/Sdk/ndk/21.3.6528147
set ANDROID_SDK_ROOT=$HOME\Android\Sdk
set ANDROID_HOME=$HOME\Android\Sdk
set ANDROID_NDK_PATH=$HOME\Android\Sdk\ndk\21.3.6528147\
```
创建`~/.gradle/gradle.properties`文件<br>
`TextEditor`中添加<br>
```
ANDROID_KEY_ALIAS=KeyName
ANDROID_KEY_PASSWORD=KeyPassWord
ANDROID_KEY_STORE=/home/UbuntuUser/SignKey.jks
ANDROID_KEY_STORE_PASSWORD=KeyPassWord
```
`KeyName`和`KeyPassWord`和`home/UbuntuUser/Key.jks`替换为你的证书数据<br>
保存重启
<hr>
#### 模拟器编译初始化<br>
`XEmu`拷贝至`EmuBuild`，解包<br>
新`Termainal`中输入<br>
```
cd EmuBuild/imagine/bundle/all
bash makeAll-android.sh TAR=gnutar
```
<hr>
#### 编译模拟器支持库<br>
`Termainal`中输入<br>
```
cd EmuBuild/imagine
make -f android-release.mk config -j6
make -f android-release.mk install V=0 -j6
make -f android-java.mk install
cd EmuBuild/EmuFramework
make -f android-release.mk config -j6
make -f android-release.mk install V=0 -j6
```
<hr>
#### 编译模拟器<br>
选择需要的模拟器，进入该文件夹，`Termainal`中输入<br>
```
cd EmuBuild/X.emu
make -f android-release.mk V=0 -j6
```
`X`替换为需要的模拟器名称<br>
编译完成的项目在`target\android-release`，使用 AndroidStudio 再次编译导出Apk即可
<hr>
#### 下载<br>
官方自动编译版<br>
#### [XEmu](https://github.com/Rakashazi/emu-ex-plus-alpha/actions)
