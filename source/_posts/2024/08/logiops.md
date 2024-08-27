---
title: 在 Linux 中驱动罗技鼠标快捷键
tags:
- 学习笔记
- linux
- 罗技
- 鼠标
categories: 
- Linux
index_img: /img/2024/logiops/anjian.webp
banner_img: /img/2024/logiops/anjian.webp
permalink: /articles/2024/logiops/index.html
date: 2024-08-18 19:30:56
---
最近由于受够了 Windows 的种种陈年老 bug ,开始润去 Linux 
但是~~bug贼多~~非常好用的 Logi Options+ 并没有 Linux 版本,但幸运的是,有人开发出了一个第三方的驱动: [logiops](https://github.com/PixlOne/logiops)  
我使用的鼠标为 M720 ,我觉得还挺好用的,不过我更推荐 Master 系列,因为 M720 的质量不太好,我已经换了两个了(Master 系列的鼠标适合手大的人,但是 Master 鼠标左侧的两个快捷键感觉不那么好用,太小了,容易误触或者按不下去)

### 准备工作
1. 项目需要c++ 20 编译器，需要安装 cmake，libevdev，libudev，libconfig等。
```bash
# Debian/Ubuntu
sudo apt install build-essential cmake pkg-config libevdev-dev libudev-dev libconfig++-dev libglib2.0-dev

# Arch Linux
sudo pacman -S base-devel cmake libevdev libconfig systemd-libs glib2

# Fedora
sudo dnf install cmake libevdev-devel systemd-devel libconfig-devel gcc-c++ glib2-devel

# Gentoo Linux
sudo emerge dev-libs/libconfig dev-libs/libevdev dev-libs/glib dev-util/cmake virtual/libudev

# Solus
sudo eopkg install cmake libevdev-devel libconfig-devel libgudev-devel glib2-devel

# openSUSE
sudo zypper install cmake libevdev-devel systemd-devel libconfig-devel gcc-c++ libconfig++-devel libudev-devel glib2-devel
```

2. 克隆仓库
```bash
git clone https://github.com/PixlOne/logiops.git
```

### 编译安装
1. 构建
```bash
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make
```
2. 安装
```bash
sudo make install
```
3. 配置守护进程
```bash
sudo systemctl enable --now logid
```
4. tip: 出现问题时重启，这可以解决大部分问题
```bash
sudo service logid restart
```
### 配置文件
配置文件位于/etc/logid.cfg,自己创建一个`vim /etc/logid.cfg`     
此文件的语法解释参见: [语法解释](https://github.com/PixlOne/logiops/wiki/Configuration)         
配置中，每个鼠标按键通过一个cid表示，鼠标按键的cid值参见: [CIDs](https://github.com/PixlOne/logiops/wiki/CIDs)      
或是通过debug模式查看。
debug模式:
```bash
# 先停止服务
sudo service logid stop
# 然后
sudo logid -v
```
此时以应该能看见下列输出，如果看不见，可以尝试重新连接鼠标到电脑。这样就能知道你鼠标上有什么按键了。
```bash
[DEBUG] Ignoring virtual node on /dev/hidraw4
[DEBUG] Ignoring virtual node on /dev/hidraw3
[INFO] Detected receiver at /dev/hidraw0
[DEBUG] Unsupported device /dev/hidraw1 ignored
[DEBUG] Unsupported device /dev/hidraw2 ignored
[DEBUG] Unsupported device /dev/hidraw5 ignored
[INFO] Device found: M720 Triathlon Multi-Device Mouse on /dev/hidraw0:2
[DEBUG] /dev/hidraw0:2 remappable buttons:
[DEBUG] CID  | reprog? | fn key? | mouse key? | gesture support?
[DEBUG] 0x50 |         |         | YES        |
[DEBUG] 0x51 |         |         | YES        |
[DEBUG] 0x52 | YES     |         | YES        | YES
[DEBUG] 0x53 | YES     |         | YES        | YES
[DEBUG] 0x56 | YES     |         | YES        | YES
[DEBUG] 0x5b | YES     |         | YES        | YES
[DEBUG] 0x5d | YES     |         | YES        | YES
[DEBUG] 0xd0 | YES     |         | YES        | YES
[DEBUG] 0xd7 | YES     |         |            | YES
```
下面是我的配置文件,我用了两三年了,非常好用,如果你用的也是 M720 ,可以参考一下     
侧键一(前进按钮/Forward Button/0x56) | 侧键二(返回按钮/Back Button/0x53) | 手势按键(Switch Apps/0xd0) | 滚轮向左(Left Scroll/0x5b) | 滚轮向右(Right Scroll/0x5d)    
![按键示意图(有点脏,请见谅)](/img/2024/logiops/anjian.webp)
按键的定义参见: [linux/input-event-codes.h](https://github.com/torvalds/linux/blob/master/include/uapi/linux/input-event-codes.h)
```json
devices: (
{
    name: "M720 Triathlon Multi-Device Mouse";
    buttons: (
        {
            cid: 0x56;
            action =
            {
                type: "Keypress";
                keys: ["KEY_LEFTCTRL","KEY_C"];
            };
        },
        {
            cid: 0x53;
            action =
            {
                type: "Keypress";
                keys: ["KEY_LEFTCTRL","KEY_V"];
            };
        },
        {
            cid: 0x5b;
            action =
            {
                type: "Keypress";
                keys:["KEY_LEFTCTRL","KEY_LEFTALT","KEY_LEFT"];
            };
        },
        {
            cid: 0x5d;
            action =
            {
                type: "Keypress";
                keys:["KEY_LEFTCTRL","KEY_LEFTALT","KEY_RIGHT"];
            };
        },
        {
            cid: 0xd0;
            action =
            {
                type: "Gestures";
                gestures:(
                {
                    direction:"Up";
                    mode="OnInterval";
                    interval=75;
                    action=
                    {
                        type:"Keypress";
                        keys:["KEY_VOLUMEUP"];
                    }
                },
                {
                    direction:"Down";
                    mode="OnInterval";
                    interval=75;
                    action=
                    {
                        type:"Keypress";
                        keys:["KEY_VOLUMEDOWN"];
                    }
                },
                {
                    direction:"None";
                    mode="OnRelease";
                    action=
                    {
                        type:"Keypress";
                        keys:["KEY_LEFTCTRL","KEY_X"];
                    }
                }
                )
            };
        }
    );
    hiresscroll:
    {
        hires: true;
        invert: false;
        target: false;
    };
}
);
```
我的配置文件解释: 按侧键一复制,侧键而粘贴,手势按键剪切,手势按键向上音量加,手势按键向下音量减    
***注意***: **如果你使用的屏幕DPI非常高，不是分辨率，是DPI。启用了高分辨率滚轮会导致滚轮速度非常块，可以关闭调整回正常的速度**      
(Windows和Linux上统一的复制和粘贴的快捷键是Ctrl+Insert和Shift+Insert，这个快捷键不区分图形软件和命令行软件)     
tips: 
* insert(KEY_INSERT)
* 左shift(KEY_LEFTSHIFT)
* 左ctrl(KEY_LEFTCTRL)
* 左alt(KEY_LEFTALT)
* 左方向键(KEY_LEFT)
* 右方向键(KEY_RIGHT)
### 参考资料
[logiops，在 Linux下设置罗技鼠标的按键和手势](https://segmentfault.com/a/1190000039985213)      
[logiops](https://github.com/PixlOne/logiops)       
[linux/input-event-codes.h](https://github.com/torvalds/linux/blob/master/include/uapi/linux/input-event-codes.h)