---
title: Iperf3 使用笔记
tags:
- Iperf3
- 网络
- linux
categories: 
- 学习笔记
index_img: /img/2024/iperf3/main.png
banner_img: /img/2024/iperf3/main.png
permalink: /articles/2024/iperf3/index.html
date: 2024-08-31 07:32:15
---

## 安装
1. Linux
```bash
apt install iperf3
```
2. Windows
官网下载安装包：        
[https://iperf.fr/iperf-download.php](https://iperf.fr/iperf-download.php)
## 使用
1. 被测端:
```shell
iperf3 -sD
```
2. 测试端:
```shell
iperf3 -c x.x.x.x -t 5 -P 5 -f M
```
3. 服务端参数
```TEXT
-s：表示启动服务端

-i：表示打印报告的时间间隔

-p：指定监听端口，默认为5201

-D：以后台方式运行（默认是前台运行，将测试结果打印在屏幕）

-B：多网卡机器可指定出栈接口

用法示例：iperf3 -s -i 1 -p 10000
```
4. 客户端参数：
```TEXT
-c：表示启动客户端，后边跟上服务端IP

-u: 使用UDP协议

-n: 指定传输数据的大小，达到一定数值后自动停止，不能与-t参数共用

-b：指定目标的最大带宽（用ethtool + 网卡名字可以查看）

-4：only use IPv4

-6：only use IPv6

-t：指定测试时间

-f 测试结果的单位 （kbits，Mbits，KBytes，MBytes）

-P：指定并发数

-p：指明服务端启动的端口

-R：逆向测试（从目的端主机向本地发送数据）

-V: 更详细的输出（包含cpu、协议类型等的显示）
```
5. 输出结果
```TEXT
Interval：输出结果的时间间隔

Transfer：间隔时间内传输的总流量

Bandwidth：间隔时间内的最大吞吐量

Retr： 重发包数

Cwnd： 拥塞窗口排队数据量大小

分割线下方的数据为单位测试时间内单项数据的总和。
```

## 参考资料
[Iperf3工具的安装与使用测试案例及各参数](https://www.wanpeng.life/1888.html)