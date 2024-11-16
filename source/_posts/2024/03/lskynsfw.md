---
title: lsky图床使用nsfw鉴黄
tags:
- linux
- 学习笔记
categories: 
- 学习笔记
index_img: /img/2024/3/17/nsfw.png
banner_img: /img/2024/3/17/nsfw.png
permalink: /2024/03/17/lskynsfw/index.html
date: 2024-03-17 21:12:51
---
~~闲的无聊弄了一个图床:`https://tc.linuxcat.top/`~~     
使用开源的lsky pro搭建      
为了防止坏比搞逝,阿里和腾讯的鉴黄太贵,就用了nsfwapi鉴黄

### docker
docker一键安装
```shell
docker run -p 3000:3000 ghcr.io/arnidan/nsfw-api:latest
```
如果你机器在国内,拉不动镜像:
```shell
docker run -p 3000:3000 registry.cn-hangzhou.aliyuncs.com/mei232/roywangdev-nsfwapi:latest
```
### nodejs
不推荐使用nodejs直接部署
使用nodejs安装比较麻烦,需要到`https://roy.wang/nsfw-appraisal-api/`选择合适的版本下载(大概2022年之前的提交)
然后参照说明文档下载模型,接着
```shell
yarn
yarn build
yarn start
```
这个过程可能有亿点久,arm架构不支持

然后把把`http(s)://IP:port/classify`填入即可,设置一个合适的阈值测试一下就好了

### API调用
```shell
curl -X POST -H "Content-Type: multipart/form-data" -F "image=@path/to/image" http(s)://IP:port/classify
```

### ~~公开API~~
~~你也可以用我的API`https://api.mmeiblog.cn/nsfw/`~~        
~~直接填进去就行,不用加`/classify`~~        
~~目前API已经寄了,三年内没有加回来的打算~~

### 参考资料
[NSFW-API 开源的图片鉴黄API](https://roy.wang/nsfw-appraisal-api/)
[nsfw-api](https://github.com/arnidan/nsfw-api/tree/41c0acb725dced11c5536ebbc6a67153bfed3100)
[nsfw_model](https://github.com/GantMan/nsfw_model)
[图片审核 Lsky Pro](https://docs.lsky.pro/docs/free/v2/group/picture-review.html)
