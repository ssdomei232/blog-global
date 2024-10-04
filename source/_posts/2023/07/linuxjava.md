---
title: linux安装jdk（java）教程
tags: 
- java
- linux
categories: 
- Linux
index_img: /img/2023/7/1/00011-1003087495.webp
banner_img: /img/2023/7/1/00011-1003087495.webp
permalink: /2023/07/01/202307012105/index.html
date: 2023-07-01 21:05:01
---

首先，为了省事，先切换root用户，如果你对Linux命令熟悉，也可以不用。

```
#设置root用户密码，如果你知道就不用设，输入你想设置的密码，密码不可见。
sudo passwd root
#切换root用户
su root
```

首先检查你以前是否安装了java，如果不是你想要的版本，请卸载它。

```
java -version
```

安装jdk，这里使用清华大学开源软件镜像站，默认屏蔽海外ip。国外用户可以选择Adoptium
这里以jdk17 x64为例。自行右键复制你需要的下载地址

```
# 创建安装目录
mkdir /usr/local/java/
# 下载JDK安装包，将地址替换成要安装的版本的下载地址
wget https://mirrors.tuna.tsinghua.edu.cn/Adoptium/17/jdk/x64/linux/OpenJDK17U-jdk_x64_linux_hotspot_17.0.6_10.tar.gz

# 解压当前目录下的JDK压缩文件到安装目录，将下面压缩包名字替换成你下载的
tar -zxvf OpenJDK17U-jdk_x64_linux_hotspot_17.0.6_10.tar.gz -C /usr/local/java/

# 进入/usr/local/java/目录
cd /usr/local/java/

# 列出目录内的文件夹，查看jdk名称，这里是 jdk-17.0.6+10
ls

# 设置环境变量(安装 nano 输入 apt -y install nano)
nano /etc/profile

# 在末尾添加对应变量，将下面的jdk-17.0.6+10改成你上面查到的JDK文件名
# 移动到末尾
# 输入下面这几串内容后，按Ctrl+O来保存，然后按一下回车确定，接着按Ctrl+X退出。
export JAVA_HOME=/usr/local/java/jdk-17.0.6+10
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

# 应用修改后的环境变量
source /etc/profile

# 软链接程序到环境变量中，将下面的jdk-17.0.6+10改成上面查到的JDK文件名
ln -sf /usr/local/java/jdk-17.0.6+10/bin/java /usr/bin/java

# 测试是否安装正常，显示类似于 openjdk version "17.0.6" 2023-01-17 则为正常
java -version

```

