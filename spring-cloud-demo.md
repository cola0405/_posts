---
title: spring-cloud-demo
date: 2022-04-09 20:53:38
tags:
categories:
---

[demo](https://gitee.com/simple_one1/spring-cloud-demo)

# 注意版本

再pom中招Spring Boot 和 cloud的版本信息

![image-20220409205417331](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220409205417331.png)



借鉴他人代码的时候留意他们Spring Boot 的版本









## 配置



![image-20230411154059031](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230411154059031.png)

![image-20230411154014709](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230411154014709.png)



### 注意事项



```java
@EnableEurekaClient
@SpringBootApplication
public class ConsumerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConsumerApplication.class, args);
    }
}
```



@EnableEurekaClient都是能够让注册中心能够发现，扫描到该服务



## 说明

```java
restTemplate.getForObject("http://producer/", String.class);
```

![image-20220409224502792](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220409224502792.png)

负载均衡会随机分配给名为producer

application.name也不用担心重复

因为eureka遇到重复的application.name会把他们归在一起

`application.properties`

```
spring.application.name=producer
```

