---
title: 工具-bat脚本
date: 2021-09-05 00:39:26
tags:
categories:
---

# 执行含中文的命令

记事本打开文件，另存为ANSI 编码



# 出现错误导致外部程序无法正确运行

使用vbs间接运行

```bash
set ws=WScript.CreateObject("WScript.Shell")
ws.Run "E:\Colleage\7\政治优题库.bat",0
```

