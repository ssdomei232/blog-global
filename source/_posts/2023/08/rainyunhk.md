---
title: 雨云香港云服务器使用体验
tags: 
- VPS使用体验
categories: 
- VPS使用体验
index_img: /img/2023/8/13/rainhk/1.png
banner_img: /img/2023/8/13/rainhk/1.png
permalink: /2023/08/13/202308132237/index.html
date: 2023-08-13 22:37:22
---
雨云香港云服务器顶配版测评

| cpu                  | 内存 | 带宽           | 硬盘                       | 价格                     |
| ---------------------- | ------ | ---------------- | ---------------------------- | -------------------------- |
| 4v Gold 6133 @2.5Ghz | 8GiB | 20Mbps上下同等 | 20GiB(可扩容)(0.38元/G/月) | 88元/月  1056/年(返利后) |

关于价格,雨云最近五周年,全场8折,年付7折。可以填我的优惠码:mei232

雨云香港云服务器的ip的属地有部分在美国,不过不影响正常使用,还可以用chatGPT api。

脚本测试结果:
```
----------------------------------------------------------------------------------
 CPU Model            : Intel(R) Xeon(R) Gold 6133 CPU @ 2.50GHz
 CPU Cores            : 4 Cores 2494.140 MHz x86_64
 CPU Cache            : L2 4096K & L3 16384K
 CPU Flags            : AES-NI Enabled & VM-x/AMD-V Enabled 
 OS                : CentOS 8 (64 Bit) KVM
 Kernel              : 4.18.0-448.el8.x86_64
 Total Space           : 5.8GB/20.0GB 
 Total RAM            : 985MB/7699MB(1000MB  Buff)
 Total SWAP            : 0MB/0MB
 Uptime              : 0day0hour8min
 Load Average           : 0.50,0.34,0.17
 TCP CC              : bbr+fq
 Organization           : AS63916 IPTELECOM Global
 Location             : Hong Kong / HK
 Region              : Central and Western
----------------------------------------------------------------------------------
 Unlock Test:
 Netflix         : Yes (Region: US)
 YouTube Premium     : No  (Region: US)
 BiliBili China     : Yes (Region: HongKong/Macau/Taiwan Only)
 TikTok          : Yes (Region: US)
 iQIYI International   : Yes (Region: US)
 ChatGPT         : Yes (Region: US)
----------------------------------------------------------------------------------
 I/O Speed(1.0GB)   : 948 MB/s
 I/O Speed(1.0GB)   : 1.2 GB/s
 I/O Speed(1.0GB)   : 1.5 GB/s
 Average I/O Speed  : 1237.6 MB/s
----------------------------------------------------------------------------------
 Geekbench v6 Test:
 Single Core : 592  
 Multi Core  : 1831
----------------------------------------------------------------------------------
 Node Name      Upload Speed      Download Speed      Latency     Packet Loss         
 Speedtest.net     16.42 Mbit/s      17.29 Mbit/s       (*)175.03ms   0.0%                
 Nanjing 5G  CT   16.72 Mbit/s      16.23 Mbit/s       84.00ms     0.0%                
 Wuhan     CT   16.01 Mbit/s      16.95 Mbit/s       205.11ms     Not available       
 Shanghai 5G  CU   16.67 Mbit/s      17.36 Mbit/s       145.56ms     0.0%                
 Wu Xi     CU   17.62 Mbit/s      17.59 Mbit/s       128.17ms     0.0%                
 Chengdu    CM   17.29 Mbit/s      17.80 Mbit/s       163.41ms     0.0%                
 Chengdu    BN   17.09 Mbit/s      17.52 Mbit/s       160.26ms     Not available       
----------------------------------------------------------------------------------
 Node Name       Upload Speed      Download Speed      Latency    Packet Loss         
 Hong Kong    CN  17.39 Mbit/s      17.11 Mbit/s       108.15ms   Not available       
 Macau       CN  17.04 Mbit/s      17.21 Mbit/s       94.99ms    0.0%                
 Taiwan      CN  16.55 Mbit/s      16.20 Mbit/s       90.75ms    0.5%                
 Singapore     SG  18.43 Mbit/s      16.77 Mbit/s       124.94ms   0.0%                
 Tokyo       JP  16.39 Mbit/s      16.72 Mbit/s       48.84ms    Not available       
 Los Angeles   US  17.14 Mbit/s      16.87 Mbit/s       194.13ms   0.0%                
 France      FR  17.13 Mbit/s      18.22 Mbit/s       278.01ms   0.0%                
----------------------------------------------------------------------------------

```

这延迟真离谱,绕路软银BGP

测速结果也是符合标称。geekbench6单核592，多核1831，从[geekbench官网](https://browser.geekbench.com/)数据看应属于略高于平均水平。

itdog全国ping测试:

![1.png](/img/2023/8/13/rainhk/1.png)
wordpress网站测速:

![2.png](/img/2023/8/13/rainhk/2.png)
![3.png](/img/2023/8/13/rainhk/3.png)
小型静态网站测速:
![4.png](/img/2023/8/13/rainhk/4.png)
![5.png](/img/2023/8/13/rainhk/5.png)
如果是用于建站这款服务器还是能用的,毕竟延迟比cloudflare低。有较高国内需求的业务还是不要用了。淋雨说以后会优化线路。
最后，买之前可以点试用先试试符不符合自己的需求，也不要买完就完结订单，毕竟这服务器还是挺贵的。
