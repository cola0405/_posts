---
title: 工具-Vscode 编译运行C/C++
date: 2021-07-09 20:08:06
tags:
categories:
---

（Ps：该插件本质只是代替用户输入指令，多文件则不支持）

#### 下载编译器

 [MinGW 官网](https://osdn.net/projects/mingw/)

![image-20210709200912198](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210709200912198.png)

![image-20210709200926441](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210709200926441.png)

![image-20210709200939142](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210709200939142.png)

然后把MinGW下的bin加到环境变量中

```bash
gcc -V
```

#### 安装插件

1. C/C++
2. Code Runner

#### 运行


- run shortcut `Ctrl+Alt+N`

- stop shortcut `Ctrl+Alt+M`



#### bug

```bash
C:\Users\Jimmy>cd "f:\桌面\c\" && gcc Untitled-1.c -o Untitled-1 && "f:\桌面\c\"Untitled-1
'"f:\桌面\c\"Untitled-1' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```

解决：

配置settings.json

```
"code-runner.executorMap": {
        "c": "cd /d $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
        "cpp": "cd /d $dir && g++ -o $fileNameWithoutExt $fileName  && $dir$fileNameWithoutExt",
},
```

Ps：运行cpp要用g++





其他出现相同问题的同理





#### 调试

增加断点

F5开始调试