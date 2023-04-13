---
title: Spring Boot with Docker
date: 2021-04-26 09:37:54
tags: Docker
categories:
---

1. Jar

```
mvn clean install
```

2. Dockerfile

new a "Dockerfile"

```
FROM openjdk:16-jdk-alpine
EXPOSE 8080
ADD docker_demo-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]
```

3. Build images

```
docker build -t demo/hello .
```

4. Run App

```
docker run -p 8080:8080 demo/hello
```



（要连接数据库的，还得先构建数据库）



#### Spring Boot 云服务器 Mysql

docker拉镜像建立MySQL方便
