---
title: vue-admin-demo
date: 2022-02-13 20:38:08
tags:
categories:
---

demo



[文档](https://element.eleme.cn/#/en-US/component/container)

Ps：

用的框架是`Element`

`vue-element-admin`只是使用`element`框架，做出来的一个成品

所以，要查文档，应该到`element`的文档去查



## Vue创建项目

不要用那个eslint

别忘了router



## Vue路由

```js
export default new Router({
  routes: [
    {
      path: '/',
      name: 'Layout',
      component: Layout,
      // 嵌套路由
      children: [{
        // 这里不设置值，是把main作为默认页面
        path: '/', 
        name: 'Main',
        component: Main
      },{
        path: '/user',
        name: 'User',
        component: User
      }]
    }
  ]
})
```



## Vue引入框架

```
npm install element
```

main.js

```js
// 添加element-ui
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI);
```

main中引入的，全局可以直接用

```vue
<el-container>
    <el-header>
      <p>
        I am Header
      </p>
    </el-header>

    <el-container>
      <el-aside>
        <p>aside</p>
        <p>aside1</p>
      </el-aside>
      <el-main>
        <!-- 主界面的路由，在index.js -->
        <router-view/>
      </el-main>
    </el-container>
  </el-container>
```



index.js

```js
// 只是部分相关代码
const routes = [
  {
    path: '/',
    name: 'Layout',
    component: Layout,
    children:[{
      path:'/',
      name:'Main',
      component:Main
    },{
      path: '/user',
      name: 'User',
      component: User
      }
      ]
  }
]
```





## Vue preset

vue 创建项目时的预设文件

`.vuerc`没有前缀

位置在`/User/用户名/.vuerc`



## yarn

![image-20220213203837247](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220213203837247.png)







# Vue颜色

```
# 背景，淡青色的那种
background-color: aliceblue;
```



## 颜色搭配





# Vue事件



```vue
<el-menu-item v-on:click="toWeatherPage()"></el-menu-item>
...
<script>
export default {
  ...
  methods:{
    toWeatherPage :function(){
      this.$router.push({path:'/weather'})
    }
  }
}
</script>
```



