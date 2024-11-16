---
title: 各厂商CDN的CNAME域名及介绍
tags:
- 工具
- 分享
categories: 
- 工具
permalink: /articles/2024/cdn-cname/index.html
date: 2024-06-30 15:30:47
---
## 速查表格
如果你不想听我瞎叭叭,可以直接使用速查表格,如果你想了解一些详情,可以往下翻翻

| 厂商 | CNAME域名 | 地址 |
| --- | --- | --- |
| 白山云 | qingcdn.com </br> bsclink.cn </br> trpcdn.net | baishan.com |
| 网宿   | wsdvs.com </br> wsglb0.com </br> wscdns.com | wangsucloud.com |
| 蓝汛   | ccgslb.com.cn | edgenext.com |
| 帝联   | fastcdn.com | dnion.com |
| 阿里云 | kunlun*.com </br> cdngslb.com | aliyun.com |
| 腾讯云 | dnsv1.com </br> tc.cdntip.com </br> spcdntip.com | cloud.tencent.com |
| 百度云 | bdydns.com </br> jomodns.com | cloud.baidu.com | 
| 七牛云 | qiniudns.com | qiniu.com |
| 又拍云 | aicdn.com | upyun.com |
| 云端智度 | spdydns.com | isurecloud.net | 
| 网易云 | 163jiasu.com | sf.163.com |
| 360云 | 360cdn.cn </br> qihucdn.com | zyun.360.cn |
| 奇安信网战卫士 | qianxincdn.com | 
| 亚马逊云 | cloudfront.net |
| Microsoft Azure | mschcdn.com |
| verycdn | verycdn.net |
| 金山云 | ksyuncdn.com </br> ks-cdn1.com |
| 华为云 | cdnhwc2.com |
| 失控的防御系统/日出CDN | cnmnmsl.top | scdn.io |
| CNMCDN | svipcdn.cn | cnmcdn.cn |
| 星穹CDN | cname.fun | domecdn.com |
| 云科 | |waf.pro|
| 明赋云 | mingfucdn.com | mingfucloud.com |
| 括彩云 | kuocaidns.com | kuocaicdn.com |
| 京东云星盾 | cloud-scdn.com |
| 星域CDN | PCDN |
| 多吉云 | dogedns.com |
| Edge one | dnse2.com |
| 雨云 | raincdn.cn | rainyun.com |
| Cloudflare CN | cf-ns.com |
| LEDCDN | qiucname.tech | cdn.ledcdn.com |
| 尊云 |
| 亿速云 | kunlun*.com |
| 未来滴 | dnss.zip | pro.dnss.zip |
| 天翼云 | ctdns.cn | www.ctyun.cn |
| 知道创宇 | jiashule.com | www.yunaq.com |
| 方能CDN | fn01.vip | funnull.buzz |
| Greypanel | greycdn.net | greypanel.com |
| 优速盾 | dun.kim | cdnb.net |
| 飞旭云 | vip1.waf-idc-scdn.xyz | fxdun.cn |
| FreeCDN | freecdn.pw | freecdn.pw|
| 级级盾 | 1idc.cc | 7gd.cn |
| 速御安全 | tyudns.com | tyucdn.com |
| 语鹿云盾CDN | cdnv8.cn | lucdn.cn |

## 详情
商业机密 /doge
### 白山云
**介绍**    
www.gov.cn 用的就是白山云,不过白山云只为企业提供加速服务     
**域名列表**:       
* qingcdn.com
* bsclink.cn
* trpcdn.net

### 网宿
* wsdvs.com
* wsglb0.com
* wscdns.com

### 蓝汛
* ccgslb.com.cn

### 帝联
* fastcdn.com

### 阿里云
**介绍**        
一夜破产CDN,如果你的钱包特别充实,阿里云绝对是最好的选择,毕竟阿里云算得上是国内唯一正经做云的厂商了  
**域名列表**:           
阿里云的CNAME域名分为两类,一类是`kunlun*.com`,星号一般通配两位字母,专为国内提供加速服务        
另一类是`cdngslb.com`,提供全球加速服务  

### 腾讯云
**介绍**        
对于个人来说,小量使用腾讯云绝对称得上是物美价廉,不过也有破产风险    
**域名列表**:       
* dnsv1.com
* tc.cdntip.com
* spcdntip.com

### 百度云
**介绍**        
百度有正经做过什么产品吗?       
**域名列表**:       
* bdydns.com
* jomodns.com

### 七牛云
* qiniudns.com

### 又拍云
* aicdn.com

### 云端智度
* spdydns.com

### 网易云
**介绍**        
网易云还有这业务?   
**域名列表**:       
* 163jiasu.com

### 360云
**介绍**        
360和奇安信应该算分家了吧   
**域名列表**:       
* 360cdn.cn
* qihucdn.com

