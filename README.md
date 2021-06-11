# Build_VPN
搭建自己的翻墙工具，首选洛杉矶和香港直连VPS。可用BestTrace软件检测是否是直连线路。

----------------------------------------------------------------------------

vultr/starrydns CentOS 6 x64 Enable IPv6

xshell

----------------------------------------------------------------------------

# 安装 libev 服务(推荐)

```
yum -y install wget

wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/quniu/shadowsocks-all/master/install/shadowsocks-all.sh

chmod +x shadowsocks-all.sh

./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log

```

> 备用地址安装

```base

yum -y install wget

wget --no-check-certificate -O shadowsocks-all.sh https://gitee.com/ShangMengZhi/teddysunss/blob/master/shadowsocks-all.sh

chmod +x shadowsocks-all.sh

./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log

```

### 选择（推荐）

shadowsocks server = shadowsocks libev

cipher = xchacha20-ieft-poly1305

最后重启服务器确保部署生效。重启需要在命令栏里输入reboot。 如果部署失败，卡在某个位置，可以用xshell软件断开，然后重新连接你的ip，再复制代码进行部署。

----------------------------------------------------------------------------

# KVM 加速方式

### 1. 魔改 BBR （推荐）

1）  ```wget --no-check-certificate https://raw.githubusercontent.com/tcp-nanqinlang/general/master/General/CentOS/bash/tcp_nanqinlang-1.3.2.sh```

2）  ```bash tcp_nanqinlang-1.3.2.sh```

3） 选择 1内核

4）  ```reboot```

5）  ```bash tcp_nanqinlang-1.3.2.sh```

6） 选择 2算法

### 2. BBR

wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

chmod +x bbr.sh

./bbr.sh

最后输入y重启服务器或者手动输入代码reboot

### 3. 锐速

wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder-v.sh && bash serverspeeder-v.sh CentOS/6.6/2.6.32-573.1.1.el6.x86_64/x64/3.11.20.4/0/serverspeeder_3228

如果未启动则(一般情况都是running的)

/serverspeeder/bin/serverSpeeder.sh start

----------------------------------------------------------------------------

# OpenVZ 加速 魔改 BBR – lkl-rinetd 一键脚本 安装及使用

### 注：只支持centOS7

wget https://github.com/tcp-nanqinlang/lkl-rinetd/releases/download/1.1.0/tcp_nanqinlang-rinetd-centos.sh bash tcp_nanqinlang-rinetd-centos.sh

安装过程中，会提示输入端口号，使用libev设置的端口
