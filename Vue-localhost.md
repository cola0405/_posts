---
title: Vue localhost
date: 2021-06-06 16:12:48
tags:
categories:
---



## 只能通过localhost访问

解决:

```
1.查看`config`文件夹下的 `index.js`，将`dev`中将`host`重新定义为：`0.0.0.0`即可

2.修改`package.json`中`script`下`dev`的值，在后面加入`--host 0.0.0.0` 也可以解决
```

Note

> 别忘了把防火墙给关了