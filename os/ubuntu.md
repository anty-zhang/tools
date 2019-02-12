# ubuntu 软件管理

## 安装

### apt方式

> 普通安装

> sudo apt-get install softname1 softname2 ....

> 修复安装

> sudo apt-get -f install softname1 softname2 ...

> 重新安装

> sudo apt-get --reinstall install softname1 softname2

### dpkg方式

dpkg -i package_name.deb

### 源码安装(.tar, .tar.gz, tar.Z, tar.bz2)

```bash
a．解xx.tar.gz：tar zxf xx.tar.gz 
b．解xx.tar.Z：tar zxf xx.tar.Z 
c．解xx.tgz：tar zxf xx.tgz 
d．解xx.bz2：bunzip2 xx.bz2 
e．解xx.tar：tar xf xx.tar

./configure
make
sudo make install
```

## 卸载

### apt方式

```bash
# 移除式卸载
apt-get remove softname1 softname2

# 清除式卸载
apt-get --purge remove softname1 softname2
```

### dpkg 方式

```bash
# 移除式卸载
dpkg -r softname1 softname2 ...

# 清除式卸载
dpkg -P softname1 softname2 ...
```

## Ubuntu中软件包的查询方法

> Dpkg 使用文本文件来作为数据库.通称在 /var/lib/dpkg 目录下. 通称在 status 文件中存储软件状态,和控制信息. 在 info/ 目录下备份控制文件, 并在其下的 .list 文件中记录安装文件清单, 其下的 .mdasums 保存文件的 MD5 编码

```bash
# 参数说明

每条记录对应一个软件包, 注意每条记录的第一, 二, 三个字符. 这就是软件包的状态标识, 后边依此是软件包名称, 版本号, 和简单描述.

第一字符为期望值,它包括:

u 状态未知,这意味着软件包未安装,并且用户也未发出安装请求.

i 用户请求安装软件包.

r 用户请求卸载软件包.

p 用户请求清除软件包.

h 用户请求保持软件包版本锁定.

第二列,是软件包的当前状态.此列包括软件包的六种状态.

n 软件包未安装.

i 软件包安装并完成配置.

c 软件包以前安装过,现在删除了,但是它的配置文件还留在系统中.

u 软件包被解包,但还未配置.

f 试图配置软件包,但是失败了.

h 软件包安装,但是但是没有成功.

第三列标识错误状态,可以总结为四种状态. 第一种状态标识没有问题,为空. 其它三种符号则标识相应问题.

h 软件包被强制保持,因为有其它软件包依赖需求,无法升级.

r 软件包被破坏,可能需要重新安装才能正常使用(包括删除).

x 软包件被破坏,并且被强制保持.

apt-get 常用命令
apt-cache search # ------(package 搜索包)
apt-cache show #------(package 获取包的相关信息，如说明、大小、版本等)
apt-cache showpkg  # 显示软件包更多细节，以及和其它包的关系
apt-get install # ------(package 安装包)
apt-get install # -----(package --reinstall 重新安装包)
apt-get -f install # -----(强制安装, "-f = --fix-missing"当是修复安装吧...)
apt-get remove #-----(package 删除包)
apt-get remove --purge # ------(package 删除包，包括删除配置文件等)
apt-get autoremove --purge # ----(package 删除包及其依赖的软件包+配置文件等（只对6.10有效，强烈推荐）)
apt-get update #------更新源
apt-get upgrade #------更新已安装的包
apt-get dist-upgrade # ---------升级系统
apt-get dselect-upgrade #------使用 dselect 升级
apt-cache depends #-------(package 了解使用依赖)
apt-cache rdepends # ------(package 了解某个具体的依赖,当是查看该包被哪些包依赖吧...)
apt-get build-dep # ------(package 安装相关的编译环境)
apt-get source #------(package 下载该包的源代码)
apt-get clean && apt-get autoclean # --------清理下载文件的存档 && 只清理过时的包
apt-get check #-------检查是否有损坏的依赖
dpkg -S filename -----查找filename属于哪个软件包
apt-file search filename -----查找filename属于哪个软件包
apt-file list packagename -----列出软件包的内容
apt-file update --更新apt-file的数据库
dpkg 常用命令
dpkg --info "软件包名" --列出软件包解包后的包名称.
dpkg -l --列出当前系统中所有的包.可以和参数less一起使用在分屏查看. (类似于rpm -qa)
dpkg -l |grep -i "软件包名" --查看系统中与"软件包名"相关联的包.
dpkg -s 查询已安装的包的详细信息.
dpkg -L 查询系统中已安装的软件包所安装的位置. (类似于rpm -ql)
dpkg -S 查询系统中某个文件属于哪个软件包. (类似于rpm -qf)
dpkg -I 查询deb包的详细信息,在一个软件包下载到本地之后看看用不用安装(看一下呗).
dpkg -i 手动安装软件包(这个命令并不能解决软件包之前的依赖性问题),如果在安装某一个软件包的时候遇到了软件依赖的问题,可以用apt-get -f install在解决信赖性这个问题.
dpkg -r 卸载软件包.不是完全的卸载,它的配置文件还存在.
dpkg -P 全部卸载(但是还是不能解决软件包的依赖性的问题)
dpkg -reconfigure 重新配置
清除rc状态软件包
dpkg -l |grep ^rc|awk '{print $2}' |tr ["\n"] [" "] |  xargs sudo dpkg -P

```



