---
title: 工具-gitignore
date: 2022-02-28 10:04:36
tags:
categories:
---



# 样例

```
HELP.md
target/
!.mvn/wrapper/maven-wrapper.jar
!**/src/main/**
!**/src/test/**

### STS ###
.apt_generated
.classpath
.factorypath
.project
.settings
.springBeans
.sts4-cache

### IntelliJ IDEA ###
.idea
*.iws
*.iml
*.ipr

### NetBeans ###
/nbproject/private/
/nbbuild/
/dist/
/nbdist/
/.nb-gradle/
build/

### VS Code ###
.vscode/
.mvn
.DS_Store
mvnw
mvnw.cmd
```





# 使用

新建.gitignore文件

```
# 删除之前缓存的文件
git rm -r --cached .
```

重新

```
# 此时的add操作会删除.gitignore中包含的文件
git add .
git commit -m ""
git push
```

