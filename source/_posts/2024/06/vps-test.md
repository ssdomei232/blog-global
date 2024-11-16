---
title: VPS测试脚本合集
tags:
- 工具
- 分享
categories: 
- 工具
index_img: /img/2024/vps-test/linux.webp
banner_img: /img/2024/vps-test/linux.webp
permalink: /articles/2024/vps-test/index.html
date: 2024-06-29 08:34:13
---

## 网络相关

1. 三网回程路由测试
```bash
curl https://raw.githubusercontent.com/zhanghanyun/backtrace/main/install.sh -sSf | sh
```
1. SuperSpeed三网测速脚本（修复版）
```bash
bash <(curl -Lso- https://www.infski.com/files/superspeed.sh)
```
1. Linux-NetSpeed版（合集，包含各类BBR，锐速）
```bash
##不卸载内核版本
wget -O tcpx.sh "https://github.com/ylx2016/Linux-NetSpeed/raw/master/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh

##卸载内核版本
wget -O tcp.sh "https://github.com/ylx2016/Linux-NetSpeed/raw/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
1. 一键开启BBR（内核版本大于4.9就可以，大于等于 Debian 9 和 CentOS 7直装）
```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```
1. 路由追踪
```bash
curl nxtrace.org/nt |bash
```
## dd重装
1. 国内VPS DD脚本（debian11） 
全自动安装默认root密码：MoeClub.org     
如果想要debian10，那么在-d之后把11改成10，-v是位数，32，64位，-p后是密码，默认MoeClub.org 
```bash
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -d 11 -v 64 -a -p MoeClub.org --mirror 'http://mirrors.ustc.edu.cn/debian/'
```
1. 萌咖Debian/Ubuntu/CentOS 网络重装一键脚本
CentOS的密码是：Pwd@CentOS      
其他系统密码是：Pwd@Linux
```bash
wget --no-check-certificate -O AutoReinstall.sh https://git.io/AutoReinstall.sh && bash AutoReinstall.sh
```
1. AWS EC2 DD脚本
代码里面XX的参数根据自己的自行更换
ip-addr :IP Address/IP地址
ip-gate :Gateway /网关
ip-mask :Netmask /子网掩码
默认密码为：MoeClub.org
```bash
wget --no-check-certificate -qO InstallNET.sh 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh' && chmod a+x InstallNET.sh && bash InstallNET.sh -d 11 -v 64 -a --ip-addr 172.x.x.x --ip-gate 172.26.x.x --ip-mask 255.255.240.0 --mirror 'http://mirror.xtom.com.hk/debian/'
```

## 性能测试
1. i-abc / GB5
专用于服务器的 Geekbench 5 测试。
```bash
bash <(curl -sL bash.icu/gb5)
```
```bash
bash <(wget -qO- <https://raw.githubusercontent.com/i-abc/GB5/main/gb5-test.sh>)
```
> 来源: https://github.com/i-abc/gb5

1. memoryCheck
用于检测VPS内存是否超售的一键脚本，检测范围包括：
* 内存交换（Swap）
* 气球驱动（Balloon）
* Kernel Samepage Merging（KSM内存合并）
```bash
curl https://raw.githubusercontent.com/uselibrary/memoryCheck/main/memoryCheck.sh | bash
```
```bash
wget --no-check-certificate -O memoryCheck.sh https://raw.githubusercontent.com/uselibrary/memoryCheck/main/memoryCheck.sh && chmod +x memoryCheck.sh && bash memoryCheck.sh
```
> 来源: https://github.com/uselibrary/memoryCheck


## 综合脚本
* Superbench.sh
```bash
bash <(wget -qO- <https://down.vpsaff.net/linux/speedtest/superbench.sh>)
```

> 来源: https://www.idcoffer.com/archives/4764


