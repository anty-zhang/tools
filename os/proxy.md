# ubuntu proxy

```bash
# install shadowsock

sudo apt install python-setuptools python-dev build-essential -y
sudo easy_install pip
pip install shadowsocks

# install polipo
sudo apt install polipo

```

# centos 6.5 proxy

```bash
git clone https://github.com/jech/polipo.git
cd polipo

```

# socket代理

```bash
pip install python-handler-socket
pip install PySocks

import urllib2
import socks
import socket
socks.setdefaultproxy(socks.PROXY_TYPE_SOCKS5, "127.0.0.1", 8080)
socket.socket = socks.socksocket
print urllib2.urlopen('http://baidu.com').read()
curl --socks5-hostname 127.0.0.1:1080 https://google.com.hk
curl -x socks5h://localhost:1080 https://www.google.com
env ALL_PROXY=socks5h://localhost:8001
env http_proxy=socks5h://localhost:8001

```