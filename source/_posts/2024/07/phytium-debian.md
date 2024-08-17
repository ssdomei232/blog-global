---
title: 为 世恒TD120A2 主机安装 Debian 12 BookWorm
tags:
- 学习笔记
- linux
categories: 
- Linux
index_img: /img/2024/phytium-debian/debian.jpg
banner_img: /img/2024/phytium-debian/debian.jpg
permalink: /articles/2024/phytium-debian/index.html
date: 2024-07-24 11:05:10
---
最近可能会发现,我的`mmeiblog.cn`和`linuxcat.top`域名下的部分子域出现了维护或无法访问的提示,这是因为我本来打算给我的国产主机从千疮百孔且极不稳定的 银河麒麟V10 换到 Debian ,但是由于换到一半我跑到[西安](#)玩了10天,所以拖了好久.
出
## 观前提示
**如果连接显示器时出现长时间灰屏,请用适当力度拍打机箱以及显示器,并使劲把插在显卡上的 HDMI线 往里怼一怼**


## 1. 准备工作
1. 下载镜像
国内用户推荐在 [Index of /debian-cd/ | 清华大学开源软件镜像站](https://mirror.tuna.tsinghua.edu.cn/debian-cd/) 下载最新的 Debian 安装镜像,下载时选择 `iso-dvd`
2. 写入镜像
使用 rufus 等写盘工具制作启动 U盘 
3. 安装系统
开机后看到提示后按 F10 进入启动项选择,选择你的 启动U盘 ,等待亿会载入引导程序,接着按照引导来设置就好

## 2. 修复 EFI 启动时的瑕疵
安装 Debian 后，硬盘的 EFI 分区里文件夹 EFI/boot 里默认没有引导文件 bootaa64.efi 和 grubaa64.efi 。因为这是给可移动的介质准备的，比如 U盘 或 光盘 。        
这时需要进入 EFI系统 中按照可移动介质的方式引导硬盘里的 Debian.
1. 进入 EFI系统
重启后看到提示后按 F10 进入启动项选择,选择 EFI Shell ,进入后 1秒 内按 Esc键 进入 EFI Shell 
2. 复制 EFI 引导文件
复制  EFI/boot/debian 里的 shimaa64.efi 和 grubaa64.efi 到 EFI/boot。重命名 EFI/boot/shimaa64.efi 为 EFI/boot/bootaa64.efi。
```shell
cp EFI/debian/shimaa64.efi EFI/boot/bootaa64.efi #复制  EFI/boot/debian 里的 shimaa64.efi 到 EFI/boot ,重命名为 EFI/boot/bootaa64.efi
cp EFI/debian/grubaa64.efi EFI/boot/grubaa64.efi #复制  EFI/boot/debian 里的 grubaa64.efi 到 EFI/boot
```

## 3. 将当前用户添加到 sudoer
1. 获取 /etc/sudoers 文件的写权限(需要切换到ROOT账户)
```bash
chmod u+w /etc/sudoers
```
2. 编辑配置文件
```bash
nano /etc/sudoers
```
3. 在 % sudo ALL = (ALL:ALL) ALL 这一行下边加入自己的用户名，比如 user。
```conf
% sudo ALL = (ALL:ALL) ALL
user ALL=(ALL:ALL) ALL
```
4. 保存退出。
5. 修改 /etc/sudoers 文件属性为只读。这时就可以使用 sudo 命令了。
```bash
chmod -w /etc/sudoers
```

## 4. 更换 银河麒麟 内核
Debian 的内核没有集成飞腾的网卡、声卡、exFAT…… 等驱动。因此非常有必要安装带驱动的内核，这里可以使用银河麒麟的内核。
**内核文件可以从安装光盘或安装的好本地操作系统中复制出来，也可以从软件仓库下载。**
软件仓库: [http://archive.kylinos.cn/kylin/KYLIN-ALL/pool/main/l/linux/](http://archive.kylinos.cn/kylin/KYLIN-ALL/pool/main/l/linux/)      
内核文件:       
* linux-image-5.4.18-85-generic_5.4.18-85.74_arm64.deb
* linux-headers-5.4.18-85_5.4.18-85.74_all.deb
* linux-headers-5.4.18-85-generic_5.4.18-85.74_arm64.deb
* linux-modules-5.4.18-85-generic_5.4.18-85.74_arm64.deb
* linux-modules-extra-5.4.18-85-generic_5.4.18-85.74_arm64.deb
内核固件仓库: [http://archive.kylinos.cn/kylin/KYLIN-ALL/pool/main/l/linux-firmware/](http://archive.kylinos.cn/kylin/KYLIN-ALL/pool/main/l/linux-firmware/)        
内核固件:
* linux-firmware_1.205kylin1_all.deb
安装新内核:
```bash
sudo dpkg -i linux*.deb
```
### GRUB-Customizer
1. 下载必要的依赖:
* [libssl3](https://packages.debian.org/zh-cn/bookworm/arm64/libssl3/download)
* [libhd21](https://packages.debian.org/zh-cn/bookworm/arm64/libhd21/download)
* [hwinfo](https://packages.debian.org/zh-cn/bookworm/arm64/hwinfo/download)
2. 下载 GRUB-Customizer 软件包: [https://packages.debian.org/zh-cn/bookworm/arm64/grub-customizer/download](https://packages.debian.org/zh-cn/bookworm/arm64/grub-customizer/download)
3. 安装依赖和 GRUB-Customizer
```bash
sudo dpkg -i linbssl3*.deb
sudo dpkg -i libhd21*.deb
sudo dpkg -i hwinfo*.deb
sudo dpkg -i grub*.deb
```
4. 启动 GRUB-Customizer
```bash
sudo grub-customizer
```
5. 切换标签到 “常规设置”，选择银河麒麟的内核（比如 5.4.18-85）为默认项。
6. 保存，退出.

## 5. GRUB 文件默认设置
1. 进入系统后，要编辑一个文件。    
```bash
nano /etc/default/grub
```
2. 在选项 GRUB_CMDLINE_LINUX_DEFAULT 中加入参数 `console=tty1`,这样就可以避免内核升级后将启动选项覆盖掉的问题了.       
```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet console=tty1"
```
3. 重新生成 grub.cfg 文件
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

## 参考资料
[UEFI 主板手动设置硬盘的引导启动](https://my.oschina.net/chipo/blog/10021751)       
[Debian 的安装（ARM64）](https://my.oschina.net/chipo/blog/5276817)