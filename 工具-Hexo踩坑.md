---
title: 工具-Hexo踩坑
date: 2020-11-05 21:24:29
tags:
- Config
categories:
- [Config,Hexo]
---

####　ssh密匙

```java
ssh-keygen -t rsa -C "邮件地址"
```

找到`.ssh\id_rsa.pub`文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：

将刚复制的内容粘贴到key那里，title随便填，保存。

Win10下的~目录就是对应User下

然后，id_rsa.pub这个文件不能直接打开，需要命令行指令

```java
more id_rsa.pub
```

#### 常用指令

```java
hexo new "postName" #新建文章
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #部署到GitHub
hexo version  #查看Hexo的版本
# 你先执行hexo clean 然后再删除文章就可以了
```

部署步骤：

```
hexo clean
hexo generate
hexo deploy
```

#### 每篇文章的配置

示例：

```
title: Spring注解是怎么工作的
date: 2020-11-05 17:05:39
tags:
- Spring
- Java
categories:
- [Java,Spring]
```

#### 配置文件的修改

_config.yml

```
# Site
title: 藏经阁
subtitle: ''
description: '太多东西要学啦'
keywords: Java
author: FreeJim
language: zh
timezone: 'Asia/Hong_Kong'
```



```
deploy:
  type: git
  repo: https://github.com/a1020151695/a1020151695.github.io
  branch: main
```

具体可查[官方文档](https://hexo.io/docs/configuration)



#### 自定义域名

Setting中设置自定义域名，然后Save保存

阿里云域名管理，要添加两个纪录

一个是CNAME www 把	把当前域名和xxx.github.io联系起来

其实是把xxx.github.io指向你自己的域名

CNAME content(Just the domain)

```
freejim.icu 
```

第二个是@ 你自己的域名指向一个IP（即xxx.github.io的实际IP）

这里我踩了坑！

你不能在你自己电脑上Ping！！！！

拿你的云服务器去ping才有用

或者不需要服务器，直接网上找一个域名解析的网站，去查

例如[这个](https://site.ip138.com/)



gtihub上看得见的文件都是在“source”文件夹里面的---CNAME--域名配置文件

#### 站长工具

然后 如果要向google提交验证的话，我们用meta的方式

如果用html的方式的话，hexo部署的时候会修改html文件里的内容

导致google无法验证

然后你也不能直接放到github中

因为github仓库不完全等于hexo部署的服务器

所以我们选择meta

然后hexo是通过各主题模板来修改、生成各网页的

和meta相关的head的模板在这

```
themes\landscape\layout\_partial\head.ejs
```

把google 给的meta 加进去就好了

添加后可以在这里查看网站数据

```
https://search.google.com/search-console/about
```

查看是否验证成功

几天后，google搜索：

```
site:“你的网站”
```

之后我看了百度的验证

不行！

github把百度屏蔽掉了

```
不到一分钟前freejim.icu使用HTML标签验证
原因：服务器连接超时，请检查服务器设置或者稍后重试。
问题分析&解决办法： 连接网站时超时，可能是网络速度过慢，请检查服务器网络线路，或者稍后再试。
```

不允许百度去爬

```
对此github官方是这样说的 : 由于百度爬虫爬得太猛烈，已经对很多Github用户造成了可用性的问题了，而禁用百度爬虫这一举措可能会一直持续下去。
```

---

>Please make sure you have the correct access rights

原因:

可能无意间动了ssh密钥，id_rsa.pub

rsa， ssh-keygen 等

解决：

在github的setting中新增ssh密钥

![image-20210609163127564](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20210609163127564.png)

#### 派生文件夹

_config.yml

```bash
post_asset_folder: true
```





## 搜索功能失效

```
search:
  path: search.json
  field: post
  format: html
  limit: 100000
```

用 `search.json` 而不用`search.xml`
