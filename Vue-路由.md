---
title: Vue 路由
date: 2021-06-04 17:07:49
tags:
categories:
---



## 页面跳转

```html
<a href="hello.html">Hello</a>
```

hello.html和index.html同级

---

#### 直接的页面跳转

```js
this.$router.push('/url')
```



---

## 组件切换(初始化时没有routers.js的情况)

[DEMO](https://github.com/a1020151695/vue-component-shift)

1.引入VueRouter，统一管理路由

main.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import routers from './routers'
import App from './App'

Vue.use(VueRouter)

const router = new VueRouter({
  mode: 'history',
  routes: routers
})

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})

```



2.新建routers.js（和main.js同级）

```js
import Home from './components/Home.vue'  // 引入要显示的组件

const routers = [
    {
        path: '/home',  // 设置好route
        name: 'home',
        component: Home
    },
]
export default routers

```

4.自定义组件 Home.vue（在components/）

```vue
<template>
<p>xxxxxx</p>
</template>

<script>
    export default {
        name: "Home"
    }
</script>

<style scoped>

</style>

```



3.App.vue

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <br>
    <router-link to="/home">Test</router-link>
    <router-view/>
  </div>
</template>
```

---

> 初始化有router的话，直接在其index.js下改就行了