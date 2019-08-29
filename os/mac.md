
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

# 替换Homebrew Bottles源
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile

source ~/.bash_profile


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
