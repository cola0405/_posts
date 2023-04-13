---
title: first-order-model-demo
date: 2022-01-11 12:38:11
tags:
categories:
---





## 构建环境

```bash
pip install -r requirements.txt
```



## 视频转换的准备

借助 face-alignment 获取crop视频的参数

```bash
git clone https://github.com/1adrianb/face-alignment
cd face-alignment
pip install -r requirements.txt
python setup.py install

python crop-video.py --inp super-idol.mp4 --cpu
```

```bash
ffmpeg -i super-idol.mp4 -ss 0.0 -t 14.366666666666667 -filter:v "crop=643:643:7:134, scale=256:256" crop.mp4
```





### numpy版本不适配的问题

可以单独把 crop-video.py copy使用

它并不依赖于first-order-model



### AssertionError: Torch not compiled with CUDA enabled

```bash
For non NVIDIA users: --cpu flag will fix this.
```



## 安装ffmpeg

```bash
brew install ffmpeg
```







## 运行

```bash
python demo.py  --config config/taichi-256.yaml --driving_video ./crop.mp4 --source_image captain.jpg --checkpoint ./taichi-cpk.pth.tar --relative --adapt_scale --cpu
```

```bash
python demo.py  --config config/dataset_name.yaml --driving_video path/to/driving --source_image path/to/source --checkpoint path/to/checkpoint --relative --adapt_scale
```



### AssertionError: Torch not compiled with CUDA enabled

```bash
For non NVIDIA users: --cpu flag will fix this.
```







## 这种python 项目都创建新虚拟环境吧

别去影响自己原来的库



## Anaconda可以不可创建任意版本的python解释器

没有任意版本，但确实还有其他版本，比如说3.7等等

然后再Pycharm里选conda的环境

![image-20220111125244953](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220111125244953.png)



## 进入虚拟的python环境

在Pycharm中打开命令行即可以进入到虚拟环境中

![image-20220111133302445](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220111133302445.png)





## checkpoint 是什么

二进制文件，储存了模型中的各个变量

没有什么数据结构

