---
title: 小狗云香港活动CN2鸡使用体验
tags:
- VPS使用体验
categories: 
- VPS使用体验
index_img: /img/2024/xiaogoucloud-cn2cheap/Daily-network.webp
banner_img: /img/2024/xiaogoucloud-cn2cheap/Daily-network.webp
permalink: /articles/2024/xiaogoucloud-cn2cheap/index.html
date: 2024-06-28 15:30:47
---
昨天(6月27日)上午,在B站刷到一条视频,看到有人在卖6元的香港CN2机器,我当时就不相信,想着这货绝对超开了114514倍,所以赶紧买了一台试试水.

配置如下:

| 机房          | cpu                   | 内存  |       硬盘     | 宽带     |     流量   |         IP                               | 价格            |
| ------------ | ---------------------- | ---- | --------------- | ------ | ----------- | --------------------------------------- | ---------------- |
| 香港自营机房(也不知道到底是啥机房) | Gold 6133 @2.5Ghz * 2 | 1GiB | 30GBSSD系统盘+30GB数据盘 | 5Mbps | 无限 | v4(我买到的103段是原生IP)*1 | 6rmb/月(可能已涨价)|

**测试CIDR**: 103.112.96.0/24
## 挂载数据盘
默认数据盘没有给挂载,使用以下步骤挂载:
1. **确认磁盘被系统识别**
`sudo fdisk -l` 查找输出中显示的未被使用的磁盘设备，通常它会被标识为/dev/sdb、/dev/vdb或其他类似的名称。
2. **创建分区**
如果磁盘没有分区，需要使用fdisk或parted命令来创建一个新的分区。这里我们使用fdisk示例：
`sudo fdisk /dev/sdb`       
然后在fdisk提示符下输入：
```bash
n   # 创建一个新分区
p   # 创建主分区
1   # 分区编号
      # 接受默认的第一扇区位置
+30G # 分区大小为30GB
p   # 打印分区表以确认分区信息
w   # 写入分区表并退出
```
3. **格式化分区**
接下来，格式化新创建的分区。    
`sudo mkfs.ext4 /dev/sdb1`
4. **创建挂载点**
`sudo mkdir -p /data`
5. **挂载分区**
临时挂载分区以测试是否一切正常：    
`sudo mount /dev/sdb1 /data`    
检查挂载状态：      
`df -hT`
6. **永久挂载**
为了让分区在每次启动时自动挂载，需要编辑/etc/fstab文件：    
`vim /etc/fstab`    
在文件末尾添加以下行：  
```bash
/dev/sdb1 /data ext4 defaults 0 2 #自己看情况修改
```
保存并关闭文件
7. **重启系统**
`reboot`


## 无聊的测试数据

线路:
| 运营商 | 去程 | 回程 |
| ------ | --- | ---- | 
| 电信 | CN2 GT | AS4837 |
| 联通 | AS10099 | AS4837 |
| 移动 | CMI | CMI |

测速:
就5M的口子,测个毛线,肯定能跑满啊

## 网络波动图
![小狗云香港活动CN2鸡网络波动图](/img/2024/xiaogoucloud-cn2cheap/Daily-network.webp "网络波动图")
这款机子可能是被友商搞了,断断续续的挨打

## 性能/超开检测
目前的结果出乎我的意料,暂时还没有特别严重的超开
### CPU
1. 我在上午(这时人还很少)用Geekbench5测了一次,单核760       
链接: [https://browser.geekbench.com/v5/cpu/22622256](https://browser.geekbench.com/v5/cpu/22622256)     
2. 我在下午又来看了一眼,发现6元的配置售罄了,而且还涨价了,然后又测了一次,不过结果相差不大       
3. 我在第二天下午又看了一次,发现又补货了,最便宜的配置涨价到了8元/月,又测了一次,单核708,看起来有一点超开,但不太严重      
链接: [https://browser.geekbench.com/v5/cpu/22626428](https://browser.geekbench.com/v5/cpu/22626428)        
4. 第三天(6月29日)上午,我去看了一眼发现最便宜的配置又卖光了,就又测了一次,这次单核686,看起来已经存在超开了   
链接: [https://browser.geekbench.com/v5/cpu/22628737](https://browser.geekbench.com/v5/cpu/22628737)       
5. 7月8日下午,又测了一次,单核606,多核1084超开较为严重了       
链接: [https://browser.geekbench.com/v5/cpu/22662370](https://browser.geekbench.com/v5/cpu/22662370)
6. 7月25日下午,又双叒叕测了一次,单核418,多核675,超开爆了,卖的便宜就只能疯狂超开来回本                       
链接: [https://browser.geekbench.com/v5/cpu/22715081](https://browser.geekbench.com/v5/cpu/22715081)
### 内存
```
内存超售检测开始
====================
检查是否使用了 SWAP 超售内存
内存 IO 速度: 21 GB/s
内存 IO 速度正常
未使用 SWAP 超售内存
====================
检查是否使用了 气球驱动 Balloon 超售内存
存在 virtio_balloon 模块
可能使用了 气球驱动 Balloon 超售内存
====================
检查是否使用了 Kernel Samepage Merging (KSM) 超售内存
Kernel Samepage Merging 状态正常
未使用 Kernel Samepage Merging (KSM) 超售内存
====================
```
气球驱动那里不用太在意,我自己的KVM虚拟机都能检出