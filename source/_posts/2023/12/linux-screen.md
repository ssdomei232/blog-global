---
title: Linux使用screen
tags: 
- shell
- linux
categories: 
- Linux
index_img: /img/2023/12/6/00015-1315254036.webp
banner_img: /img/2023/12/6/00015-1315254036.webp
permalink: /2023/12/06/202312061055/index.html
date: 2023-12-06 10:55:44
---
## screen 是啥
简单地说就是linux系统的让应用后台运行

## 安装

```
# CentOS
yum install screen
# Debian/Ubuntu
apt install screen
# 检查安装
screen -v
```
## 使用

### 常用命令
```
# 帮助
screen -help
# 查看已有的screen列表
screen -ls
```
### 创建终端
一般有两种常用的方式创建一个新的session
```
# 使用 -S 创建(把Name替换成你想使用的名称即可)
screen -S [Name]
# 使用 -R 创建(把Name替换成你想使用的名称即可)
screen -R [Name]
```
**区别**:
使用`-R`创建时，如果之前有重名的session，则会直接进入之前的session
使用`-S`创建时如果以前有重名的session的话不会进入，而是会创建一个重名的session

### 退出并保存session
在你创建的session中按下`Ctrl+a+d`即可退出并保存(退回到主终端)

### 重新进入session
```
# 使用 -r 
screen -r [pid/Name]
```
当然你也可以用`-R`:
`screen -R [Name]`

### 删除session
当你不需要一个session，想要将其删除时
```
# 进入想要删除的终端
screen -r [Name]
# 输入exit来停止终端
exit
```
也可以在主终端中删除session
```
# 使用-R/-r/-S
screen -R [pid/Name] -X quit
```

## 高级命令
screen有一些高级命令，不过这里不介绍，想要了解可以自行搜索，因为一般用不到