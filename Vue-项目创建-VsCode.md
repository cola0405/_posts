---
title: Vue-项目创建-VsCode
date: 2021-06-06 15:18:07
tags:
categories:
---

所需插件：

```
Vetur  // Vue开发插件
ESLint // 代码校验
```

工具：

```
npm install -g vue-cli
```

命令:

```
vue init webpack projectName
```

```
npm install
```

```
npm run dev
```

---

```
You seem to be using old vue-cli and 
scaffolded your project using vue init webpack <project-name>.

Since it all evolved into vue cli 3
old vue-cli is deprecated
we are now using @vue/cli
vue create <project-name> for scaffolding out projects.

It's perfectly fine for you to use the old way(and I still do sometimes)
vue.config.js is the global configuration file for your project 
when you are using @vue/cli. Check more about it here.

For webpack configurations when using vue-cli
in projects scaffolded using npm init command
check the /build directory in the root of the project folder.
```



## 新建项目启动慢

解决：更换npm的源

```bash
npm config set registry https://registry.npm.taobao.org
```

