---
title: docker mysql
date: 2021-06-19 10:01:58
tags:
categories:
---

```
# docker 中下载 mysql
docker pull mysql:5.7

#启动
sudo docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7

#进入容器
sudo docker exec -it mysql bash

#登录mysql
mysql -u root -p

# 外部访问
grant all privileges on *.* to root@'%' identified by "password";
```



传输sql文件

```
docker cp <path> container_name:path
```



执行sql文件

```
source xxx.sql
```



修改密码

```
SET PASSWORD FOR 'root'@'%' = '1a1a1a1A';
```

Ps

如果是root@localhost的话，只是修改本地访问mysql的密码

而不能修改外部访问的密码
