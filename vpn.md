---
title: vpn
date: 2021-09-15 14:56:00
tags:
categories:
---





# vpn简介

VPN是英文Virtual Private Network的缩写，翻译过来就是虚拟专用网络。VPN最初的设计是为了让世界上任一两台电脑，在一个加密的通道中传输数据，保障通信数据的安全，只是在数据上加密了，而不是在硬件上区别开来，所以就称为虚拟。国内的手机或电脑设备连接国外服务器，建立VPN加密通信，也因此成为了绕过网络封锁的翻墙工具。VPN相比于Shadowsocks来说要更加底层一些，它首先通过操作系统虚拟一张网卡，之后所以的收发数据都通过这张网卡加密。



# 中国防火长城

防火长城GFW是英文Great Firewall的缩写，也叫做墙，最开始是因为一名外国人写的《The Great Firewall of China》的文章而得名，又由于防火墙的原因，在网络上演变成了”墙“，表示访问境外的网站，如Facebook、Twitter、YouTube等网站被阻拦，主要通过拦截方式为：1）黑名单的方式污染DNS解析，在黑名单中的域名会被解析到无效的IP地址，从而表现为网站不能访问。2）IP地址封锁，由于大部分被封锁的网站使用的是"虚拟主机"，所以一旦某个ip被封锁，这个虚拟主机上的网站也会被封，国内无法访问。这种方式主要是通过自动分析出入境流量的特征，墙也在不断自我学习进化，目前的自建梯子较流行的协议，比如SS(R)、V2ray、、Trojan、Vmess等在大封锁期间都无法幸免，IP大批上黑名单。3）针对HTTP关键字过滤，中国防火长城会针对某些关键字进行过滤。其实网络审查制度不只是中国存在，其他国家也存在网络审查制度，但是仅仅用于金融洗钱、国际诈骗等犯罪行为，而防火长城的则会监控所有国际通讯，对不符合规定的传输内容进行屏蔽。域名解析服务缓存污染是防火长城常见的拦截手段，所有出口骨干路由在UDP的53端口的域名查询都会被检测，一旦所访问的域名不符合规定，防火长城就会返回错误域名解析地址。

# vpn商

## panda

[点击访问官网](https://www.panhdpe.xyz/)

## strong

[Strong](https://strongvpn.com/)

## 蓝灯

[蓝灯下载](https://gitlab.com/getlantern/lantern-binaries-mirror/-/raw/master/lantern-installer.exe)

[备用1](https://s3.amazonaws.com/lantern/lantern-installer.exe)

[备用2](https://github.com/getlantern/lantern-binaries/raw/master/lantern-installer.exe)



## xx-net

[下载](https://github.com/XX-net/XX-Net/releases/download/4.5.2/XX-Net-windows-4.5.2.7z)

## firefly

[下载](https://raw.githubusercontent.com/cdtmirrors/yhc/master/yhc.exe)

## 西部世界

[官网](https://xbsj9729.website/)

## pure

[点击访问官网](https://my.purevpn.com/login)

## lvacy

# **[点击访问官网](https://www.ivacykodi.com/)**