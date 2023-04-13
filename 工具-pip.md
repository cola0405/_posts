---
title: 工具-pip
date: 2021-03-27 19:34:20
tags:
categories:
---







```
-i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```



pip目录的位置

![image-20220811143439963](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220811143439963.png)

```
pip install -r requirements.txt
```



**ignore**



```
pip install -r requirements.txt --ignore-installed
```



SSL的问题

![image-20220811143956569](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220811143956569.png)





有些库的版本只支持Linux，不支持Windows，导致pip install 失败

![image-20220811144327978](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220811144327978.png)





update pip

```
python -m pip install --upgrade pip
```

use mirror

```
pip install scrapy -i https://pypi.tuna.tsinghua.edu.cn/simple
```

```
pip install -r ./requirements.txt -i https://pypi.douban.com/simple/
```



```
报错
The repository located at pypi.douban.com is not a trusted or secure host and is being ignored. If this repository is available via HTTPS it is recommended to use HTTPS instead, otherwise you may silence this warning and allow it anyways with '--trusted-host pypi.douban.com'.
```

```
解决
将url中的http修改为https
```

```
Linux 下pip无法安装的，pip3支持
```



