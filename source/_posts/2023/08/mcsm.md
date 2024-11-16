---
title: 使用mcsm面板搭建我的世界服务器
tags: 
- 雨云
- mc服务器
categories: 
- Linux
index_img: /img/2023/8/19/mcsm/8.webp
banner_img: /img/2023/8/19/mcsm/8.webp
permalink: /2023/08/19/202308191605/index.html
date: 2023-08-19 16:05:12
---
**由于MCSM10的更新,本教程已经过期**
# 视频教程

~~更加详细，适合极度小白人士。~~

ps:不敢说话

<iframe src="https://player.bilibili.com/player.html?bvid=BV1dh4y1T7p9&amp;page=1" width="100%" height="300px" frameborder="0" allowfullscreen="true" framespacing="0"></iframe>

# 使用雨云游戏云面板服

使用mcsm面板搭建我的世界服务器其实非常简单，只需要跟着教程执行命令就好了，但如果您认为自己没有这种能力，这里有一个简单的办法：(有能力的直接跳过这一部分)

在雨云购买游戏云面板服，最低只要0.9元一天，还有雨云的按天计费以及独家动态计费，不开服不收费，闲时省钱，非常适合学生的需求，甚至还可以免费领取面板服(但需要抢，手慢无，蹲点抢就行)。

## 购买

为了防止部分人连购买都不会，这里也写上教程

注册我就不说了，如果你连注册都不会就划走吧，直接花钱找人给你搭建。

注册完成后点击官网右上角的“进入控制台”

![1.png](/img/2023/8/19/mcsm/1.png)
接着如图操作：
![2.png](/img/2023/8/19/mcsm/2.png)
![3.png](/img/2023/8/19/mcsm/3.png)
![4.png](/img/2023/8/19/mcsm/4.png)
## 加入游戏

在控制台进入mcsm管理面板开启服务器，控制台会给你连接地址，填入我的世界“多人游戏”的游戏地址(点击添加游戏后从上往下数第二个框框)中即可。
![5.png](/img/2023/8/19/mcsm/5.png)
![6.png](/img/2023/8/19/mcsm/6.png)
![7.png](/img/2023/8/19/mcsm/7.png)
## 注意

我认为上述教程完全没有必要，雨云的操作已经足够简便了，如果你需要上述教程的话我还是建议你尽早放弃，因为一旦出现问题你根本就无法解决。

了解更多可以去雨云百科：[最新雨云百科/游戏云 VPS话题 - 雨云论坛 (](https://forum.rainyun.com/c/wiki/rgskvm/17)[rainyun.com](https://rainyun.com/)[)](https://forum.rainyun.com/c/wiki/rgskvm/17)
# linux服务器

服务器可以购买云服务器，也可以使用内网穿透，云服务器推荐雨云游戏云，按天计费以及独家动态计费

## 连接服务器

如果是云服务器会给ssh连接地址机账密，本地服务器就是自己设置的账密

ssh工具可以用：[SSH工具_Aechoterm (](https://ec.nantian.com.cn/#/home)[nantian.com.cn](http://nantian.com.cn/)[)](https://ec.nantian.com.cn/#/home)

个人感觉很好用，当然你也可以在cmd用ssh命令连接

## 安装java

首先检查你以前是否安装了java，如果不是你想要的版本，请卸载它。
```
java -version
```
安装jdk，这里使用清华大学开源软件镜像站，默认屏蔽海外ip。国外用户可以选择Adoptium

这里以jdk17 x64为例。jdk文件下载地址右键需要的版本复制链接即可.
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
## 安装mcsm面板

这里仅展示一键安装命令，如果需要手动安装请去mcsm面板文档：[首页 - MCSManager 帮助文档 (](https://mcsm.imlazy.ink/)[imlazy.ink](http://imlazy.ink/)[)](https://mcsm.imlazy.ink/)
```
# 安装完成后使用 systemctl start mcsm-{web, daemon} 即可启动
wget -qO- https://gitee.com/mcsmanager/script/raw/master/setup.sh | bash
```
面板需要23333和24444端口，请提前开放防火墙和安全组

访问：https;//服务器的ip地址:23333

使用nat模式需要映射端口：

访问：http://你的服务器ip地址:映射后的23333端口

## 创建服务器

### 使用“一键开服”

如果使用一键开服就不用准备服务端

点击左侧导航栏的快速开始--一键开服，选择想用的服务端

### 普通流程

这里可以选择java版或基岩版，这里以java版为例，需要自行准备服务端，直接去bing上搜就行，其它版本流程一致

1.点击面板左侧导航栏应用实例--创建实例(右上角)--java版--上传单个服务端软件--填写基本信息后上传服务端，我准备了几个，可以去文章最下方下载。

![8.webp](/img/2023/8/19/mcsm/8.webp)
2.上传完后点击编辑实例具体参数，什么都不要动，点要下角的控制台

3.进入控制台后点击开启实例，这里以mogist1.18.2做示例。

4.mohist会询问是否同意eula，但有些服务端不会，需要点击服务端配置文件--eula.txt--将eula改为”是“

5.如果你没有正版且要开离线服务器，需要在配置文件中浏览 [**server.properties**](http://server.properties/)  找到  online-mode在线（正版）验证“选项并改为否。

![9.webp](/img/2023/8/19/mcsm/9.webp)

## 添加mod/插件

首先要确认你使用的服务端是否支持你想要添加的mod/插件，一般你下载mod的地方都会注明支持什么。

mod放在文件管理--mods文件夹中

插件放在文件管理--plugins文件夹中

### 注意

我的世界java版服务端分为原版，mod服，插件服，混合服，插件服仅支持插件，mod服至支持mod，混合服支持插件和mod。

但具体是否支持你想要添加的mod请自行查看服务端的官网，例如forgr服务端仅支持forge mod。

# 其它系统

其它系统的安装方式自己去读mcsm的文档，我就不抄下来了，安装完成后的操作都是基本相同的。[首页 - MCSManager 帮助文档 (](https://mcsm.imlazy.ink/)[imlazy.ink](http://imlazy.ink/)[)](https://mcsm.imlazy.ink/)

# 内网穿透

我选择使用樱花frp，他们的文档十分详细，这里就不写了，其它内网穿透软件也是基本通用的。[我的世界(Minecraft) 局域网联机穿透指南 | SakuraFrp 帮助文档 (](https://doc.natfrp.com/app/mc.html)[natfrp.com](http://natfrp.com/)[)](https://doc.natfrp.com/app/mc.html)

# 服务端下载
[Index of / - mc服务端下载站 (mmeiblog.cn)](https://d.mmeiblog.cn/)