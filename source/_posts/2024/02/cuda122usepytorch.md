---
title: CUDA12.2使用支持CUDA的pytorch
tags:
- AI
- python
- 学习笔记
categories: 
- 学习笔记
index_img: /img/2024/2/17/torch.png
banner_img: /img/2024/2/17/torch.png
permalink: /2024/02/17/cuda122usepytorch/index.html
date: 2024-02-17 11:36:55
---
如果你在nvidia官网安装了最新版的CUDA(CUDA12.2/12.3),但访问 [https://download.pytorch.org/whl/cu122/torch_stable.html](https://download.pytorch.org/whl/cu122/torch_stable.html) 就会发现pytorch并没有支持此版本的CUDA       
但是支持CUDA12.1的pytorch也可以支持CUDA12.2(看网上说CUDA12.3也可以支持,但没有试过) 
执行    
```shell
pip install torch torchvision torchaudio -f https://download.pytorch.org/whl/cu121/torch_stable.html
```
来安装支持CUDA12.1的torch
### 检查
创建一个.py文件,内容为:
```python
import torch
print(torch.cuda.is_available())
```
运行它,如果返回True,则说明PyTorch已成功启用CUDA支持
如果返回False,那么重装一下torch或重启一下服务器应该就好了