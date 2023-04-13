---
title: cpp web
date: 2023-01-12 09:37:52
tags:
categories:
---



cmake

g++

```
sudo apt-get install cmake
sudo apt-get install g++
```



boost

```
sudo apt install libboost-all-dev
```

openssl

```
sudo apt-get install libssl-dev
```









## 源

```
sudo sed -i "s@http://.*archive.ubuntu.com@https://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list
sudo sed -i "s@http://.*security.ubuntu.com@https://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list
```





## check c++ standard

```c++
#include<iostream>

int main() {
    if (__cplusplus == 201703L) std::cout << "C++17\n";
    else if (__cplusplus == 201402L) std::cout << "C++14\n";
    else if (__cplusplus == 201103L) std::cout << "C++11\n";
    else if (__cplusplus == 199711L) std::cout << "C++98\n";
    else std::cout << "pre-standard C++\n";
}
```







## concept



### 句柄和描述符

Windows 平台——“句柄”

 Linux 平台——“描述符”





## Socket

插座



为了表示和区分已经打开的文件，UNIX/Linux 会给每个文件分配一个 ID，这个 ID 就是一个整数，被称为文件描述符（File Descriptor）。例如：

- 通常用 0 来表示标准输入文件（stdin），它对应的硬件设备就是键盘；
- 通常用 1 来表示标准输出文件（stdout），它对应的硬件设备就是显示器。


UNIX/Linux 程序在执行任何形式的 I/O 操作时，都是在读取或者写入一个文件描述符。一个文件描述符只是一个和打开的文件相关联的整数，它的背后可能是一个硬盘上的普通文件、FIFO、管道、终端、键盘、显示器，甚至是一个网络连接。

请注意，网络连接也是一个文件，它也有文件描述符！你必须理解这句话。



我们可以通过 socket() 函数来创建一个网络连接，或者说打开一个网络文件，socket() 的返回值就是文件描述符。有了文件描述符，我们就可以使用普通的文件操作函数来传输数据了，例如：

- 用 read() 读取从远程计算机传来的数据；
- 用 write() 向远程计算机写入数据。


你看，只要用 socket() 创建了连接，剩下的就是文件操作了，网络编程原来就是如此简单！





## compile and run

```
g++ -o output foo.cpp
```







## wsl-vs

修改配置文件

```
sudo vi /etc/ssh/sshd_config
```

```
port=22
PasswordAuthentication yes
PermitRootLogin yes
```





wsl开启ssh

```
sudo service ssh start
sudo service ssh restart
```



Windows端ssh测试

```
ssh cola@localhost
```



如果ok，则开始配置vs

“Tool” -- “Options” -- “Cross Platform” -- “Connection Manager” -- “Add”







