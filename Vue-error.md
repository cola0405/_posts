---
title: Vue error
date: 2021-06-09 23:33:31
tags:
categories:
---



> Component template should contain exactly one root element

解决

```
用一个div把template内的多个标签包起来就行
```

---

#### vue 没有错误信息

```bash
npm run build  //可以显示详细信息
```



## 包老是下载错误

把package.json里的依赖给删了

自己另外手动安装



中途改的话

得把原来的node_module给删了重新install
