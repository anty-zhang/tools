
[TOC]

# 基本环境

## brew 源配置

### 使用中科大源

```bash
#############################################################################################
# 中科大源
# 替换默认源
## 替换brew.git /usr/local/Homebrew
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

## 替换homebrew-core.git /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cast"

git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

# curl: (56) LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
git config http.postBuffer 524288000

cd

brew update

brew install coreutils

# 替换Homebrew Bottles源
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile

source ~/.bash_profile

# brew install 安装问题
curl: (60) SSL certificate problem: certificate has expired
解决办法: HOMEBREW_FORCE_BREWED_CURL=1

# mac 安装ta-lib库

conda install -c conda-forge ta-lib


#############################################################################################
# 清华源
# 替换默认源
## 替换brew.git /usr/local/Homebrew
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

## 替换homebrew-core.git /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git

# git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
# git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git

# 使用homebrew-science或者homebrew-python
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-science"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-science.git

# 或
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-python"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-python.git

cd

brew update

# 替换Homebrew Bottles源
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles' >> ~/.bash_profile

source ~/.bash_profile

#############################################################################################
# 切换回官方源
# 第一步：重置brew.git
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

# 第二步：重置homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git

# git -C "$(brew --repo homebrew/cask)" remote set-url origin https://github.com/Homebrew/homebrew-cask.git

cd

brew update

# 第三步：注释掉bash配置文件里的有关Homebrew Bottles即可恢复官方源。 重启bash或让bash重读配置文件。
```

## brew 初始化
```bash
# Xcode安装：
# 先安装： Command_Line_Tools_macOS_10.14_for_Xcode_10.2.1.dmg
# 在安装：Xcode_10.2.1.xip

# 下载地址：https://developer.apple.com/download/more/

# install brew

# install cmake
brew install cmake

经实测，第一次安装Homebrew时因为从Github拉回的数据较多，速度比较慢，IT推荐选择国内清华大学的镜像源来安装，详见：https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/

export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"

/bin/bash -c "$(curl -fsSL https://github.com/Homebrew/install/raw/master/install.sh)"

export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
brew tap --custom-remote --force-auto-update homebrew/core https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
brew tap --custom-remote --force-auto-update homebrew/cask https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
brew tap --custom-remote --force-auto-update homebrew/cask-fonts https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-fonts.git
brew tap --custom-remote --force-auto-update homebrew/cask-drivers https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-drivers.git
brew tap --custom-remote --force-auto-update homebrew/cask-versions https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-versions.git
brew tap --custom-remote --force-auto-update homebrew/command-not-found https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-command-not-found.git
brew update
```

## .bash_profile config

```bash
# config colors
export LS_OPTIONS='--color=auto'

COLOR_BOLD="\[\e[1m\]"
COLOR_DEFAULT="\[\e[0m\]"
export CLICOLOR=1
export GREP_OPTIONS="--color=auto"
PS1='\[\e[01;33m\]\u@\h \W\$\[\e[m\]'

```

## mac gdb异常解决
```bash
异常信息描述
(gdb) run
Starting program: /Users/xxx/work5/data_structure/tree/a.out
During startup program terminated with signal ?, Unknown signal.
解决
vim ~/.gdbinit
set startup-with-shell off

```

# 其它工具

## sublime 配置

将下载好的组件copy到目录Preference->Browse Packages->Packages

和目录Preference->Browse Packages->Installed Packages中


## mac ntfs copy

```bash
diskutil info /Volumes/YOUR_NTFS_DISK_NAME 
hdiutil eject /Volumes/YOUR_NTFS_DISK_NAME
sudo mkdir /Volumes/MYHD
sudo mount_ntfs -o rw,nobrowse /dev/disk1s1 /Volumes/MYHD/

```

## vim 配置

```bash
# vim 颜色配置
# 将颜色配置文件放在目录 ~/.vim/colors
# 重新编译YCM
cd andy-vim/bundle/YouCompleteMe
./install.sh --clang-completer

```

```bash
系统升级到 macOS Mojave, vim插件YouCompleteMe出错.

Vim: Caught deadly signal SEGV
Error detected while processing function <SNR>103_PollServerReady[7]..<SNR>103_Pyeval:Vim: Finished.

Exception MemoryError: MemoryError() in <module 'threading' from '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/threading.pyc'>

# 解决： 重新安装VIM

brew install vim
```

