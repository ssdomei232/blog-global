---
title: 解决长亭雷池WAF tengine容器 无限重启的问题
tags: 
- linux
- Safeline WAF
- IPv6
categories: 
- 学习笔记
index_img: /img/2024/safeline-waf-tengine/CF752E194B1FF5AA96EC2CFD9A59C18B.webp
banner_img: /img/2024/safeline-waf-tengine/CF752E194B1FF5AA96EC2CFD9A59C18B.webp
permalink: /articles/2024/safeline-waf-tengine/index.html
date: 2024-10-07 10:00:55
---
最近在折腾虚拟机的时候,把安装了雷池WAF的虚拟机重启了一下,结果重启后发现套了雷池网站全部502了    
根据之前折腾 Harbor 的经验,这大概率是哪个容器启动不正常了,看了一下,果然,tengine容器在不断的重启,同样根据之前折腾 Harbor 的经验,这种情况手动把容器停止然后开启就行,如果不行就把所有的容器一起重启一下一般就好了,但是这次没有成功,做完后 tengine容器 还是在不断重启       
于是我去雷池文档里搜了一下,找到了一个[解决方案](https://docs.waf-ce.chaitin.cn/zh/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E6%8E%92%E6%9F%A5),下面是原文:

*问题表现：重启或升级后编辑任何站点配置都报错，后台 tengine 一直在重启。*    
*一般原因是 tengine 配置在当前设备环境上不合法，导致 tengine 无法以原配置启动，例如重启过程中网站端口被其他进程所占用、网站 dns 配置异常导致解析不到 IP 等。*     
*解决方案：可以通过查看 tengine 容器的日志，排查问题，也可以使用安装目录下的 reset_tengine.sh 脚本重置 tengine 容器配置。*        
```
# 执行时间根据网站数量和配置情况而定， 请耐心等待
cd /data/safeline && bash reset_tengine.sh
```
*执行成功后会有如下输出，此时可以尝试重新编辑站点配置，观察是否正常。*
```
[SafeLine] 是否重新生成 tengine 的所有配置 (Y/n)
重新生成 tengine 配置完成
```

### 老阴逼
然而按照官方文档的说明执行后并无卵用,等了好久都不见成功,于是去看了 tengine 容器的日志,发现了这一行:
```log
nginx: [emerg] invalid IPv6 address in resolver "[fe80::1%eth0]" in /etc/nginx/nginx.conf:132
```
里面有一个熟悉的东西`fe80::1%eth0`,安装雷池的时候就报过提醒,这种格式的 Nameserver 配置不合法,我也改了,不过雷池安装脚本也没有提醒这玩意重启之后会重置为默认值        
**解决方案**:    
1. 安装 `resolvconf`
```shell
sudo apt-get install resolvconf
```

1. 创建一个包含所需 DNS 服务器的头文件，例如：
```shell
sudo sh -c 'echo "nameserver 223.5.5.5" > /etc/resolvconf/resolv.conf.d/head'
sudo sh -c 'echo "nameserver 223.6.6.6" >> /etc/resolvconf/resolv.conf.d/head'
```

1. 更新 `/etc/resolv.conf`
```shell
sudo resolvconf -u
```

### 参考资料
[常见问题排查 | 雷池 SafeLine](https://docs.waf-ce.chaitin.cn/zh/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E6%8E%92%E6%9F%A5)