---
title: Vue 数据传输
date: 2021-06-11 10:06:28
tags:
categories:
---

#### 页面刷新后，prototype挂载的全局变量消失

```
在页面刷新时
vue实例对象被重新构造
所有变量都被初始化
```

解决：

---

#### Vue 路由传递数据

```js
handleClick (row) {
      this.$router.push({
        path: '/unpostInfo',
        query: {
          unpostInfoId: 1
        }
      })
    }
```

数据获取

```js
this.$route.query.unpostInfoId
```

Ps:是$route而不是router

---

#### Vue 表格传递数据(一行的全部数据)

scope

```html
<template slot-scope="scope">
   <el-button @click="handleClick(scope.row)" type="text" size="small" v-if="scope.row.role === 'USER'" :id="scope.row.username">锁定</el-button>
   <el-button @click="handleClick(scope.row)" type="text" size="small" v-else :id="scope.row.username">取消锁定</el-button>
</template>
```



---

#### Vue 设置id

```html
<div :id="scop.row.username"></div>
```

---