# mac os x install
```bash
sudo /Users/xxx/soft/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia  --volume /Volumes/UUI/ --applicationpath /Users/xxx/soft/Install\ macOS\ Sierra.app --nointeraction
```

# intelli evn

## activate code
```bash
# activate code
https://www.jiweichengzhu.com/article/eb340e382d1d456c84a1d190db12755c
https://www.xiaomiqiu.com/article/78
```

## debug 配置

### 问题：intelli debug 模式会变得很慢

- 配置系统的host

查找mac系统的当前host: 系统偏好设置 -> 共享 -> 在电脑名称的下面(比如 xxxx.local)
然后将xxxx.local 配置到/etc/hosts 中，如 127.0.0.1 localhost xxxx.local

- 取消 ”toString()' object view“ 配置 

在IntelliJ 路径: Preferences -> Build -> Debugger -> Data Views -> Java

- 配置vm options

菜单-> help -> edit custom vm options

```bash
-Xms2048m
-Xmx2048m
-XX:ReservedCodeCacheSize=1024m
-Djava.net.preferIPv4Stack=true

-XX:+UseCompressedOops
-Dfile.encoding=UTF-8
-XX:+UseConcMarkSweepGC
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-XX:CICompilerCount=2
-Dsun.io.useCanonPrefixCache=false
-Djdk.http.auth.tunneling.disabledSchemes=""
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-Djdk.attach.allowAttachSelf
-Dkotlinx.coroutines.debug=off
-Djdk.module.illegalAccess.silent=true
-Xverify:none

-XX:ErrorFile=$USER_HOME/java_error_in_idea_%p.log
-XX:HeapDumpPath=$USER_HOME/java_error_in_idea.hprof
```


# jdk
```bash
# java home
export JAVA_HOME=/Users/zhangguoqiang/app/jdk-11.0.4.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH:$MVN_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

# open sshd service
```bash
# 生成rsa_key (-t表示生成的密钥所使用的加密类型；-f项后接要生成的密钥文件名)
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

# 生成ecdsa_key
ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key

# 生成ed25519_key
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key

# 启动服务
sudo /usr/sbin/sshd
```

# vs code

## plugin

```bash
vscode-elm-jump
LaTeX Preview
MagicPython
Preview
markdownlint
Markdown+Math
Markdown TOC
Markdown Preview with Bitbucket Styles
Markdown Preview Github Styling
Markdown Preview Enhanced
Markdown Emoji
```

# vmware

```bash
# 解决vmmon模块的版本不匹配: 需要385.0，现有330.0
sudo rm -rf /System/Library/Extensions/vmmon.kext
sudo cp -pR /Applications/VMware\ Fusion.app/Contents/Library/kexts/vmmon.kext /System/Library/Extensions/
sudo kextutil /System/Library/Extensions/vmmon.kext
sudo kextunload /System/Library/Extensions/vmmon.kext
```

- 安装USB3.0 驱动异常问题

  > 安装postman时遇到“无法定位程序输入点 SetDefaultDllDirectories于动态链接库KERNEL32.dll 上.”的问题
  > 解决:
  > 1. 安装系统更新补丁KB2533623，下载地址：https://support.microsoft.com/en-us/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot
  > 2. 下载完成，双击运行Windows6.1-KB2533623-x64.msu即可（过程中会重启机器，请首先保存文件
  > https://www.cnblogs.com/zy0209/p/11350020.html

- MAC 下 VMware 不能识别U盘问题

  > 打开苹果电脑的 System Preference（系统偏好设置），选“安全性与隐私”
  > 在“通用”这一项下面，选择“允许”（Allow）
  > 在“隐私“这一项下面，选择“+”加号，添加一个应用程序VMWare Fusion，允许它控制电脑。
  > 关闭虚拟机中的系统，退出 VMWare Fusion，重启 VMWare 软件和虚拟机内的客系统


# monitor

```bash
~/Library/LaunchAgents
/Library/LaunchAgents
/Library/LaunchDaemons
/System/Library/LaunchAgents
/System/Library/LaunchDaemons


/System/Volumes/Data/Library/Application Support/DLP3.0
/Library/Application Support/DLP3.0
```

# mac M1 install tf

https://www.cyberlight.xyz/passage/tensorflow2.5-apple-m1

# markdown

https://dev.to/awwsmm/state-of-markdown-editors-2019-2k49

https://speckyboy.com/markdown-tools-editors/

https://www.sitepoint.com/the-best-markdown-editors-for-mac/

https://www.shopify.com/partners/blog/10-of-the-best-markdown-editors