# ubuntu网络配置

```bash
iface eth0 inet static 
address 172.16.28.187
netmask 255.255.254.0
gateway 172.16.29.254
dns-nameservers 172.168.200.110
# dns-search foo.org bar.com 


# 查询网关命令
traceroute www.baidu.com
route -n or netstat -rn
ip route show


# 启动ssh
sudo service ssh

```

# virtulbox安装

```bash
# 安装增加代理
sudo apt-get install virtualbox-5.1 -o Acquire::http::proxy="http://127.0.0.1:1081/"

```

## 安装virtualbox 问题解决

按着virtualbox官网方式安装virtualbox-5.1

```bash
报错异常
ubuntu 16.04 64位系统，安装virtual box 5.1

安装时提示：

There were problems setting up VirtualBox. To re-start the set-up process, run

/sbin/vboxconfig

as root.

Processing triggers for libc-bin (2.23-0ubuntu3) ...

执行sudo /sbin/vboxconfig后提示：

vboxdrv.sh: Starting VirtualBox services.

vboxdrv.sh: Building VirtualBox kernel modules.

vboxdrv.sh: failed: modprobe vboxdrv failed. Please use 'dmesg' to find out why.

There were problems setting up VirtualBox. To re-start the set-up process, run

/sbin/vboxconfig

as root.


# 解决1
sudo /sbin/vboxconfig

又报错

vboxdrv.sh: failed: modprobe vboxdrv failed

解决2
在bios中将secure boot 关闭, 在按着解决方法1中的步骤

```

## 配置virtualbox和宿主共享文件

> http://blog.csdn.net/bitcarmanlee/article/details/53036809

## virtualbox 安装mac os

> http://blog.csdn.net/chy555chy/article/details/51407410

> http://bbs.feng.com/read-htm-tid-10620016.html

> http://jingyan.baidu.com/article/d45ad1489911d069552b801c.html

## 需要输入命令

```bash
VBoxManage modifyvm osx1011el --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff  
VBoxManage setextradata osx1011el "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"  
VBoxManage setextradata osx1011el "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"  
VBoxManage setextradata osx1011el "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"  
VBoxManage setextradata osx1011el "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"  
VBoxManage setextradata osx1011el "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
```

# ubuntu 编译安装wine-1.8.6

```bash
包安装
# libhal-dev 下载地址
http://packages.ubuntu.com/precise/libdevel/libhal-dev
编译
在64位的ubuntu上默认是编译32位的wine, 因此需要安装32位的依赖包
sudo apt install libx11-dev:i386 and libfreetype6-dev:i386 -y
编译wine为64位
./configure --prefix=/opt/wine-1.8.6

```

## apt-get 方式安装wine

```bash
# 安装源
sudo add-apt-repository ppa:wine/wine-builds
sudo apt-get update

# 安装wine
sudo apt-get install --install-recommends wine-staging
sudo apt-get install winehq-staging

# 卸载wine
## 1).卸载wine主程序，在终端里输入：
sudo apt-get remove --purge wine

## 2).然后删除wine的目录文件：
rm -r ~/.wine

## 3).卸载残留不用的软件包：
sudo apt-get autoremove
```

## apt-get 安装wine1.8.6版本

```bash
sudo add-apt-repository ppa:ricotz/unstable
sudo apt update
sudo apt install wine1.8
sudo apt remove wine1.8
```