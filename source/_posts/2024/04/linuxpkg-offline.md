---
title: Linux创建简易的离线apt仓库
date: 2024-4-1 21:23:24
tags:
- linux
- shell
- 学习笔记
categories:
- Linux
index_img: /img/2024/4/linuxpkg-offline/00020-3477423043.webp
banner_img: /img/2024/4/linuxpkg-offline/00020-3477423043.webp
permalink: /2024/03/17/linuxpkg-offline/index.html
---
### 制作
```bash
## 查看当前软件包
ls /var/cache/apt/archives/

#此路径下如果软件包较多可以运行下面命令进行删除,非必要项，按需删除（方便后面制作离线源）
rm -rf /var/cache/apt/archives/*

## 下载软件与相关依赖包
apt-get -d install <pkg-name> && apt-get -d install <pkg-name> $(apt-cache depends <pkg-name> | grep Depends | cut -d: -f2)

## 创建目录并添加权限
mkdir -p /opt/pkgs/
touch /opt/pkgs/Packages.gz
chmod 777 -R /opt/pkgs

## 拷贝软件包到
cp -r /var/cache/apt/archives/* /opt/pkgs/

## 安装dpkg-dev
apt-get install dpkg-dev

## 生成软件包索引
cd /opt/pkgs && dpkg-scanpackages -m . > Packages
```

### 使用

#### 本地使用
```bash
## 备份源文件
mv /etc/apt/sources.list /etc/apt/sources.list.bak
## 使用
echo "deb [trusted=yes] file:///opt/pkgs ./" >> /etc/apt/sources.list
```

#### 网络使用
```bash
## 备份源文件
mv /etc/apt/sources.list /etc/apt/sources.list.bak
## 使用
echo "deb [trusted=yes] http(s)://example.com/pkgs ./" >> /etc/apt/sources.list
```


### 参考资料
[Linux基础-制作本地apt仓库（离线安装软件）](https://blog.csdn.net/Passerby_Wang/article/details/123600746)
[如何创建一个简单 APT 仓库 ](https://www.cnblogs.com/bamanzi/p/create-simple-apt-repo.html)