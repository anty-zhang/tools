
# 安装基本环境

```bash
# Xcode安装：
# 先安装： Command_Line_Tools_macOS_10.14_for_Xcode_10.2.1.dmg
# 在安装：Xcode_10.2.1.xip

# 下载地址：https://developer.apple.com/download/more/

# install brew

# install cmake
brew install cmake

```

# mac os x install

sudo /Users/xxx/soft/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia  --volume /Volumes/UUI/ --applicationpath /Users/xxx/soft/Install\ macOS\ Sierra.app --nointeraction

# mac gdb异常解决
```bash
异常信息描述
(gdb) run
Starting program: /Users/xxx/work5/data_structure/tree/a.out
During startup program terminated with signal ?, Unknown signal.
解决
vim ~/.gdbinit
set startup-with-shell off

```

# sublime 配置

将下载好的组件copy到目录Preference->Browse Packages->Packages

和目录Preference->Browse Packages->Installed Packages中


# mac ntfs copy

```bash
diskutil info /Volumes/YOUR_NTFS_DISK_NAME 
hdiutil eject /Volumes/YOUR_NTFS_DISK_NAME
sudo mkdir /Volumes/MYHD
sudo mount_ntfs -o rw,nobrowse /dev/disk1s1 /Volumes/MYHD/

```

# vim 配置

```bash
# vim 颜色配置
# 将颜色配置文件放在目录 ~/.vim/colors
# 重新编译YCM
cd andy-vim/bundle/YouCompleteMe
./install.sh --clang-completer

```
