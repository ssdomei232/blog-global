---
title: FileCodeBox（文件快递柜）S3配置
tags: 
- linux
- 开源
categories: 
- Linux
index_img: /img/2023/10/17/bt/3.png
banner_img: /img/2023/10/17/bt/3.png
permalink: /2023/10/17/202310172109/index.html
date: 2023-10-17 21:09:39
---
(本来这是一篇使用宝塔部署的教程，但是有了Docker和1Panel，bt那坨玩意那啥都不用)
文件快递柜是一个开源项目，[开源地址](https://github.com/vastsa/FileCodeBox)
> *匿名口令分享文本，文件，像拿快递一样取文件*

作者演示地址：[文件快递柜-FileCodeBox](https://share.lanol.cn/#/)

~~我搭的：[meiのshare](https://share.linuxcat.top/#/)~~

# 安装配置

Docker一键部署
`docker run -d --restart=always -p 12345:12345 -v /opt/FileCodeBox/:/app/data --name filecodebox lanol/filecodebox:beta`
**也可以在1Panel一键部署**

V2.0的默认管理地址为 `/#/admin` 默认密码为 `FileCodeBox2023`

进入后台后**记得修改**

## S3配置

这里使用的是[雨云](https://www.rainyun.com/cat_?s=blog)的ROS，用它是因为当时正在免费公测。

如下图填写

**注意：API端点前要加“ `https://`” ，末尾不能加“ `/`”**

![3.png](/img/2023/10/17/bt/3.png)
保存后上传一个文件测试一下，如果不行请检查配置并重启一遍尝试

## 配置修改

如果有端口冲突，请找到根目录下的 `/data/.env2`

参照以下注释进行修改(作者提供)

```
# 端口
PORT=12345
# Sqlite数据库文件
DATABASE_URL=sqlite+aiosqlite:///database.db
# 静态文件夹
DATA_ROOT=./static
# 静态文件夹URL
STATIC_URL=/static
# 开启上传
ENABLE_UPLOAD=True
# 错误次数
ERROR_COUNT=5
# 错误限制分钟数
ERROR_MINUTE=10
# 上传次数
UPLOAD_COUNT=60
# 上传限制分钟数
UPLOAD_MINUTE=1
# 删除过期文件的间隔（分钟）
DELETE_EXPIRE_FILES_INTERVAL=10
# 管理地址
ADMIN_ADDRESS=admin
# 管理密码
ADMIN_PASSWORD=admin
# 文件大小限制，默认10MB
FILE_SIZE_LIMIT=10
# 网站标题
TITLE=文件快递柜
# 网站描述
DESCRIPTION=FileCodeBox，文件快递柜，口令传送箱，匿名口令分享文本，文件，图片，视频，音频，压缩包等文件
# 网站关键词
KEYWORDS=FileCodeBox，文件快递柜，口令传送箱，匿名口令分享文本，文件，图片，视频，音频，压缩包等文件
# 存储引擎
STORAGE_ENGINE=filesystem
# 如果使用阿里云OSS服务的话需要额外创建如下参数：
# 阿里云账号AccessKey
KeyId=阿里云账号AccessKey
# 阿里云账号AccessKeySecret
KeySecret=阿里云账号AccessKeySecret
# 阿里云OSS Bucket的地域节点
OSS_ENDPOINT=阿里云OSS Bucket的地域节点
# 阿里云OSS Bucket的BucketName
BUCKET_NAME=阿里云OSS Bucket的BucketName
```

# 反向代理
## 1Panel面板

直接创建网站时在已装应用中选择就好了

## 宝塔面板
在此推荐使用1Panel，开源免费无bug，而且好用
bt那坨那啥都不用
### 创建网站

在宝塔面板的网站-PHP项目-添加站点

PHP版本选择为纯静态

![4.png](/img/2023/10/17/bt/4.png)
点击“提交”

### 添加反向代理

进入网站设置-反向代理-创建反向代理

![5.png](/img/2023/10/17/bt/5.png)
然后添加解析就好了
