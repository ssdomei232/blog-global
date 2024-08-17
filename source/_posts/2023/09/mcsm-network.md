---
title: 部分地区由于网络问题无法安装mcsm面板的解决方案
hide: true
tags: 
- linux
- minecraft
categories: 
- Linux
index_img: /img/2023/9/9/mcsminstall/index.webp
banner_img: /img/2023/9/9/mcsminstall/index.webp
permalink: /2023/09/09/202309091908/index.html
date: 2023-09-09 19:08:29
---

```
以下方案已作废
# 懒狗方案 
用我改好的脚本：
为了节省成本，不再提供脚本，请自行修改

脚本放在阿里云南京oss上
如果你认为我会在脚本里放其它的东西，可以打开脚本自己看一眼，我将node.js换成了清华大学开源软件镜像站的链接,并将mcsm安装文件放在123云盘上(123够良心，4块钱100G流量)
```

## 自己动手 
可以自己动手改脚本
1.访问mcsm文档 [运行在Linux - MCSManager 帮助文档 (imlazy.ink)](https://mcsm.imlazy.ink/#in-linux.html)
拿到官方脚本：https://gitee.com/mcsmanager/script/raw/master/setup.sh
2.看到脚本第5行的
`mcsmanager_donwload_addr="https://github.com/MCSManager/MCSManager/releases/latest/download/mcsmanager_linux_release.tar.gz"`
将里面GitHub的链接换成你的，用什么是你的事，能下载就行
**不要手贱去给http加上s**
除非你用的不是Let's Encrypt这类的证书
### 更快一点 
上面你自己改的脚本已经可以使用了，如果你想更快一点：
看到脚本第60行的
`wget https://nodejs.org/dist/"$node"/node-"$node"-linux-"$arch".tar.gz`
不要乱动，换成以下
`wget http://mirrors.tuna.tsinghua.edu.cn/nodejs-release/"$node"/node-"$node"-linux-"$arch".tar.gz`
这里使用了清华大学开源软件镜像站，速度很快
**不要手贱去给http加上s**