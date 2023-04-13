---
title: 汇编-Java游记
date: 2022-04-22 22:40:17
tags:
categories:
---



# 词汇



ASCII => a:ski

C Language

Java => 家va:

Circuit => /'sɜːkɪt/

A minus B

negative B => 负B

queue => /kjuː/

formula => 公式

module => /'mɒdjuːl/ 不是抖！！！

token => /'təʊk(ə)n/ 偷

UID => unique ID



# AI

## Java结合AI

1. 使用Java的ProcessBuilder类来调用Python脚本 你可以使用Java的ProcessBuilder类来启动Python脚本并将数据传递给它。在Python脚本中，你可以加载所需的AI模型，对传入的数据进行预测并将结果返回给Java服务器。
2. 使用Python的flask框架和Java的HttpClient类进行通信 你可以使用Python的flask框架创建一个API来接收来自Java服务器的请求，并将数据传递给AI模型进行预测。Java服务器可以使用HttpClient类来发送请求和接收响应。
3. 使用Java的Jython库 Jython是一个将Python解释器嵌入到Java应用程序中的库。你可以使用它来加载Python模型并在Java中进行预测。
4. 将Python模型导出为Java可执行文件 一些AI框架，如TensorFlow和PyTorch，提供了将Python模型导出为Java可执行文件的功能。你可以将这些文件加载到Java应用程序中，并使用它们来进行预测。





# 编码

## 单复数问题

![image-20220427214228557](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214228557.png)

有些确实可能是为0的

你加s就不合适了





## final

![image-20220505230553515](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20220505230553515.png)



static final常量是好的，HotSpot VM里的JIT编译器会利用这个信息来做优化；



## 空格

![image-20220615173113696](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220615173113696.png)



# 传参

## 路径参数

```java
@RequestMapping(value = "/{id}", method = RequestMethod.GET)
public CommonResult<OmsOrderSetting> getItem(@PathVariable Long id) {
	...
}
```





# 日志



## 操作日志实现

基于AOP

[参考文档](https://cloud.tencent.com/developer/article/1655923)

![image-20220422224710414](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220422224710414.png)





## 规范

![image-20220427213017958](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213017958.png)

![image-20220427213045844](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213045844.png)

![image-20220427213106407](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213106407.png)



# 单元测试

写了单元测试之后，你就不用一个个接口去测了:)

![image-20220427213246557](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213246557.png)



例子：

```java
import cn.dev33.satoken.stp.StpUtil;
import com.alibaba.fastjson.JSON;
import com.lpcs.modules.user.controller.AccountManageController;
import com.lpcs.modules.user.entity.account.manage.AddSubAccountReq;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.HttpHeaders;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.transaction.annotation.Transactional;

import javax.annotation.Resource;

import com.lpcs.LpcsApplication;

import java.util.ArrayList;
import java.util.List;


@RunWith(SpringRunner.class)
@SpringBootTest(classes = LpcsApplication.class)
public class AccountManageTest {

    @Resource
    AccountManageController accountManageController;

    MockMvc mockMvc;

    String mainToken;

    String adminToken;

    @Before
    public void setup() {
        mockMvc = MockMvcBuilders.standaloneSetup(accountManageController).build();
        mainToken = buildMainToken();
        adminToken = buildAdminToken();
    }

    private String buildMainToken() {
        StpUtil.login(6427);
        return StpUtil.getTokenValue();
    }

    private String buildAdminToken() {
        StpUtil.login(6431);
        return StpUtil.getTokenValue();
    }



    @Test
    @Transactional
    public void addSubAccount() throws Exception {
        setup();
        String param = buildAddSubAccountParams();
        HttpHeaders headers = buildAddSubAccountHeaders();
        mockMvc.perform(
                MockMvcRequestBuilders.
                        get("/account/manage/add/sub/account").
                        content(param).
                        headers(headers)).
                        andExpect(MockMvcResultMatchers.status().isOk());
    }

    private HttpHeaders buildAddSubAccountHeaders() {
        HttpHeaders headers = new HttpHeaders();
        headers.add("lpcs_token", mainToken);
        headers.add("Content-Type","application/json;charset=UTF-8");
        return headers;
    }

    private String buildAddSubAccountParams() {
        AddSubAccountReq req = new AddSubAccountReq();
        List<Integer> permissions = new ArrayList<>();
        permissions.add(5);
        permissions.add(6);
        req.setPassword("123456");
        req.setDepartmentId(2);
        req.setRealName("小红");
        req.setLabel("保安2");
        req.setPermissions(permissions);
        String json = JSON.toJSONString(req);
        System.out.println(json);
        return json;
    }
}

```





