---
title: Spring MVC Tutorial
date: 2021-01-07 22:48:22
tags:
- SpringMVC
- Tutorial
categories:
- [SpringMVC,Tutorial]
---

1.New a Empty Maven project

2.Add "Web" module

Go to "Project Structure" -- "Modules"

3.Config dependencies

```xml
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.9.RELEASE</version>
        </dependency>
    </dependencies>
```

---

4.New "ApplicationContext.xml" in classpath

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <mvc:annotation-driven />
    <mvc:default-servlet-handler/>
    <context:component-scan base-package="xxx"/>

</beans>
```

Description

```
annotation-driven --  Spring MVC Controller programming model
default-servlet-handler -- Configures a handler for serving static resources
```

---

5.Config "web.xml"

```xml
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:ApplicationContext.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

---

6.Build Artifact

Go to "Project Structure"

```
Web Application exploded
```

Introduction

```
The dependencies will be put in a folder named "lib" in "WEB-INF"
```

---

7.Configure Tomcat

Go to "Deployment" 

Put war in it

Then change the "Application context" to "/"

So that you can access your application directly 

```
http://localhost:8080
```

---

END