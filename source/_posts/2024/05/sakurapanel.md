---
title: Sakura Panel 使用笔记
tags:
- FRP
- 学习笔记
categories: 
- 学习笔记
index_img: /img/2024/sakurapanel/banner.webp
banner_img: /img/2024/sakurapanel/banner.webp
permalink: /articles/2024/sakurapanel/index.html
date: 2024-05-02 7:25:33
---
Sakura Panel是由[@kasuganosoras](https://github.com/kasuganosoras)开发并开源的FRP内网穿透管理面板,支持商业化修改,后来卖给现在的SakuraFRP(但两者代码上实际没有关系,SakuraFRP重构了代码)    
开源地址: [Github](https://github.com/ZeroDream-CN/SakuraPanel)		
我搭建的demo:[LinuxcatFRP](https://frp.linuxcat.top/)

### 本地部署
首先克隆项目到本地`git clone https://github.com/ZeroDream-CN/SakuraPanel.git`,建议先Fork到自己的仓库，然后再clone到本地,因为用GitHub保存代码真的很让人放心.    
(n久之后来解释一下为什么有这句怪怪的话,因为写这篇文章的前一段时间我有一些写了很久的代码被误删了,最后在GitHub私有库上找到了那段代码前一段时间留的备份)		

#### 环境准备
Sakura Panel使用PHP开发,下面以1Panel和debian系统为示例:
首先`curl -sSL https://resource.fit2cloud.com/1panel/package/quick_start.sh -o quick_start.sh && bash quick_start.sh`安装1Panel    
然后在应用商店安装OpenResty和mysql   
![安装OpenResty](/img/2024/sakurapanel/install_openresty.webp "安装Openresty")   
![安装mysql](/img/2024/sakurapanel/install_mysql.webp "安装mysql")   
接着安装PHP(5.6以上应该都行)(选择默认扩展模板再加上`mysqli`)   
![安装PHP](/img/2024/sakurapanel/install_php.webp "安装PHP")   

### 部署代码
首先,进入`网站`导航下点击"创建网站",选择`运行环境`,类型选择`PHP`,接着在下拉菜单中找到之前安装的PHP,输入域名,点击"确认"稍等片刻,网站就创建完成了   
![创建网站](/img/2024/sakurapanel/create_website.webp "创建网站")   
创建好网站后,如下图所示,进入网站目录:   
![进入网站目录1](/img/2024/sakurapanel/enter_website_dir1.webp "进入网站目录1")   
![进入网站目录2](/img/2024/sakurapanel/enter_website_dir2.webp "进入网站目录2")   
接着添加一个远程下载来下载最新版代码`https://github.com/ZeroDream-CN/SakuraPanel/archive/refs/heads/master.zip`压缩包并解压(图中文件名可能不一样)   
![下载代码](/img/2024/sakurapanel/download_code.webp "下载代码")   
![解压代码](/img/2024/sakurapanel/unzip_code.webp "解压代码")   
将解压后代码移动到网站根目录:  
![移动代码](/img/2024/sakurapanel/move_code.webp "移动代码")   

### 创建数据库
先创建一个数据库:
![创建数据库](/img/2024/sakurapanel/create_db.webp "创建数据库")
前文中克隆的代码中有一个import.sql文件,里面有创建数据库和表,直接导入即可:   
![导入数据库](/img/2024/sakurapanel/import_db.webp "导入数据库")   

### 配置环境
切换到网站目录,编辑`configuration.php`(只展示数据库部分示例,其它自己按照注释设置):
```php
<?php
$_config = Array(
	
	/* 站点名称 */ 'sitename'      => 'Linuxcat FRP',
	// 会显示在标题等地方
	
	/* 站点简介 */ 'description'   => '内网穿透管理面板',
	// 会显示在大部分地方
	
	// 数据库相关配置
	/* 地址 */ 'db_host'           => '1Panel-mysql-<xxxx>', //这里填写"1Panel-mysql-<xxxx>"(以实际在连接信息界面获取到的为准)
	/* 端口 */ 'db_port'           => 3306,
	/* 账号 */ 'db_user'           => 'example',
	/* 密码 */ 'db_pass'           => 'example',
	/* 名称 */ 'db_name'           => 'example',
	/* 编码 */ 'db_code'           => 'utf8mb4',
```
接着配置`daemon.php`(看着上面填就行,剩下的代码不要动):
```php
<?php
$db = [
	/* 数据库地址 */ "host" => "1Panel-mysql-<xxxx>", //这里填写"1Panel-mysql-<xxxx>"(以实际在连接信息界面获取到的为准)
	/* 数据库账号 */ "user" => "example",
	/* 数据库密码 */ "pass" => "example",
	/* 数据库名字 */ "name" => "example",
	/* 数据库端口 */ "port" => 3306
];
```
接着来到`api/`目录下,配置`index.php`:
![切换目录](/img/2024/sakurapanel/dir_change.webp "切换目录")
```php
<?php
namespace SakuraPanel;

use SakuraPanel;

// API 密码，需要和 Frps.ini 里面设置的一样
define("API_TOKEN", "example"); //选一个你喜欢的密码填上
define("ROOT", realpath(__DIR__ . "/../"));

if(ROOT === false) {
	exit("Please place this file on /api/ folder");
}
```

### 管理员设置
先访问解析好的域名,注册一个账号(注册不了请检查smtp发件配置)    
然后返回1panel,安装PHPmyadmin   
![安装PHPmyadmin](/img/2024/sakurapanel/install_phpmyadmin.webp "安装PHPmyadmin")   
接着进入PHPmyadmin(连接地址以实际在连接信息界面获取到的为准):		
![进入PHPmyadmin](/img/2024/sakurapanel/enter_phpmyadmin.webp "进入PHPmyadmin")
根据上文的数据库密码,登录数据库:	
![登录数据库](/img/2024/sakurapanel/login_db.webp "登录数据库")		
接着找到`user`表,找到`admin`字段,将`guoup`字段改为`admin`:  	
![修改数据库1](/img/2024/sakurapanel/modify_db1.webp "修改数据库1")		
![修改数据库2](/img/2024/sakurapanel/modify_db2.webp "修改数据库2")		
然后点击`执行`就好了		


### 添加节点
访问管理面板,进入`节点管理`:
```
节点名称:起一个你喜欢的名字
节点简介:用一句简单的话来介绍这个节点
主机名称:填写你解析到节点IP的域名,如果没有直接填IP
IP 地址:服务器的 IP 地址，请不要输入域名
节点端口:节点的 Frps 服务器运行端口,与下文中frps.ini中"Frp 运行端口"一致
管理端口:Frps 管理 API 的端口，用于系统接口,与下文中frps.ini中"管理端口"一致
管理密码:填写一个密码,与下文中frps.ini中"管理密码"一致
Token:填写一个Token,与下文中frps.ini中"Frp Token 特权密码"一致
用户组:允许的用户组,如果你不打算给别人用就填"admin;"
```

### FRPS配置
Sakura Panel需要特殊的FRPS,访问作者的另一个项目[SakuraFrp](https://github.com/ZeroDream-CN/SakuraFrp)下载特制的FRPS		
`https://github.com/ZeroDream-CN/SakuraFrp/releases`		
下载后解压,编辑frps.ini文件,原本的注释都写得很全面,自己看着改就行,**注意`Api 密码`要与上文中`/api/index.php`中的一致**

### 启动FRPS
将frps和配置好的frps.ini上传到一个你喜欢的目录下,先不要动它,再次进入1Panel,进入`工具箱-进程守护`,按照指引安装软件	
#### 配置进程守护
在1Panel初始化Supervisor后,点击`创建守护进程`:		
下面以`/home/mei/frps`为运行目录为示例,启动命令填写`frps -c frps.ini`,启动用户选择`root`,填写完成后点击右下角的`确认`,稍等片刻,进程守护就创建完成了		
![创建守护进程](/img/2024/sakurapanel/create_daemon.webp "创建守护进程")
接着返回管理面板,到`流量统计`界面选择刚刚添加的节点,查看能否连接成功,连接成功后,就可以创建隧道正常使用了










