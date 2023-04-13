---
title: clion
date: 2023-01-09 14:38:52
tags:
categories:
---





## 单独运行c++文件

C/C++ Single File Execution Plugin

然后

```
cmake_minimum_required(VERSION 3.24)
project(usaco_cpp)

set(CMAKE_CXX_STANDARD 17)

add_executable(usaco_cpp main.cpp)

add_executable(t t.cpp)
```





## out文件位置到当前目录

编辑配置 - Working Dir 修改为：

```
$FileDir$
```

