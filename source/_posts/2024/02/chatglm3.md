---
title: chatglm3使用笔记
tags:
- AI
- 学习笔记
categories: 
- 学习笔记
index_img: /img/2024/2/17/chatglm3.png
banner_img: /img/2024/2/17/chatglm3.png
permalink: /2024/02/16/chatglm3/index.html
date: 2024-02-16 20:34:02
---
ChatGLM3是智谱AI和清华大学 KEG 实验室联合发布的对话预训练模型。  
ChatGLM3共有三种模型,如何选择请看[这里](https://modelscope.cn/models/ZhipuAI/chatglm3-6b/summary) 
实测windows 2022数据中心版+CUDA12.2+全部环境+anaconda+ChatGLM3-6b模型大约需要85G空间 
如果你没有GPU,那么可以来[启智](https://openi.pcl.ac.cn/user/sign_up?sharedUser=mei232)白嫖(真的白嫖,想充钱都充不了的,从前面的链接注册可以获得100积分,100积分在启智可以用11个小时A100,不过启智把内网穿透禁掉了,所以使用webui的模型没法跑)(其实也不是不能跑,就是自己改代码有点太麻烦了)
## 软件安装
运行ChatGLM3需要anaconda和Git,如果你的电脑上有,可以跳过这一部分。
### anaconda 
在[这里](https://docs.anaconda.com/free/anaconda/install/)选择合适的anaconda安装,安装时记得勾选添加环境变量
#### Conda 换源
如果你的机器不在大陆或连接默认源很快,可以跳过这一步
```shell
# 首先，看一下目前conda源都有哪些内容
conda info
# 然后，删除并恢复默认的conda源
conda config --remove-key channels 
```
换源
```shell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/
conda config --set show_channel_urls yes
```
### Git 
参照[这里](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)选择合适的Git安装(安装时直接一路点next就行) 

## 下载模型
具体如何让部署请参考模型官方仓库,这里只是一个示例(以从modelspace上使用Git下载为例) 
**三个模型按需选一个就行,不要全部下载**
```shell 
# 安装Git LFS
git lfs install
# ChatGLM3-6b
git clone https://www.modelscope.cn/ZhipuAI/chatglm3-6b.git
# ChatGLM3-6b-Base
git clone https://www.modelscope.cn/ZhipuAI/chatglm3-6b-base.git
# ChatGLM3-6B-32K
git clone https://www.modelscope.cn/ZhipuAI/chatglm3-6b-32k.git
```
模型很大,可能需要等待较长时间
## 环境部署
执行以下命令新建一个 conda 环境并安装所需依赖：
```shell
conda create -n chatglm3-demo python=3.10
# 如果这一步报错,试试 activate chatglm3-demo
conda activate chatglm3-demo
# 如果下载过慢请使用 pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple 更换pip源
pip install -r requirements.txt 
```
### pytorch & CUDA
默认安装的pytorch可能不带有CUDA支持,请参照一下步骤重装/安装带有CUDA支持的pytorch
#### 安装带有CUDA支持的PyTorch
```shell
pip install torch torchvision torchaudio -f https://download.pytorch.org/whl/cu111/torch_stable.html
``` 
其中的cu111表示支持CUDA 11.1,自行替换为你的CUDA版本,在安装前记得先访问一下这个URL,看看你的CUDA版本是否受到支持 
**如果你的CUDA版本为12.2,可以安装支持CUDA12.1的pytorch**
#### 验证安装
安装完成后，可以在Python环境中检查PyTorch是否正确识别到了CUDA：
```python
import torch
print(torch.cuda.is_available())
```
如果返回True，则说明PyTorch已成功启用CUDA支持

## 代码修改
请先看完下面这部分内容,如果符合你的情况,你可以选择直接克隆我已经修改好仓库 
```shell
# Github
git clone https://github.com/ssdomei232/ChatGLM3-easydemo.git
# 如果你访问GitHub比较困难,可以用下面这个
git clone https://openi.pcl.ac.cn/mei232/ChatGLM3.git
```
ps:如果你觉得我弄的配色很丑,可以在右上角改掉  
如果你使用windows或带有桌面的linux,更推荐你使用`composite_demo`,如果你使用命令行的linux,请使用`basic_demo`体验
### 模型量化
默认情况下，模型以 FP16 精度加载，运行ChatGLM3-6b模型需要大概13GB显存。如果你的 GPU 显存有限，可以尝试以量化方式加载模型，使用方法如下：
运行4-bit量化的ChatGLM3-6b模型大约需要8G显存.
#### 综合demo
如果你使用windows或带有桌面的linux,请看这部分内容 
找到`client.py` 130行左右
```python 
self.model = AutoModel.from_pretrained(
                model_path,
                trust_remote_code=True,
                config=config,
                device_map="auto").eval()
            # add .quantize(4).cuda() before .eval() and remove device_map="auto" to use int4 model
```
改为
```python 
self.model = AutoModel.from_pretrained(
                model_path,
                trust_remote_code=True,
                config=config,
                ).quantize(4).cuda().eval()
            # add .quantize(4).cuda() before .eval() and remove device_map="auto" to use int4 model
```
`client.py `150行左右,
```python
self.model = AutoModel.from_pretrained(MODEL_PATH, trust_remote_code=True, device_map="auto").eval()
```
改为
```python
self.model = AutoModel.from_pretrained(MODEL_PATH, trust_remote_code=True).quantize(4).cuda().eval()
```
#### 命令行对话 Demo
如果你使用命令行的linux,请看这部分内容 
找到cli_demo.py第八行左右
```python
model = AutoModel.from_pretrained(MODEL_PATH, trust_remote_code=True, device_map="auto").eval()
```
改为
```python 
model = AutoModel.from_pretrained("THUDM/chatglm3-6b", trust_remote_code=True).quantize(4).cuda().eval()
```

### 从本地加载模型
如果你的机器位于某堵墙内或无法访问huggingface,有或者你已经提前下载好了模型,请看这部分内容
#### 综合demo
如果你使用windows或带有桌面的linux,请看这部分内容 
找到client.py第十八行左右
```python
MODEL_PATH = os.environ.get('MODEL_PATH', 'THUDM/chatglm3-6b')
```
改为
```python
# 模型文件放在同目录chatglm3-6b目录下,如果你想放在别处,请自行修改
MODEL_PATH = 'chatglm3-6b'
```
#### 命令行对话 Demo
如果你使用命令行的linux,请看这部分内容 
找到cli_demo.py第四行左右
```python
MODEL_PATH = os.environ.get('MODEL_PATH', 'THUDM/chatglm3-6b')
```
改为
```python
# 模型文件放在同目录chatglm3-6b目录下,如果你想放在别处,请自行修改
MODEL_PATH = 'chatglm3-6b'
```

## 运行
### 综合demo
```shell
conda activate chatglm3-demo
cd composite_demo
streamlit run main.py
```
稍等一会加载模型,加载完浏览器会自动弹出到webui,若没有自动弹出,请查看命令行输出手动开启
### 命令行对话 Demo
```shell
conda activate chatglm3-demo
cd basic_demo
python cli_demo.py
```
稍等一会加载模型,加载完就可以开始对话

### 温馨提示
相当不建议你使用CPU来运行,除非你使用AMD的线程撕裂者之类的CPU,否则就不要难为电脑了.

## 参考资料
[Conda 替换镜像源方法尽头，再也不用到处搜镜像源地址](https://blog.csdn.net/adreammaker/article/details/123396951)
[THUDM/ChatGLM3: ChatGLM3 series: Open Bilingual Chat LLMs | 开源双语对话语言模型](https://github.com/THUDM/ChatGLM3)

