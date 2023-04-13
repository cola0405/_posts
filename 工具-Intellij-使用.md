---
title: 工具-Intellij 使用
date: 2021-06-08 09:12:21
tags:
categories:
---

有些函数没有解释，是需要先下载源码先



#### lombok报错

```
java.lang.IllegalAccessError: class lombok.javac.apt.LombokProcessor cannot access class com.sun.tools.javac.processing.JavacProcessingEnvironment [duplicate]
```

解决

Switch to at least the `1.18.20` version of Lombok that contains [the fix](https://github.com/rzwitserloot/lombok/issues/2681)

```
<dependency>
  <groupId>org.projectlombok</groupId>
  <artifactId>lombok</artifactId>
  <version>1.18.20</version>
</dependency>
```



# 无效的源发行版：14

1.Project Structure-SDK version

2.Module-Language Level

3.Build,Execution,Deployment - Java Compiler - project bytecode version 





# resolving maven depen...

解决：

Build, Execution, Deployment - Build Tools - Maven - Runner - VM options

```bash
-DarchetypeCatalog=internal
```





# 莫名其妙扫描不到存在的文件

解决：

清缓存--重启Intellij
