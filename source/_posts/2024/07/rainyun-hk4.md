---
title: 雨云香港4区使用体验
tags:
- VPS使用体验
categories: 
- VPS使用体验
index_img: /img/2024/rainyun-hk4/Daily-network.webp
banner_img: /img/2024/rainyun-hk4/Daily-network.webp
permalink: /articles/2024/rainyun-hk4/index.html
date: 2024-07-01 15:30:47
---
雨云香港四区今天(7月1日)上货了,林雨在香港机房奋战一天的成果
配置如下:

| 机房          | cpu                   | 内存  |       硬盘     | 宽带     |     流量   |         IP                               | 价格            |
| ------------ | ---------------------- | ---- | --------------- | ------ | ----------- | --------------------------------------- | ---------------- |
| 香港四区 | Gold 6133 @2.5Ghz * 4 | 4GiB | 30GB SSD | 30Mbps | 无限 | v4(广播ip)*1 | 60rmb/月|

**测试CIDR**: 154.40.45.0/24


## 无聊的测试数据
线路:
| 运营商 | 去程 | 回程 |
| ------ | --- | ---- | 
| 电信 | 接入CN2的NTT | 163 |
| 联通 | AS9929 | AS4837 |
| 移动 | NTT+CMI | CMI |

### 测速
```bash
ID    网络服务提供商       测速服务器位置   上传/Mbps   下载/Mbps   延迟/ms
59386 中国电信             中国浙江杭州   　↑ 29.04     ↓ 30.35     71.45   
17145 中国电信５Ｇ         中国安徽合肥   　↑ 28.43     ↓ 28.54     73.74   
5396  中国电信５Ｇ         中国江苏苏州   　↑ 28.07     ↓ 30.42     65.15   
45170 中国联通             中国江苏无锡   　↑ 28.51     ↓ 29.15     96.96   
35527 中国广电             中国四川成都   　↑ 28.66     ↓ 28.01     128.95  
```


## 网络波动图
![小雨云香港4区网络波动图](/img/2024/rainyun-hk4/Daily-network.webp "网络波动图")

## 性能测试
```bash
Geekbench 5 测试结果

系统信息
  Operating System              Debian GNU/Linux 12 (bookworm)
  Kernel                        Linux 6.1.0-10-amd64 x86_64
  Model                         QEMU Standard PC (i440FX + PIIX, 1996)
  Motherboard                   N/A
  BIOS                          SeaBIOS rel-1.16.3-0-ga6ed6b701f0a-prebuilt.qemu.org

处理器信息
  Name                          Intel(R) Xeon(R) Gold 6133 CPU @ 2.50GHz
  Topology                      1 Processor, 4 Cores
  Identifier                    GenuineIntel Family 6 Model 85 Stepping 4
  Base Frequency                2.49 GHz
  L1 Instruction Cache          32.0 KB x 4
  L1 Data Cache                 32.0 KB x 4
  L2 Cache                      4.00 MB x 4
  L3 Cache                      16.0 MB

内存信息
  Size                          3.82 GB

单核测试分数：584
多核测试分数：2200
详细结果链接：https://browser.geekbench.com/v5/cpu/22637138
可供参考链接：https://browser.geekbench.com/search?k=v5_cpu&q=Intel%20Xeon%20Gold%206133
```