---
title: transformers_learning
date: 2023-03-21 18:10:45
tags:
categories:
---







![image-20230321181455710](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321181455710.png)



![image-20230321181624461](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321181624461.png)





然后是更细化的encode（矩阵运算）

![image-20230321182522002](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321182522002.png)



从这里也可以看到value, key, query 都是统一的矩阵

只是他们将会进行的运算不一样

![image-20230321182704207](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321182704207.png)





然后key和value参与一系列运算后（左边），和query再运算（右边）

![image-20230321182820031](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321182820031.png)





multi head 的输出

![image-20230321182958355](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230321182958355.png)



把multi head 的输出 和head前的输入结合运算

![image-20230321183016978](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321183016978.png)





再一步，得到encoder的最终输出（即完成“我很好”的编码，包含了**字的位置信息**和**字之间的关联** 等信息）

![image-20230321183101827](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321183101827.png)







右边的decoder同理，只是encoder的输出做key和value再来一遍

![image-20230321183255419](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321183255419.png)





最后每个位置做一个百万分类，得到 “I am fine”

![image-20230321183326613](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230321183326613.png)
