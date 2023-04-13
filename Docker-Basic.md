---
title: Docker Basic
date: 2021-03-28 12:49:35
tags:
categories:
---

```
sudo docker exec -it 775c7c9ee1e1 /bin/bash 
```



## 安装

### docker install

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
DRY_RUN=1 sh ./get-docker.sh
sudo sh get-docker.sh
```



---

### docker 导入文件

```bash
docker cp 你的文件路径 容器长ID:docker容器路径
```

```bash
docker cp /var/backup/nginx.zip 68b99:/cert
```



Docker 部署使用localhost时，一定要注意容器与容器，容器与主机之间的关系

Container

run container

1.check images

```
docker images
```

2.run images and attach it

```
docker run -i -t rastasheep/ubuntu-sshd:18.04 /bin/bash
```

```
-t: 在新容器内指定一个伪终端或终端。

-i: 允许你对容器内的标准输入 (STDIN) 进行交互。
```

3.exit

```
exit
```

4.daemon model

```
docker run -itd --name ubuntu-test ubuntu /bin/bash
```

```
-d daemon
```

---



## 导出镜像

1.export container

```
docker export 1e560fca3906 > ubuntu.tar
```

2.import 

```
cat ./ubuntu.tar | docker import - test/ubuntu:v1
```

```
docker import http://example.com/exampleimage.tgz example/imagerepo
```


