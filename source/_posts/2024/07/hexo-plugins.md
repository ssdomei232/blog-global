---
title: Hexo 常用插件
tags:
- 工具
- 分享
categories: 
- 工具
index_img: /img/2024/hexo-plugins/hexo.webp
banner_img: /img/2024/hexo-plugins/hexo.webp
permalink: /articles/2024/hexo-plugins/index.html
date: 2024-07-03 09:46:47
---

### hexo-generator-feed -- RSS 订阅 
**安装**:   
```shell
npm install hexo-generator-feed --save
```
**使用**:       
在`_config.yml`中添加:
```yaml
#订阅RSS
feed:
  type: atom
  path: atom.xml
  limit: false
```
或
```yaml
feed:
  type: rss2
  path: rss.xml
  limit: false
```

配置含义：  
* `type`: RSS的类型(atom/rss2)
* `path`: 文件路径，默认是 atom.xml/rss2.xml
* `limit`: 展示文章的数量,使用 0 或则 false 代表展示全部
* `hub`: URL of the PubSubHubbub hubs (如果使用不到可以为空)
* `content`: （可选）设置 true 可以在 RSS 文件中包含文章全部内容，默认：false
* `content_limit`: （可选）摘要中使用的帖子内容的默认长度。 仅在内容设置为false且未显示自定义帖子描述时才使用。
* `content_limit_delim`: （可选）如果content_limit用于缩短post内容，则仅在此分隔符的最后一次出现时进行剪切，然后才达到字符限制。默认不使用。
* `icon`: （可选）自定义订阅图标，默认设置为主配置中指定的图标。
* `order_by`: 订阅内容的顺序。 (默认: -date)

### hexo-generator-sitemap -- sitemap
**安装**: 
```shell
npm install hexo-generator-sitemap --save
```
**使用**:       
在`_config.yml`中添加:
```yaml
menu:
  home: / || home
  #about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
```

### hexo-deployer-git
详见 [推送Hexo至自建gitea仓库中 - mei.lv](https://mei.lv/articles/2024/hexo-git/)