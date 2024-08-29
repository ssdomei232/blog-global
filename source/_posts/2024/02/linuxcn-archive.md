---
title: linux中国归档站-Linuxcat
tags:
- linux
categories: 
- 技术
index_img: /img/2024/linuxcn-archive/finally.jpg
banner_img: /img/2024/linuxcn-archive/finally.jpg
permalink: /linuxcn.html
date: 2024-02-25 11:29:54
---
在我看到[这篇文章](https://linux.cn/article-16603-1.html)后，我便想要将Linux中国的文章保留下来并渲染成我喜欢的主题,于是就有了[linuxcat.top](https://linuxcat.top/)

## 过程
渲染 Linuxcat 的过程极其烦人, windows 的最大打开文件数使我无法再 windows 上进行渲染
> User interface objects support only one handle per object. Processes cannot inherit or duplicate handles to user objects. Processes in one session cannot reference a user handle in another session.
There is a theoretical limit of 65,536 user handles per session. However, the maximum number of user handles that can be opened per session is usually lower, since it is affected by available memory. There is also a default per-process limit of user handles. To change this limit, set the following registry value:
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\USERProcessHandleQuota
This value can be set to a number between 200 and 18,000.

Linuxcat 使用 149kf 渲染大约用了 15 分钟,加上传文件和删删改改耗费了近一天的时间。(Linuxcat 完整的索引文件高达200M)

### 修改数据
头图和大图
```shell
shopt -s globstar
sed 's|largepic|banner_img|g' -i **/*.md
sed 's|pic|index_img|g' -i **/*.md
```
如果没有头图:
```python
import os
import re

def replace_content(dir_path):
    for root, dirs, files in os.walk(dir_path):
        for file in files:
            if file.endswith('.md'):
                file_path = os.path.join(root, file)
                
                with open(file_path, 'r+', encoding='utf-8') as f:
                    content = f.read()
                    
                    # 查找并提取 banner_img 后面的内容
                    match_banner = re.search(r'banner_img:\s*(.*)', content, re.IGNORECASE | re.MULTILINE)
                    if match_banner:
                        banner_img = match_banner.group(1).strip()  # 去除两边空白字符
                        
                        # 查找并替换 index_img 后面的内容
                        match_index = re.search(r'index_img:\s*(.*)', content, re.IGNORECASE | re.MULTILINE)
                        if match_index and 'islctt: false' in content:
                            new_content = re.sub(r'index_img:\s*.*?\n', f'index_img: {banner_img}\n', content, flags=re.IGNORECASE | re.MULTILINE)
                            
                            # 替换文件内容
                            f.seek(0)
                            f.truncate()
                            f.write(new_content)

# 调用函数，指定要遍历的目录
replace_content('_posts')
```
如果渲染是出现`Error: EMFILE, too many open files`报错,执行
```shell
ulimit -n 10000
```
如果还报错就把这个数改大点

## 有趣的发现
在渲染Linux中国数据集的过程中,由于Linux中国文章时间跨度极大,不难发现一些有趣的东西
### 人工智能
打开[标签 - AI - Linuxcat](https://linuxcat.top/tags/AI/),Linux中国共编写了347篇与AI相关的文章,最早的一篇在2016年  
2017年共3篇,2018年5篇,2019年共4篇,2020年共10篇,2021年共34篇,2022年共81篇,2023年共187篇  
2024年1月共22篇(约为2023年平均篇数的141.2%)  
由此可以看出,人工智能的发展并不是突然暴起的,而是循序渐进的,若按照2023年的增速,2024年Linux中国可能会有超过300篇有关AI的文章  


## 参考资料
[User Objects - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/sysinfo/user-objects)
[Home · Linux-CN/archive Wiki (github.com)](https://github.com/Linux-CN/archive/wiki)

在此感谢Linux中国的全体贡献者,感谢他们创作/翻译了这么多优质的内容,感谢他们为中文开源社区做出的贡献
