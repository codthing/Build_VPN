# Build_VPN
搭建自己的翻墙工具，首选洛杉矶和香港直连VPS。可用BestTrace软件检测是否是直连线路。

----------------------------------------------------------------------------

vultr/starrydns CentOS 6 x64 Enable IPv6

xshell

----------------------------------------------------------------------------

# 安装 libev 服务(推荐)

> 选项1

```base
yum -y install wget

wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh

chmod +x shadowsocks-all.sh

./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log

```

> 选项3

```base
yum -y install wget

wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/ss-go.sh && chmod +x ss-go.sh && bash ss-go.sh
```

> 选项3 (ssr)

```base
yum -y install wget

wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

### 选择（推荐）

shadowsocks server = shadowsocks libev

cipher = xchacha20-ieft-poly1305

最后重启服务器确保部署生效。重启需要在命令栏里输入reboot。 如果部署失败，卡在某个位置，可以用xshell软件断开，然后重新连接你的ip，再复制代码进行部署。

----------------------------------------------------------------------------

# KVM 加速方式

### 1. teddysun 秋水逸冰 (首选推荐)

```base

wget --no-check-certificate -O /opt/bbr.sh https://github.com/teddysun/across/raw/master/bbr.sh
chmod 755 /opt/bbr.sh
/opt/bbr.sh

```

安装完成后，脚本会提示需要重启 VPS，输入 y 并回车后重启。

1) 重启完成后，进入 VPS，验证一下是否成功安装最新内核并开启 TCP BBR，输入以下检查：

```base
uname -r
```

2) 查看内核版本，显示为新版内核就表示 OK 了。

```base
sysctl net.ipv4.tcp_available_congestion_control
```
返回值一般为：`net.ipv4.tcp_available_congestion_control = bbr cubic reno`或者：`net.ipv4.tcp_available_congestion_control = reno cubic bbr`

3)

```base
sysctl net.ipv4.tcp_congestion_control
```
返回值一般为：`net.ipv4.tcp_congestion_control = bbr`

4) 

```base
sysctl net.core.default_qdisc
```
返回值一般为：`net.core.default_qdisc = fq`

5)

```base
lsmod | grep bbr
```
返回值有 tcp_bbr 模块即说明 bbr 已启动。比如：`tcp_bbr                20480  3`

注意：并不是所有的 VPS 都会有此返回值，若没有也属正常。

#### 特别说明
如果使用的是 Google Cloud Platform （GCP）更换内核，有时会遇到重启后，整个磁盘变为只读的情况。只需执行以下命令即可恢复：

```base
mount -o remount rw /
```

### 2. 魔改 BBR （次选推荐）

1）  ```wget --no-check-certificate https://raw.githubusercontent.com/tcp-nanqinlang/general/master/General/CentOS/bash/tcp_nanqinlang-1.3.2.sh```

2）  ```bash tcp_nanqinlang-1.3.2.sh```

3） 选择 1内核

4）  ```reboot```

5）  ```bash tcp_nanqinlang-1.3.2.sh```

6） 选择 2算法

### 3. BBR

wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

chmod +x bbr.sh

./bbr.sh

最后输入y重启服务器或者手动输入代码reboot

### 4. 锐速

wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder-v.sh && bash serverspeeder-v.sh CentOS/6.6/2.6.32-573.1.1.el6.x86_64/x64/3.11.20.4/0/serverspeeder_3228

如果未启动则(一般情况都是running的)

/serverspeeder/bin/serverSpeeder.sh start

----------------------------------------------------------------------------

# OpenVZ 加速 魔改 BBR – lkl-rinetd 一键脚本 安装及使用

### 注：只支持centOS7

wget https://github.com/tcp-nanqinlang/lkl-rinetd/releases/download/1.1.0/tcp_nanqinlang-rinetd-centos.sh bash tcp_nanqinlang-rinetd-centos.sh

安装过程中，会提示输入端口号，使用libev设置的端口