# 用户考虑

![image-20220427213354984](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213354984.png)







# 安全



## sql注入

![image-20220427213427122](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213427122.png)



所以，这就是为什么不准用特殊字符的原因！！！

[参考](https://www.cnblogs.com/czfan/p/15039504.html)





## 用户传过来的参数大小

![image-20220427213912815](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427213912815.png)

# 注解

## 用作标记

AOP

```java
        try {
            result = joinPoint.proceed();
        } catch (Throwable throwable) {
            //有CacheException注解的方法需要抛出异常
            if (method.isAnnotationPresent(CacheException.class)) {
                throw throwable;
            } else {
                LOGGER.error(throwable.getMessage());
            }
        }
```



CacheException.class

```java
package com.macro.mall.security.annotation;

import java.lang.annotation.*;

/**
 * 自定义注解，有该注解的缓存方法会抛出异常
 * Created by macro on 2020/3/17.
 */
@Documented
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface CacheException {
}

```





# 数据库



![image-20230314144545530](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230314144545530.png)

## 与nosql的对比

![img](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/20200424200904550.png)



## 字段

![image-20220427214131128](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214131128.png)



## 小数

![image-20220427214355342](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214355342.png)



## 长文本

![image-20220427214435031](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214435031.png)



## 适当冗余

![image-20220427214525049](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214525049.png)







## 分库分表

![image-20220427214540021](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214540021.png)



## join

![image-20220427214631255](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214631255.png)



## 对字符串的索引

![image-20220427214654119](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214654119.png)



## COUNT

![image-20220427214906813](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214906813.png)



## SUM

![image-20220427214930276](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427214930276.png)









## 外键

![image-20220427215028118](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427215028118.png)





## 存储过程

![image-20220427215043543](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427215043543.png)





## 避免IN

![image-20220427215122290](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427215122290.png)





## 不用*

![image-20220427215158696](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427215158696.png)





## @Transactional

![image-20220427215329156](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427215329156.png)





# 设计模式

## Service Interface存在的意义

1. 使控制层只依赖这个接口

2. 当某天这个应用要跑在其它数据库上时，就而只需要增加一个serviceImpl类（不同的实现）

当然，当项目小，开发人员少或者且开发人员水平较高且接近的情况下

可以选择不写interface，可以减少编码





# Spring Cloud

## Eureka

The Netflix engineering team built a tool for this called **Eureka**, and open sourced it.

Eureka provides the means for microservices to power up

advertise their existence, and shutdown as well.

It supports multiple copies of the same service registering themselves





## Circuit Breaker

![image-20220425222632714](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220425222632714.png)





# Maven

## 多模块

父模块

pom.xml

```xml
	<!--模块的信息-->
	<groupId>org.example</groupId>
    <artifactId>multi-module-demo</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
	
	<!--指定子模块 -->
    <modules>
        <module>sub-module1</module>
    </modules>

	<!--指定项目内的子模块为依赖-->
    <dependencies>
        <dependency>
            <groupId>org.example</groupId>
            <artifactId>sub-module1</artifactId>
            <version>1.0-SNAPSHOT</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>
```



子模块

pom.xml

```xml
	<!--指定父模块关系-->
	<parent>
        <artifactId>multi-module-demo</artifactId>
        <groupId>org.example</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
	
	<!--该子模块名-->
    <artifactId>sub-module1</artifactId>
```







# 消息队列

## RabbitMQ

AMQP，即Advanced Message Queuing Protocol







# 异常

## 错误码

![image-20220427212419007](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427212419007.png)



## 异常处理

![image-20220427212557721](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427212557721.png)



![image-20220427212605295](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427212605295.png)



## NPE

![image-20220427212843146](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220427212843146.png)







## 直接插，再异常处理

异常处理再去更新



# 框架

## @Transational

“@Transactional”注解有两个出处，一是来自JAVA官方，包名为“javax.transaction”

一是来自Spring Framework，包名为“org.springframework.transaction.annotation”

在Spring框架中，大部分的情况下，它们都可以交换使用,效果是等价的

只不过Spring Framework提供的“@Transactional”功能更强，粒度更细

例如支持“TransactionManager”的配置、支持隔离性（isolation）、只读（isolation）、超时(timeout)等




# 情景

## token存redis的好处

服务器重启，仍可用
