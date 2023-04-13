---
title: blog-app-demo
date: 2022-01-16 12:10:40
tags:
categories:
---



## Gridsome 

基于 Vue.js 构建的 Jamstack 框架

项目结构的[说明](https://gridsome.org/docs/directory-structure/)



![image-20220116135353925](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220116135353925.png)

与传统vue的mount并不完全一致







## yarn

包管理工具





## vuetify

![image-20220116135224033](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220116135224033.png)



## npm install --save-dev

save to dev的`dependencies`

vue项目run dev 的都需要那个dev的args





## export default component





## v-app





## slot

占坑



## gridsome main

```vue
import DefaultLayout from '~/layouts/Default.vue'

export default function (Vue, { router, head, isClient }) {
  // Set default layout as a global component
  Vue.component('Layout', DefaultLayout)
}
```

DefaultLayout 只是相当于别名一样的东西

Layout 这个标签名，则是映射到Default.vue中

main中导入的这个Layout标签是全局使用的



Default.vue

```vue
<template>
  <div class="layout">
    <header class="header">
      <strong>
        <g-link to="/">{{ $static.metadata.siteName }}</g-link>
      </strong>
      <nav class="nav">
        <g-link class="nav__link" to="/">Home</g-link>
        <g-link class="nav__link" to="/about/">About</g-link>
      </nav>
    </header>
    <slot/>
  </div>
</template>
```

`g-link` 是页面跳转的标签

导航跳转时，只有`slot`标签里的内容会发生改变

`/`是跳转到`src/pages/index.vue`

`/about`是跳转到 `src/pages/about.vue`

![image-20220116143715716](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220116143715716.png)





![image-20220116142916017](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220116142916017.png)



Layout 再main中已经设置成全局的一个标签

古不用再export引入



## npm

安装的包会自动更新到package.json的



## export default





