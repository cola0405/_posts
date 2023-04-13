---
layout: 
title: SpringBoot Helloworld
date: 2021-12-29 08:35:54
tags:
---







## 版本选择

spring boot

```
2.3.2.RELEASE
```

Springboot3 强制要求Java17

有时还是用Springboot2吧，然后都设置成Java8





# 建立项目

JDK不一致会有问题（404），但是idea并不报错



https://start.aliyun.com/



# 依赖



Web-SpringBoot web



# Controller

建立包，然后

```java
@Controller
public class Hello {

    @RequestMapping("/hello")  	// http://localhost:8080/hello
    @ResponseBody  				// 不进行页面跳转，而是返回字符串
    public String hello(){
        return "hello";
    }
}
```





# Dao



## 实体类

```java
@Data
@Entity(name = "tb_user")       // 实体类，值为表名
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)  //主键自增
    private Long id;
    private String name;
    private String password;
    private String role;

    public String getUsername() {
        return name;
    }
    
}
```



## 数据库访问接口

```java
public interface UserRepository extends JpaRepository<User,Long> {
    @Query(value = "select COUNT(*) from tb_user where role = 'USER'",nativeQuery = true)
    long getUserNum();
}
```



## 数据库接口参数

```bash
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/db_authority?serverTimezone=GMT%2B8
spring.datasource.username=root
spring.datasource.password=123456
spring.jpa.hibernate.naming.physical-strategy= org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
```



解释：

```bash
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

依赖

```xml
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
```





## dao调用

```java
@Resource
UserRepository userRepository;

@RequestMapping("/getUserNum")
@ResponseBody
public long getUserNum(){
    return userRepository.getUserNum();
}
```



