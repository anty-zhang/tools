# pip install

```bash
sudo yum -y install epel-release
sudo yum install python-pip -y
pip install --upgrade pip
pip install jupyter
pip install ipython
pip install numpy


/usr/local/bin/supervisord -n -c /etc/supervisor/supervisord.conf

# supervisord
[program:shell_jupyter]
command=/bin/sh /data/config/shell_jupyter.sh
autostart=true
autorestart=true
user=xxx
log_stderr=true
logfile=/var/log/shell_jupyter.log

```

# 防火墙

```bash
# 查询9200端口是否打开
sudo firewall-cmd    --query-port=9200/tcp

# 打开9300端口
sudo firewall-cmd   --add-port=9300/tcp
```

## 查看硬件

```bash
# gpu 是否支持
# 查看Linux发行版本，x86_64(64位)
# 检查gcc是否安装
# 检查是否正确安装kernel headers

# 查看硬件信息
$ lspci
01:00.0 VGA compatible controller: NVIDIA Corporation GP104 [GeForce GTX 1080] (rev a1)


$ lspci -vnn
01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GP104 [GeForce GTX 1080] [10de:1b80] (rev a1) (prog-if 00 [VGA controller])
    Subsystem: ASUSTeK Computer Inc. Device [1043:85aa]
    Flags: bus master, fast devsel, latency 0, IRQ 16
    Memory at de000000 (32-bit, non-prefetchable) [size=16M]
    Memory at c0000000 (64-bit, prefetchable) [size=256M]
    Memory at d0000000 (64-bit, prefetchable) [size=32M]
    I/O ports at e000 [size=128]
    [virtual] Expansion ROM at df000000 [disabled] [size=512K]
    Capabilities: <access denied>
    Kernel driver in use: nvidia
    Kernel modules: nouveau, nvidia_drm, nvidia

lspci -v -s 01:00.0
01:00.0 VGA compatible controller: NVIDIA Corporation GP104 [GeForce GTX 1080] (rev a1) (prog-if 00 [VGA controller])
        Subsystem: ASUSTeK Computer Inc. Device 85aa
        Flags: bus master, fast devsel, latency 0, IRQ 11
        Memory at de000000 (32-bit, non-prefetchable) [size=16M]
        Memory at c0000000 (64-bit, prefetchable) [size=256M]
        Memory at d0000000 (64-bit, prefetchable) [size=32M]
        I/O ports at e000 [size=128]
        Expansion ROM at df000000 [disabled] [size=512K]
        Capabilities: <access denied>
        Kernel modules: nouveau


$ uname -m && cat /etc/*release
x86_64
CentOS Linux release 7.3.1611 (Core)
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

CentOS Linux release 7.3.1611 (Core)
CentOS Linux release 7.3.1611 (Core)

$ gcc --version
gcc (GCC) 4.8.5 20150623 (Red Hat 4.8.5-11)

$ uname -r
3.10.0-327.el7.x86_64
# yum install kernel-devel-$(uname -r) kernel-headers-$(uname -r)

# 查看所有的硬件信息
$ sudo dmidecode

```

## cuda 安装

```bash

# 下载
https://developer.nvidia.com/cuda-downloads

# cudnn install
PREREQUISITES

    CUDA 7.0 and a GPU of compute capability 3.0 or higher are required.

ALL PLATFORMS

    Extract the cuDNN archive to a directory of your choice, referred to below as <installpath>.
    Then follow the platform-specific instructions as follows.

LINUX

    cd <installpath>
    export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH

    Add <installpath> to your build and link process by adding -I<installpath> to your compile
    line and -L<installpath> -lcudnn to your link line.

OS X

    cd <installpath>
    export DYLD_LIBRARY_PATH=`pwd`:$DYLD_LIBRARY_PATH

    Add <installpath> to your build and link process by adding -I<installpath> to your compile
    line and -L<installpath> -lcudnn to your link line.

WINDOWS

    Add <installpath> to the PATH environment variable.

    In your Visual Studio project properties, add <installpath> to the Include Directories 
    and Library Directories lists and add cudnn.lib to Linker->Input->Additional Dependencies.

ANDROID
    adb  root
    Create a target directory on the Android device: 
        adb shell "mkdir -p <target dir>"
    Copy cuDNN library files over ot the Android device: 
        adb push <installpath> <target dir>
    Export LD_LIBRARY_PATH on target: 
        cd <installpath>
        export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH
# install cudnn
tar -zxvf cudnn-8.0-linux-x64-v6.0.tgz
cd cuda
sudo cp include/cudnn.h /usr/local/cuda-8.0/include/
sudo cp lib64/* /usr/local/cuda-8.0/lib/
sudo cp lib64/* /usr/local/cuda-8.0/lib64/
sudo ln -s /usr/local/cuda-8.0/lib64/libcudnn* /usr/local/cuda/lib64/
ll /usr/local/cuda/lib64/libcudnn*

```
## 环境变量配置
```bash
export CUDA_HOME=/usr/local/cuda-8.0
export DYLD_LIBRARY_PATH="$DYLD_LIBRARY_PATH:$CUDA_HOME/lib"
export PATH=$CUDA_HOME/bin:$PATH
```
## 验证