### 奇安信网战卫士
**介绍**        
良心厂商,极少的国内免费CDN,虽然节点有点少,申请有点麻烦.     
奇安信网战卫士的免费服务已于2024年5月终止,看来做公益也很烧钱啊      
**域名列表**:       
* qianxincdn.com

### 亚马逊云
* cloudfront.net

### Microsoft Azure
* mschcdn.com

### verycdn
* verycdn.net

### 金山云 
**介绍**        
坑货一个,不提供API的签名算法各语言的SDK     
**域名列表**:       
* ksyuncdn.com
* ks-cdn1.com

### 华为云 
* cdnhwc2.com

### 失控的防御系统/日出CDN
地址: scdn.io       
**介绍**        
小厂CDN,不要抱太大期待,节点全都是小鸡,1-1和2-2一大堆,带宽估计高不到哪去,不过小厂域名挺有个性    
**域名列表**:       
* cnmnmsl.top

### CNMCDN
地址: cnmcdn.cn     
**介绍**        
国内有证小厂CDN,很抗揍,价格较低               
**域名列表**:                      
* svipcdn.cn

### 星穹CDN
地址: domecdn.com       
**介绍**        
很便宜的CDN小厂     
**域名列表**:       
* cname.fun

### 云科
地址: waf.pro
**介绍**        
新的便宜小厂,目前还在部署系统

### 明赋云
地址: mingfucloud.com       
**介绍**        
知名的123云盘就是他们的东西,明赋云的CDN几乎算业内最低价,0.035元/GB,不过明赋云之前也干过一些不太道德的事
**域名列表**:       
* mingfucdn.com

### 括彩云
地址: kuocaicdn.com     
**介绍**        
价格与明赋云相似,但比明赋云略贵,不过有免费额度,而且可以通过bug白嫖流量
**域名列表**:       
* kuocaidns.com

### 京东云星盾
**介绍**        
这价格真的...太贵了吧,不过京东云的节点质量确实强,在国内也有很多自建机房
**域名列表**:       
* cloud-scdn.com

### 星域CDN
**介绍**        
知名PCDN网心云的CDN,节点质量参差不齐,导致体验不咋地,典型的例子就是Bilibili的直播,什么牛鬼蛇神都能跑赚钱宝,不过价格确实便宜,不过买的量要大,不然都懒得理你

### 多吉云
**介绍**        
融合CDN,没有自建节点,不过有一点免费额度
**域名列表**:       
* dogedns.com

### Edge one
**介绍**        
腾讯云边缘加速网络,类似于Cloudflare,价格便宜        
**域名列表**:               
* dnse2.com     

### 雨云
**介绍**        
自研融合CDN,也有部分自建节点,支持部分地域的内网回源,目前仍在测试中      
**域名列表**:       
* raincdn.cn        

### Cloudflare CN
**介绍**        
Cloudflare与京东云合作的CDN,价格低廉,不过质量很烂,但有消息称Cloudflare已结束与京东云的合作,转为自建节点     
**域名列表**:       
* cf-ns.com

### LEDCDN
地址: cdn.ledcdn.com    
**介绍**    
原来的 Qui CDN      
为希望优化大陆访问的个人站长提供公益 CDN
**域名列表**:   
* qiucname.tech

### 未来滴
地址: pro.dnss.vip      
**域名列表**:           
* dnss.vip      

### 亿速云
**介绍**    
阿里云CDN的代理     
**域名列表**:   
* kunlun*.com  

### 天翼云
**介绍**        
中国电信的云服务
**域名列表**:   
* ctdns.cn

### 知道创宇
**介绍**    
我也不知道
**域名列表**:   
* jiashule.com

### 方能CDN
**介绍**    
在itdog上打广告的小厂,看起来很垃圾
**域名列表**:   
* fn01.vip

### Greypanel 灰域CDN
**介绍**    
在itdog上打广告的小厂,外表看起来还不错?
**域名列表**:   
* greycdn.net

### 优速盾
**介绍**    
...
**域名列表**:   
* dun.kim

### 飞旭云
**介绍**    
https访问都不支持
**域名列表**:   
* vip1.waf-idc-scdn.xyz

### FreeCDN
**介绍**    
控制台为什么要带端口访问:(      
感觉站主是个MJJ,毕竟南非那机器一般人不会买
**域名列表**:
* freecdn.pw

### 级级盾
**介绍**    
有证,但是官网有点敷衍吧:(
**域名列表**:
* 1idc.cc

### 速御安全
**介绍**    
有证,看起来还不错?
**域名列表**:
* tyudns.com

### PTGCDN
**介绍**    
官网SSL都过期了...
**域名列表**:
* 

### 语鹿云盾CDN
**介绍**    
CDNfly
**域名列表**:
* cdnv8.cn









