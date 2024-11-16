---
title: 搭建自己的openai api高速反向代理
tags: 
- AI
- proxy
categories: 
- AI
index_img: /img/2024/1/25/openai.jpg
banner_img: /img/2024/1/25/openai.jpg
permalink: /2024/01/25/202401250927/index.html
date: 2024-01-25 09:27:45
---
在去年(2023年),我看到了极客湾的这个视频:[我们做了个能对话的AI派蒙，免费给大家玩!](https://b23.tv/Ap27xLS)
觉得很有意思,但是由于没有显卡且不敢翻墙,一直没有机会尝试,但最近搞来了一块RTX A2000(目前这卡性价比很低,不推荐),便想着折腾一下
由于不敢翻墙，只能使用反向代理的方式来访问openai api
## 准备
你需要:
* 一个Cloudflare账户
* Cloudflare账户中有未被墙的有效域名(若有下一项,则为可选项)
* 一台高速的非中国大陆服务器(配置不用太高,可选)(若无此项,则上一项为必选)
* 一个好用的脑子

## Cloudflare worker
创建一个Cloudflare worker，并把一下代码塞入其中(代码来自[这里](https://gitee.com/GoGPTAI/ChatGPT-Proxy))

```
const TELEGRAPH_URL = 'https://api.openai.com';

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url);
  url.host = TELEGRAPH_URL.replace(/^https?:\/\//, '');

  const modifiedRequest = new Request(url.toString(), {
    headers: request.headers,
    method: request.method,
    body: request.body,
    redirect: 'follow'
  });

  const response = await fetch(modifiedRequest);
  const modifiedResponse = new Response(response.body, response);

  // 添加允许跨域访问的响应头
  modifiedResponse.headers.set('Access-Control-Allow-Origin', '*');

  return modifiedResponse;
}
```
使用Cloudflare理论上可以降低被封的概率
由于workers.dev被墙了,所以需要在“触发器”中换用你的域名(如果有非中国大陆服务器则可以跳过这一步)
如果你没有非中国大陆服务器,那么这篇文章就结束了

## 反向代理加速
众所周知,cloudflare在中国大陆的访问速度极慢,所以可以使用自己的服务器套一层加速
我这里使用一台香港CN2GIA线路的服务器和nginx做演示
(或许你可以去导航栏的推广页看看,那里获取会有这种服务器,如果那个页面在你看到的时候还在)
```nginx
location ^~ / {
    proxy_pass https://xxx.xxx.workers.dev; 
    proxy_set_header Host xxx.xxx.workers.dev; 
    proxy_set_header X-Real-IP $remote_addr; 
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
    proxy_set_header REMOTE-HOST $remote_addr; 
    proxy_set_header Upgrade $http_upgrade; 
    proxy_set_header Connection "upgrade"; 
    proxy_set_header X-Forwarded-Proto $scheme; 
    proxy_http_version 1.1; 
    add_header X-Cache $upstream_cache_status; 
    add_header Strict-Transport-Security "max-age=31536000"; 
    add_header Cache-Control no-cache; 
}
```
使用面板创建的反向代理是这样的,但是你会发现这是访问显示502
这是因为Nginx在建立SSL/TLS连接时没有发送服务名到后端服务器，导致导致后端服务器使用错误的证书或拒绝连接，所以需要做以下修改:
```nginx
location ^~ / {
    proxy_pass https://xxx.xxx.workers.dev; 
    proxy_set_header Host xxx.xxx.workers.dev; 
    proxy_set_header X-Real-IP $remote_addr; 
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
    proxy_set_header REMOTE-HOST $remote_addr; 
    proxy_set_header Upgrade $http_upgrade; 
    proxy_set_header Connection "upgrade"; 
    proxy_set_header X-Forwarded-Proto $scheme; 
    proxy_http_version 1.1; 
    proxy_ssl_server_name on;   # 使Nginx在建立SSL/TLS连接时发送服务名到后端服务器
    proxy_ssl_protocols TLSv1 TLSv1.1 TLSv1.2;  # 指定Nginx应该使用的SSL/TLS协议版本
    add_header X-Cache $upstream_cache_status; 
    add_header Strict-Transport-Security "max-age=31536000"; 
    add_header Cache-Control no-cache; 
}
```

添加了以下两行配置

```
proxy_ssl_server_name on;   # 使Nginx在建立SSL/TLS连接时发送服务名到后端服务器
proxy_ssl_protocols TLSv1 TLSv1.1 TLSv1.2;  # 指定Nginx应该使用的SSL/TLS协议版本
```
访问`://YOURHOSTNAME/v1/chat/completions`
若出现以下回复就配置成功了
```json
{
    "error": {
        "message": "You didn't provide an API key. You need to provide your API key in an Authorization header using Bearer auth (i.e. Authorization: Bearer YOUR_KEY), or as the password field (with blank username) if you're accessing the API from your browser and are prompted for a username and password. You can obtain an API key from https://platform.openai.com/account/api-keys.",
        "type": "invalid_request_error",
        "param": null,
        "code": null
    }
}
```

### 参考文章
[最新宝塔反代openai官方API开发接口详细搭建教程，解决502 Bad Gateway问题](https://blog.csdn.net/weixin_43227851/article/details/134404942)
[ChatGPT-Proxy](https://gitee.com/GoGPTAI/ChatGPT-Proxy)