---
title: 雨云香港三区线路测试&&使用体验
tags:
- VPS使用体验
categories: 
- VPS使用体验
index_img: /img/2024/3/18/index.webp
banner_img: /img/2024/3/18/index.webp
permalink: /2024/03/18/rainyunhk3/index.html
date: 2024-03-18 08:22:45
---
雨云在2024年3月17日22:30分左右突然上架了香港三区服务器(这上的也太不是时候了,我都上床睡觉了2333333)   
由于上的太晚了,所以没有第一时间买到机器,不过也根据群友提供的测试信息在[雨云论坛](https://forum.rainyun.com/t/topic/7246)做了粗略的总结   
于是我在第二天上午试用了一台高配版来测试以下(感冒在家,结果班主任开的网课直播还没声233333)   

### 配置信息
*CPU均为EPYC7702,带宽均为上下对等,硬盘免费30G,可自己加,带宽单位为Mbps,雨云一般会有折扣,上网搜个优惠码就行,一般会给到8折,当然本网站不会出现推广信息,如果你想要靠谱的折扣,可以看CSDN@mei232*
| 套餐名称 | CPU | 内存 | 硬盘 | 带宽 | 价格 | 折后价格(八折) |
| ------- | ---- | --- | ----- | ---- | ----- | ----- |
| KVM 入门版 | 1c | 1G | 30G | 3M | 30/月 152/年 | 24/月 121.6/年 |
| KVM 标配版 | 2c | 2G | 30G | 5M | 38/月 319.2/年 | 30.4/月 255.2/年 |
| KVM 中配版 | 2c | 4G | 30G | 8M | 53/月 445.2/年 | 42.4/月 356.2/年 |
| KVM 高配版 | 4c | 4G | 30G | 10M | 69/月 579.6/年 | 55.2/月 463.7/年 |
| KVM 顶配版 | 4c | 8G | 30G | 15M | 133/月 1117.2/年 | 106.4/月 893.8/年 |
| KVM 高配版 | 8c | 16G | 30G | 20M | 192/月 1654.8/年 | 153.6/月 1323.84/年 |

### 性能
```bash
----------------------CPU测试--通过sysbench测试-------------------------
 -> CPU 测试中 (Fast Mode, 1-Pass @ 5sec)
 1 线程测试(单核)得分: 		1638 Scores
 4 线程测试(多核)得分: 		6481 Scores
---------------------内存测试--感谢lemonbench开源-----------------------
 -> 内存测试 Test (Fast Mode, 1-Pass @ 5sec)
 单线程读测试:		44397.12 MB/s
 单线程写测试:		19463.69 MB/s
------------------磁盘dd读写测试--感谢lemonbench开源--------------------
 -> 磁盘IO测试中 (4K Block/1M Block, Direct Mode)
 测试操作		写速度					读速度
 100MB-4K Block		63.2 MB/s (15.42 IOPS, 1.66s)		69.8 MB/s (17049 IOPS, 1.50s)
 1GB-1M Block		1.0 GB/s (995 IOPS, 1.01s)		7.9 GB/s (7496 IOPS, 0.13s)
---------------------磁盘fio读写测试--感谢yabs开源----------------------
Block Size | 4k            (IOPS) | 64k           (IOPS)
  ------   | ---            ----  | ----           ---- 
Read       | 160.95 MB/s  (40.2k) | 1.40 GB/s    (21.8k)
Write      | 161.38 MB/s  (40.3k) | 1.40 GB/s    (21.9k)
Total      | 322.34 MB/s  (80.5k) | 2.80 GB/s    (43.8k)
           |                      |                     
Block Size | 512k          (IOPS) | 1m            (IOPS)
  ------   | ---            ----  | ----           ---- 
Read       | 1.50 GB/s     (2.9k) | 1.54 GB/s     (1.5k)
Write      | 1.58 GB/s     (3.1k) | 1.64 GB/s     (1.6k)
Total      | 3.09 GB/s     (6.0k) | 3.19 GB/s     (3.1k)
```
测试结果:https://paste.spiritlhl.net/code/H1H6Et.txt
### 网络
**IP不是原生香港IP,是从美国广播过来的**
先说总结:线路非常好,但是带宽太小,性价比不高,但是雨云限速不限流,如果出一些限流的大带宽机器应该会好不少,如200G+20M或200G+15M   
这条线在中国和亚太地区体验很好,但是出海不行,勉强能当作国内to海外mc/其他游戏加速

#### 线路
国内:
|运营商 | 去程 | 回程|
|--- | --- | ---|
|电信 | CTGNet(CN2GIA)* | CTGNet(CN2GIA)* |
|联通 | AS4837(169骨干网) | AS4837(169骨干网) |
|移动 | CMI | CMI |


国际(无法准确测试,国际线路辨别很困难,这个测试主要是有些人用来加速游戏给海外客户看的):
|国家 | 去程(服务器去海外) |速度 |延迟|
|--- | --- | --- | --- | 
|韩国CN2 | CTGNet(CN2GIA)* | 挺快的 | 60-70ms |
|荷兰CUII | 无法辨别 | 很慢 | 200-300ms |
|德国CUII | 无法辨别 | 很慢 | 200-300ms |
|日本IIJ | NTT | 较快 | 50-70ms |
|日本软银 | 无法辨别(大概率是NTT) | 较快 | 50-70ms |
|美国CN2 | 无法辨别 | 较快 | 130-140ms |
#### 测速
我买的这台是10M上下对等带宽
国内:
```bash
ID    网络服务提供商       测速服务器位置   上传/Mbps   下载/Mbps   延迟/ms
59386 中国电信             中国浙江杭州   　↑ 9.59      ↓ 9.88      36.46   
17145 中国电信５Ｇ         中国安徽合肥   　↑ 9.47      ↓ 9.54      35.97   
5396  中国电信５Ｇ         中国江苏苏州   　↑ 9.59      ↓ 9.54      41.09   
54432 中国联通             中国海南三亚   　↑ 9.55      ↓ 9.35      25.99   
35527 中国广电             中国四川成都   　↑ 9.51      ↓ 9.52      43.65   
```
欧洲:
```bash
ID    网络服务提供商       测速服务器位置   上传/Mbps   下载/Mbps   延迟/ms
34948 Swish Fibre          英国伦敦     　　↑ 9.23      ↓ 9.72      202.34  
30981 KPI-Telecom          乌克兰基辅   　　↑ 9.74      ↓ 10.35     283.08  
21615 JMDI Sp. z o.o.      波兰华沙     　　↑ 9.55      ↓ 10.54     270.29  
1434  CPN Fibra            意大利米兰   　　↑ 10.26     ↓ 9.97      186.59  
12919 Telenor Norge AS     挪威奥斯陆   　　↑ 9.67      ↓ 10.05     232.29  
37211 Avatel Telecom       西班牙马德里   　↑ 9.81      ↓ 10.39     197.41  
37193 CITIC Telecom CPC    爱沙尼亚塔林   　↑ 9.53      ↓ 10.16     276.08  
24481 CityTelecom.ru       俄罗斯莫斯科   　↑ 10.16     ↓ 10.67     187.82  
38092 Three Ireland        爱尔兰都柏林   　↑ 9.38      ↓ 9.85      268.96  
44477 TELE AG              德国法兰克福   　↑ 10.10     ↓ 9.79      212.95  
15152 fonira Telekom       奥地利维也纳   　↑ 10.01     ↓ 9.57      203.41  
48096 ONI Telecom          葡萄牙里斯本   　↑ 9.91      ↓ 9.61      207.16 
```
美洲:
```bash
ID    网络服务提供商       测速服务器位置   上传/Mbps   下载/Mbps   延迟/ms
46790 Bell Canada          加拿大魁北克   　↑ 9.29      ↓ 9.95      245.81  
16781 TELUS Mobility       加拿大温哥华   　↑ 10.18     ↓ 9.76      163.08  
50932 Tusass A/S            格林兰努克   　　↑ 9.26      ↓ 9.96      270.47  
11777 KPU Telecom          美国阿拉斯加   　↑ 10.42     ↓ 10.05     197.45  
22144 H&B Communications   美国堪萨斯   　　↑ 9.86      ↓ 9.70      191.95  
13098 Pilot Fiber          美国纽约     　　↑ 9.40      ↓ 10.02     208.57  
44477 AT&T México          墨西哥墨西哥城   ↑ 10.23     ↓ 9.99      213.47  
31195 PoP-RJ/RNP        阿根廷里约热内卢↑ 9.61      ↓ 9.98      336.88 
```
中东:
```bash
ID    网络服务提供商       测速服务器位置   上传/Mbps   下载/Mbps   延迟/ms
17336 ETISALAT-UAE         阿联酋       　　↑ 2.38      ↓ 9.57      107.57  
52872 Deltanet             巴基斯坦     　　↑ 9.51      ↓ 9.55      136.50  
43365 TurkNet              土耳其       　　↑ 9.98      ↓ 10.15     311.24  
37151 Kazakhtelecom        哈萨克斯坦   　　↑ 9.55      ↓ 10.95     358.70  
16051 Saudi Telecom        沙特阿拉伯   　　↑ 9.51      ↓ 9.90      263.98  
15570 Yemen Net            也门         　　↑ 9.63      ↓ 10.97     273.96  
42379 SatLink Pvt          马尔代夫     　　↑ 9.50      ↓ 9.78      83.46  
```
亚太:
```bash
ID    网络服务提供商       测速服务器位置   上传/Mbps   下载/Mbps   延迟/ms
32155 China Mobile         中国香港     　　↑ 4.86      ↓ 1.18      2.92    
13623 Singtel              新加坡       　　↑ 9.59      ↓ 9.64      37.82   
12492 Telstra              澳大利亚     　　↑ 9.70      ↓ 10.55     122.61  
41663 Sky Broadband        新西兰       　　↑ 10.08     ↓ 9.82      174.10  
3756  Globe Telecom        菲律宾       　　↑ 10.41     ↓ 10.00     149.82  
30131 Telekom Malaysia     马来西亚     　　↑ 9.50      ↓ 9.87      60.56   
1370  Telekomunikasi       印度尼西亚   　　↑ 9.50      ↓ 9.55      62.62   
36978 AIS Fibre            泰国         　　↑ 9.58      ↓ 9.63      61.84   
45357 Asia Pacific Telecom 中国台湾     　　↑ 9.52      ↓ 9.55      15.92  
```
#### 流媒体解锁
**雨云禁止搭建VPN服务,同时有着极为敏感的VPN流量检测系统,请不要在雨云搭建VPN**
```bash
---------------------流媒体解锁--感谢sjlleo开源-------------------------
以下测试的解锁地区是准确的，但是不是完整解锁的判断可能有误，这方面仅作参考使用
----------------Youtube----------------
[IPv4]
连接方式: Youtube Video Server
视频缓存节点地域: 美国  洛杉机(LAX17S56)
Youtube识别地域: 香港(HK)
----------------Netflix----------------
[IPv4]
您的出口IP完整解锁Netflix，支持非自制剧的观看
NF所识别的IP地域信息：香港
[IPv6]
您的网络可能没有正常配置IPv6，或者没有IPv6网络接入
---------------DisneyPlus---------------
[IPv4]
当前IPv4出口解锁DisneyPlus
区域：香港区
解锁Youtube，Netflix，DisneyPlus上面和下面进行比较，不同之处自行判断
----------------流媒体解锁--感谢RegionRestrictionCheck开源--------------
 以下为IPV4网络测试，若无IPV4网络则无输出
============[ Multination ]============
 Dazn:					Yes (Region: US)
 HotStar:				No
 Disney+:				Yes (Region: US)
 Netflix:				Yes (Region: HK)
 YouTube Premium:			Yes (Region: HK)
 Amazon Prime Video:			Yes (Region: US)
 TVBAnywhere+:				Yes
 iQyi Oversea Region:			US
 Viu.com:				No
 YouTube CDN:				Los Angeles, CA 
 Netflix Preferred CDN:			Hong Kong  
 Spotify Registration:			No
 Steam Currency:			USD
 ChatGPT:				Yes
 Bing Region:				US
 Instagram Licensed Audio:		->
 Instagram Licensed Audio:		No
=======================================
```

### 总结
雨云香港三区线路非常号,但是带宽太小   
如果出一些限流的大带宽机器应该会好不少,如200G+20M或200G+15M(对与这个线路15M算挺大的了,同类产品有1c1g+250G+15M 35/月的)   
### 注释
* 关于CTGNet:
> 由于通过CTG/CTA/CTE购买GIA带宽需要中国电信集团级别审批合约，因此CTG自己搞了个CTGNet（自卖自销系列），与过去直接和AS4809接入的CN2 GIA对比， 除了中间多出来CTGNet的2-3跳左右路由以外，和之前CN2 GIA的路由看起来没多少差别了。但是CTGNet网内偶尔 会出现莫名其妙的延迟增加情况，体现在香港地区CTGNet网内两跳路由之间延迟增加15-20ms，这个问题属于偶发。
* 之前雨云香港三区是用的阿里云线路,后来好像换了(没开卖之前放出的测试IP)

### 参考资料
[中国三大电信运营商国际网络互联相关资料](https://blog.sunflyer.cn/archives/594)
[VPS常用脚本合集（持续更新）](https://www.zzzi.org/article/shell-jiaoben)
[VPS | 大数据最佳实践](https://bigdata.icu/tools/vps.html#_0x03-%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%B5%8B%E8%AF%95%E8%84%9A%E6%9C%AC)