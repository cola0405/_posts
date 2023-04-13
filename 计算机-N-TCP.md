---
title: 计算机-N-TCP
date: 2021-05-24 08:26:52
tags:
categories:
---

Transmission Control Protocol



TCP连接的建立（三次握手）

第一次握手（A发给B）

![image-20210524084347239](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524084347239.png)

然后SYN置为1（set）

随机初始序号2319633865

然后自己的序号sequence number为0 （自己的序号也可称为相对序号，relative sequence number）

第二次握手（B回复A）

![image-20210524084547340](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524084547340.png)

首先看Ack部分

ack=A自己序号+1即0+1=1 （relative ack number）

然后下面的ack序号为A的初始随机序号+1即2319633865+1=231963386

再是自己的序号从0开始

又随机生成一个序号670416643发给A

第三次握手（A回复B）

![image-20210524084814392](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524084814392.png)

A自己的序号=原序号+1即0+1=1

然后随机序号也+1

接下来是Ack部分

ack=B自己的序号+1即0+1=1

然后ack随机序号=B的随即序号+1即670416643+1=670416644

以上数据确认都没问题的话，就可以分配端口资源（套接字）然后正式建立连接了



Conclusion：

随机序号的作用

答：一定程度上防止TCP syn 攻击

建立连接时的标志位

答：涉及连接建立的TCP报文，SYN都置1，回复方的ACK置为1（第二次和第三次握手）

ACK和ack是不一样的，一个是标志位，一个是序号

ACK再标志位中的全称叫 Acknowledgment

关于相对序号

答:初始双方都是0，然后收到对方回复的ack后才有机会增加

---

 TCP连接的释放

（1）A发给B（A准备关闭连接）

![image-20210524212654486](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524212654486.png)

主要是在标志位FIN置为1

![](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524212759858.png)

Ps：SYN在连接释放时置为0

（2）B回复A

![image-20210524213038001](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524213038001.png)



ack加1

但是！relative sequence number 并未做加1操作

再看标志位

![image-20210524213208909](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524213208909.png)

FIN置为0，ACK置为1

此时，A的发送通道就关闭了，即A不能主动发送数据包到B了（但是可以被动回复B）

（建立连接后有两条通路，分别是A和B的发送通道）

（3）B发给A（B也准备关闭连接）

![image-20210524213407417](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524213407417.png)

relative sequence number 仍未做加1操作

ack也没有做加1操作

（也就是说，和之前B回复给A的数据包序号都一样）

再看标志位

![image-20210524213548780](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524213548780.png)

FIN置为了1

（4）A回复B

![image-20210524213612152](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524213612152.png)

relative sequence number 未做加1操作

ack加1了

再看标志位

![image-20210524213917593](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524213917593.png)



关于ack的总结

ack加1表示接收方确实受到了

每次回复时，ack都会加1

但是，连续发送两个TCP数据报，relative sequence number 是不会变化的（因为期间并没有收到对方的ack）

只有收到了对方的ack，相对序号才有加的机会

---

误区

序号每次只会加1

答：不对

举个例子

发送方，此时相对序号为769，发送了一个600字节数据

![image-20210524214756347](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524214756347.png)

接收方的回复

![image-20210524214911160](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210524214911160.png)

ack=769+600=1369

所以说，序号与发送数据的大小有关

