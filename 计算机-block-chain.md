---
title: 计算机-block-chain
date: 2022-05-31 17:14:53
tags:
categories:
---



# POW

Proof of work

工作量证明

![image-20220531171607351](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220531171607351.png)

首先，工作量就是那一串字符串—— Hash(previous hash + timestamp + nounce + root)

枚举没意义的，只能不停地通过改变nonce去Hash

（0的个数是difficulty，需要的0越多，mining越难）

当你计算Hash出了一串前n位为0的字符串时，把你的构造参数告诉其他人

然后其他人验证之后，发现这个串真的被你Hash出来了，承认了你

（这里的其他人可以是区块链的用户，他们其实更喜欢你早点把矿挖出来，因为他们的钱就更快到账了）

然后你就可以得到报酬了~



# Smart Contracts

智能合约

代码写在区块链上

自动执行

![image-20220531173233523](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220531173233523.png)



must pay back the loan before the transaction ends

otherwise the smart contract reverses the transaction
