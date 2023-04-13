---
title: SpringCloud-Tutorial
date: 2021-12-29 13:40:11
tags:
categories:
---





# Dynamic scale up and down

Feign for rest client



# Fault tolerance

## hystrix

service shut down, then give some default response





# Gateway

## Netflix API gateway

rating limiting 



## tracing

Zipkin Distributed Tracing

(when the request go)





# Scalable 

可升级的





# Cloud native application



Spring Cloud build default cloud native app



# Spring Cloud and Spring Boot

where you can run jar

and you can run spring cloud app

![image-20211229135259084](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211229135259084.png)



## Configuration

### Config Server

![image-20211229135928243](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211229135928243.png)



Config server can store the config



refresh the config as the schedule 

you don't need to shut down the service and redeploy



or the config notify the micro to refresh







## Service Discovery

micro service know where they live



know the current URL, status



Netflix Eureka

zookeeper

consul



![image-20211229145753209](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211229145753209.png)





## Circuit Breakers

fault tolorance



## Routing and Message

request between micro service



## API Gateway

client to the micro service

![image-20211229140541204](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211229140541204.png)



确实，不仅仅是微服务之间需要discovery

client和server之间则是API Gateway 在帮忙







## Tracing

debugging

![image-20211229150941801](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211229150941801.png)

## CI pipelines and testing





??

test between the micro services



## Jenkins





## Spring cloud CLI







# Spring boot CLI

[仓库](https://repo.spring.io/ui/native/release/org/springframework/boot/spring-boot-cli)



```bash
spring install org.springframework.cloud:spring-cloud-cli:1.4.0.RELEASE
```





![image-20211229233854233](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211229233854233.png)





spring-boot-starter-parent的父依赖是spring-boot-dependences，里面管理了所有需要的默认的依赖版本。



Spring Cloud CLI 2.1.x will work with Spring Boot CLI 2.1.x
Spring Cloud CLI 2.0.x will work with Spring Boot CLI 2.0.x
Spring Cloud CLI 1.4.x will work with Spring Boot CLI 1.5.x