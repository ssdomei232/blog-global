---
title: 推送Hexo至自建gitea仓库中
tags:
- 学习笔记
- linux
categories: 
- 学习笔记
index_img: /img/2024/hexo-git/enter-seeting.png
banner_img: /img/2024/hexo-git/enter-seeting.png
permalink: /articles/2024/hexo-git/index.html
date: 2024-06-21 16:04:22
---

## Gitea 配置

### 创建仓库
首先创建一个仓库，例如`blog-web`    
### 配置SSH
进入命令行，执行`ssh-keygen -t ed25519 -C "你的 Gitea 邮箱"`    
然后一路按 Enter ，完成后进入`C:\Users\ 用户名 \.ssh`目录   
打开`ed25519.pub`并复制内容  
点击Gitea界面的`设置`   
![进入设置](/img/2024/hexo-git/enter-seeting.png)
添加一个SSH密钥     
![添加SSH密钥](/img/2024/hexo-git/seeting.png)
将先前获得的`ed25519.pub`中的内容填入`密钥内容`中，点击`增加密钥`    

## Hexo配置
先cd到Hexo的目录，然后`npm install hexo-deployer-git --save`

然后修改`_config.yml`，移动到最下方，添加
```yaml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repository: <你的仓库地址> # example: https://example.net/user/repo.git
  branch: main
```
保存后`hexo d`测试一下  



## 参考资料
[One-Command Deployment](https://hexo.io/docs/one-command-deployment)
[Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

