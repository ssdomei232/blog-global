---
title: 一些自建加速/镜像服务
hide: true
date: 2024-03-10 15:32:57
tags:
- linux
- proxy
categories:
- Internet
index_img: /img/2024/3/10/index.webp
banner_img: /img/2024/3/10/index.webp
permalink: /2024/03/10/Accelerated-services/index.html
---
由于某知名防火墙的原因,许多网站都无法访问,还有许多网站的访问十分魔幻。  
在这里放一些我自建的反代服务   
使用这些服务需要搭配一张根证书,点击[这里](https://static.mmeiblog.cn/files/ssl/home.cer)下载   
目前已有的服务:
* Github
* Pixiv
* Hugggingface
* jsdelivr

## 使用方法

### Github
安装根证书后修改hosts文件
windows在`C:\Windows\System32\drivers\etc`下   
Linux在`/etc`下
```
# MFW-Github
45.153.130.227 api.github.com
45.153.130.227 gist.github.com
45.153.130.227 raw.github.com
45.153.130.227 raw.githubusercontent.com
45.153.130.227 camo.githubusercontent.com
45.153.130.227 cloud.githubusercontent.com
45.153.130.227 avatars.githubusercontent.com
45.153.130.227 avatars0.githubusercontent.com
45.153.130.227 avatars1.githubusercontent.com
45.153.130.227 avatars2.githubusercontent.com
45.153.130.227 avatars3.githubusercontent.com
45.153.130.227 user-images.githubusercontent.com
45.153.130.227 objects.githubusercontent.com
45.153.130.227 private-user-images.githubusercontent.com
45.153.130.227 github.com
45.153.130.227 pages.github.com
45.153.130.227 githubapp.com
# MFW-Github-end
```

### Pixiv
GFW不会拦截Pixiv的http流量,因此使用http来做数据传输,在内网自行反代https(当然我的服务不是这样实现的)  
下面提供的数据传输域名可以选择开启https来加密,也可以直接用http来加速,但都需要本地反代为原来的域名
数据传输域名(年抛域名,到期后记得来换):
| 数据传输域名 | 对应原来域名 |
| ----------- | ----------- |
| pximg-proxy.aps.icu | i.pximg.net |
| pixiv-accounts-proxy.aps.icu | accounts.pixiv.net |
| pixix-proxy.aps.icu | www.pixiv.net |

### Huggingface
与Pixiv类似,下面提供的数据传输域名可以选择开启https来加密,也可以直接用http来加速,但都需要本地反代为原来的域名
数据传输域名(年抛域名,到期后记得来换):
| 数据传输域名 | 对应原来域名 |
| ----------- | ----------- |
| hug.aps.icu | huggingface.co |
| hug-cdn.aps.icu | cdn-lfs-us-1.huggingface.co |

### jsdelivr
安装根证书后修改hosts文件
windows在`C:\Windows\System32\drivers\etc`下   
Linux在`/etc`下
```
# MFW-jsdelivr
45.153.130.227 cdn.jsdelivr.net
# MFW-jsdelivr-end
```



**我不会收集任何流过反代服务器的流量,我没有偷看别人隐私的垃圾爱好**
后续也许还会有更多加速