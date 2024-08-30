---
title: 在 Linux 中使用 Wireguard 客户端
tags:
- 学习笔记
- linux
- wireguard
categories: 
- Linux
index_img: /img/2024/wireguard-cli-linux/main.png
banner_img: /img/2024/wireguard-cli-linux/banner.png
permalink: /articles/2024/wireguard-cli-linux/index.html
date: 2024-08-30 16:44:40
---

1. 安装 wireguard-tools
```bash
sudo apt update
sudo apt install wireguard-tools resolvconf
```
2. 编辑隧道文件
隧道文件放在 `/etc/wireguard/` 下       
例如 `/etc/wireguard/wg0.conf`      
3. 启动隧道
```bash
sudo wg-quick up <隧道名>
```
4. 停止隧道
```bash
sudo wg-quick down <隧道名>
```

隧道名就是 `.conf` 文件的名称

## 参考资料
[如何在 Ubuntu 22.04 上安装 Wireguard VPN](https://cn.linux-console.net/?p=29550)