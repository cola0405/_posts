---
title: Spring Security Fliter
date: 2021-05-25 10:28:44
tags:
categories:
---



Difference from addBefore and addAfter

#### Security 拦截多请求

```java
http.antMatcher("/user/**").antMatcher("/login/dgut").authorizeRequests()...
```

xxxxxxxxxxxxxxxxxx