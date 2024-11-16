---
title: 介绍部分 Minecraft 服务端并提供下载，推荐一些插件
tags: 
- minecraft
categories: 
- Minecraft
index_img: /img/2023/9/29/00013-3883135775.webp
banner_img: /img/2023/9/29/00013-3883135775.webp
permalink: /2023/09/29/202309291221/index.html
date: 2023-09-29 12:21:22
---

## 核心介绍
由于此前的文章存在过多的问题，在重构后相关的内容已经被挪到了一个独立的项目里：[Minecraft Severs List ](https://d.mmeiblog.cn/) ，同时这个项目也集成了 [Linux 一键开服功能](https://d.mmeiblog.cn/mcs-quick.php)          
如果你有什么好点子或者新的服务端,欢迎在 [Github](https://github.com/ssdomei232/Start-the-minecraft-server-automatically) 发起 Issue         
如果你发现了任何错误，欢迎进行反馈，但请带上足够的证明，仅凭三言两语甚至一句话根本无从查证      
截至目前共整理了 54 款核心,列表如下:
* Airplane(插件)
* Akarin(插件)
* Arclight(混合)
* Banner(混合)
* BungeeCord(群组)
* Bedrock Server(基岩)
* Catserver(混合)
* CraftBukkit(插件)
* CubeRite(插件)
* Cauldron(混合)
* DragonProxy(代理)
* Folia(插件)
* Forge(模组)
* Fabric(模组)
* Floodgate(代理)
* GlowStone(插件)
* Geyser(代理)
* Hose(插件)
* HexaCord(群组)
* Leaves(插件)
* lightfall(群组)
* LightfallClient(群组)
* LightingLuminol(插件) 
* Luminol(插件)
* Mirai(插件)
* Mohist(混合)
* Nukkit(基岩)
* NukkitX(基岩)
* Nemisys(群组)
* NeoForge(模组)
* PowerNukkitX(基岩)
* Paper(插件)
* PocketMine(基岩)
* Pufferfish(插件)
* Pufferfish+(插件)
* Pufferfish+Purpur(插件)
* Purformance(插件)
* Purpur(插件)
* Patina(插件)
* Petal(插件)
* Spigot(插件)
* SpongeForge(混合)
* SpongeVanilla(插件)
* Sugarcane(插件)
* Sakura(插件)
* Thermos(混合)
* Travertine(代理)
* Tuinity(插件)
* Uranium(混合)
* Vanilla(原版)
* Velocity(群组)
* Waterfall(群组)
* yatopia(插件)
* Youer(混合)

## 关于插件兼容性
Spigot 是基于 Bukkit 的一个分支，由 CraftBukkit 的原作者之一开发。      
Paper 是另一个基于 Spigot 的分支。Paper 的目标是进一步提升服务器性能，并添加一些额外的功能和优化选项。      
也就是说兼容关系大致如下：      
Paper **理论上**兼容所有插件, Spigot 兼容 Bukkit 插件 , Bukkit 不完全兼容 Spigot 插件,至于到底兼容什么，**请在 [Minecraft 插件百科](https://mineplugin.org/)上查询**      

## 关于插件
这里提供几个开服常用的插件

### CoreProtect
CoreProtect - 快速，高效的方块记录，回滚和恢复
CoreProtect是一种快速，高效的数据记录和防止恶意破坏的工具。可以回滚和恢复破坏。为大型服务器设计，CoreProtect将记录和管理数据，而不会影响服务器性能。
CoreProtect是最常用的服务器保护的插件，并自2012年年初得到了大力发展。
了解更多:
[CoreProtect - Minecraft插件百科 (](https://mineplugin.org/CoreProtect)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/CoreProtect)
### EssentialsX
EssentialsX 是一个基于 Spigot 服务端的基础插件，为从大到小的服务器提供核心功能。这些功能包括：
玩家可以自由设置家 服务器传送或给玩家提供物品套组，可以设置跨世界或单独世界。 玩家与玩家间的私有消息，传送，发送传送请求 玩家自定义昵称 很多的管理员工具包括踢出服务器，临时禁止登陆服务器、禁言与监禁 内建经济系统，包括木牌商店、付费执行命令和完全的 Vault 支持 此外，EssentialsX 的选择模块提供了更多综合的功能如聊天、世界保护、GeoIP查找还有更多
了解更多:
[EssentialsX - Minecraft插件百科 (](https://mineplugin.org/EssentialsX)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/EssentialsX)
### BlockLocker
该插件允许您仅使用标志即可保护箱子、门、炉子、分配器、滴管、料斗和许多其他块。贴上标志后，只有标志上列出的人才能访问容器。它不使用数据库，所有信息都存储在附加到受保护块的标志上。因此，如果您使用 WorldEdit 移动宝箱，宝箱仍将受到保护。
[瞒块锁 |SpigotMC - 高性能我的世界](https://www.spigotmc.org/resources/blocklocker.3268/)
### AuthMe
AuthMe Reloaded可以防止在未登录的情况下放置方块、移动、使用其他命令，或者查看当前的在线玩家数。只有输入正确的密码才能正常登陆。特别是防止被盗号，自动通过UUID更新ID。登陆失败可能是你没有在指定时间内登陆。
每个命令和每个设置都可以用极其简单的配置文件来启用或者禁用。如果你不喜欢英语，或者不喜欢作者的翻译，你也可以轻松的自主编辑语言环境！
[Authme - Minecraft插件百科 (](https://mineplugin.org/Authme)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/Authme)
### CMILib
一个支持库，我也不知道是哪个的。
### Vault
Vault 插件是一个关于权限、聊天以及经济插件的前置插件，他能让这些插件快速地与Vault插件挂钩而不需要依赖于其他个别插件。多数关于注册和权限的前置插件配置过于繁琐且缺乏大部分功能，于是这个插件便诞生了。Vault插件可以通过更加直观明了的方式解决这些问题，并为这些插件提供他们可能所需要的支持与依赖服务。
[Vault - Minecraft插件百科 (](https://mineplugin.org/Vault)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/Vault)
### Residence
Residence是大多数服务器都会使用的插件，它不同于其他保护类插件，它可以让玩家自己保护自己的家园，无需再麻烦管理员。新版的Residence更是增添了许多新特性，为服主减轻了不少负担。
[Residence - Minecraft插件百科 (](https://mineplugin.org/Residence)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/Residence)
### LuckPerms
LuckPerm是一款先进、高等的权限插件，仅仅以快速、稳定可靠、灵活多变的特点，
便可以替代现有的许多权限插件，例如PermissionsEX、GroupManagerX、z/bPermissions、BungeePerms等主流权限插件。
LuckPerms这个插件的计划，本来是围绕着两个主要特点来制作的：高性能、强大且广泛的功能，
填补其他同类插件的功能缺陷、并且建立在同类现有功能上更进一步的优化功能。
LuckPerms还包括了非常广泛的API支持，这是为开发人员的添加的，
并且，luckperms还兼容各式各类Minecraft服务器软件&支持多种数据存储的选择。
[LuckPerms - Minecraft插件百科 (](https://mineplugin.org/LuckPerms)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/LuckPerms)
### QuickShop
QuickShop是一个商店插件, 不需要使用命令, 玩家可以直接用箱子来售卖物品, 也可以简单的输入要购买的数量。 实际上, 玩家不需要掌握任何的命令, 就可以使用这个插件了。
这个插件需要安装前置Vault插件
[QuickShop - Minecraft插件百科 (](https://mineplugin.org/QuickShop)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/QuickShop)
### SkinsRestorer
SkinsRestorer是一个插件，用于恢复离线模式服务器和网络的皮肤，使玩家能够通过键入单个命令来更改皮肤。
[皮肤修复剂 |SpigotMC - 高性能我的世界](https://www.spigotmc.org/resources/skinsrestorer.2124/)
### ViaVersion
ViaVersion旨在允许新版本的客户端进入旧版本的服务器，支持CraftBukkit/Spigot/Paper/Sponge/BungeeCord/Velocity服务端核心，支持到最新游戏版本。
搭配ViaBackwards和ViaRewind甚至可以向下兼容，允许旧版本的客户端进入新版本的服务器。
ViaBackwards和ViaRewind都需要ViaVersion作为前置插件。
[ViaVersion - Minecraft插件百科 (](https://mineplugin.org/ViaVersion)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/ViaVersion)
### worldedit
我的世界地图编辑器...在游戏中运行！
具有选择、原理图、复制和粘贴、画笔和脚本。
在创意中使用它，或在生存中暂时使用它。
需要 Java 版本。
与基于 Bukkit 的平台（Spigot 和 Paper）兼容。
[WorldEdit/命令 - Minecraft插件百科 (](https://mineplugin.org/WorldEdit/%E5%91%BD%E4%BB%A4)[mineplugin.org](http://mineplugin.org/)[)](https://mineplugin.org/WorldEdit/%E5%91%BD%E4%BB%A4)
### EasyWhitelist
白名单插件
白名单用法：（控制台中无需输入斜杠）
1.在游戏或控制台中执行“/easywl add <玩家名>”添加白名单
2.在游戏或控制台中执行“/easywl remove <玩家名>”删除白名单
3.在游戏或控制台中执行“/easywl list”查看白名单列表
4.在游戏或控制台中执行“/easywl on”开启白名单
5.在游戏或控制台中执行“/easywl off”关闭白名单
6.在游戏或控制台中执行“/easywl reload”重新加载
