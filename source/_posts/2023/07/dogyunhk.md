---
title: 狗云(dogyun)香港BGP线路经典云使用体验(hk.cld.s)
tags: 
- VPS使用体验
- dogyun
categories: 
- VPS使用体验
index_img: /img/2023/7/26/dogyunhk/1.png
banner_img: /img/2023/7/26/dogyunhk/1.png
permalink: /2023/07/26/202307262221/index.html
date: 2023-07-26 22:21:21
---
2024.2.21更新
配置如下:

| 机房   | cpu                   | 内存 | 硬盘            | 宽带   | 流量      | 价格            |
| -------| ----------------------| -----| ---------------| -------| ---------| ----------------|
| 香港cld | E5-2696v3 2.30GHz * 1 | 1GiB | 20GiBSSD-raid10 | 50Mbps | 300GiB/月 | 25/月    250/年 |

脚本测试结果:

![1.png](/img/2023/7/26/dogyunhk/1.png)
![2.png](/img/2023/7/26/dogyunhk/2.png)

从测速结果看，宽带达到标称甚至部分超过

itdog延迟测试

![3.png](/img/2023/7/26/dogyunhk/3.png)
![4.png](/img/2023/7/26/dogyunhk/4.png)

经测试,此台机器去程及回程线路如下:
| 运营商 | 去程 | 回程 |
| ------ | --- | ---- | 
| 电信 | CN2 GIA | AS4837(169骨干网) |
| 联通 | AS4837(169骨干网) | AS4837(169骨干网) |
| 移动 | CMI | CMI |

电信去程会走CN2GIA是令我意想不到的,毕竟这玩意便宜宽带还大,但在多次对比后确实排除了CN2GT和CTGNet的可能