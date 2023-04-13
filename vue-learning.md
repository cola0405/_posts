---
title: vue learning
date: 2023-02-23 10:13:34
tags:
categories:
---





# 介绍

所谓 ViewModel 即为保持状态和视图的同步  

可以将任意封装好的代码注册成标签  





一个 Vue 实例相当于一个 MVVM 模式中的 ViewModel 

![image-20230223182402911](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230223182402911.png)



Vue.js 作为数据驱动视图的框架，我们首先要知道的就是如何将数据在视图中展示出来

传统的 Web 项目中，这一过程往往是通过后端模板引擎来进行数据和视图的渲染

例如 PHP的 smarty， Java 的 velocity 和 freemarker

但这样导致的情况是前后端语法会交杂在一起，前端 HTML 文件中需要包含后端模板引擎的语法

而且渲染完成后如果需要再次修改视图，就只能通过获取 DOM 的方法进行修改，且手动维持数据和视图的一致。  



Vue.js 的核心是一个响应式的数据绑定系统

建立绑定后， DOM 将和数据保持同步，这样就无需手动维护 DOM

使代码能够更加简洁易懂、提升效率









## 版本支持

Vue.js 也抛弃了对 IE8 的支持

在移动端支持到 Android 4.2+ 和 iOS 7+。





# axios



## GET



`util/axios.js`

```js
import axios from 'axios'

let service = axios.create({
    baseURL:'http://localhost:8080'
})

export default service
```



`api/problem.js`

```js
import service from '@/util/axios'


export function getProblemList(){
    return service.request({
        url: '/problem/getList',
        method:'get'
    })
}
```



`App.vue`

```js
  beforeMount() {
    getProblemList().then((res) => {
      console.log(res)
    })
    // init table data
    this.resetTableData()

    // init page 1
    this.updatePage(1)
  }
```







## POST

`api/problem.js`

```js
export function newProblem(formData){
    return axios.request({
        url: 'api/problem/new',
        method:'post',
        data: formData
    })
}
```







# command



## @

```
# @表示安装最新版
npm install -g @vue/cli
```





## npx



npx 是 npm5.2.0版本新增的一个工具包，定义为npm包的执行者，相比 npm，npx 会自动安装依赖包并执行某个命令。







## npm指定版本

```
npm uninstall -g @vue/cli
```



```
npm install vue-cli@2.9.6 （指定版本安装【指定版本为3.0以下版本】）
npm install -g @vue/cli@3.11.0（指定版本安装【指定版本为3.0以上版本】）
```



```
npm install -g @vue/cli@4.4
```







# component 组件





## $emit

在实例本身上触发事件。  





## $dispatch  

派发事件，事件沿着父链冒泡，并且在第一次触发回调之后自动停止冒泡，除非触发函
数明确返回 true，才会继续向上冒泡。  









## 分页算法

```js
	updatePage : function (targetPage){
      this.showData = []

      for(let i=(targetPage-1)*this.pageSize;i<this.tableData.length;i++){
        this.showData.push(this.tableData[i]);
        if(this.showData.length===this.pageSize) break;
      }
    }
```





## back header

```html
<el-page-header @back="goBack" content="题目详情"></el-page-header>
```

```js
  methods: {
    goBack(){
      this.$router.back()
    }
  }
```







## 交集

```js
		for(let i=0;i<this.originData.length;i++){
          let curTypes = this.originData[i].type
          
          let intersect = curTypes.filter(x => problemTypes.has(x))
          
          if(intersect.length === problemTypes.size){
            this.tableData.push(this.originData[i]);
          }
        }
```













## props

```html
<HelloWorld msg="Welcome to Your Vue.js App"/>
```

```vue
<h1>{{ msg }}</h1>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
```









## 修改页码

`:` 是为了取值

`current-page` 当前页数

`.sync` 表示同步

```html
	<el-pagination
          @current-change="updatePage"
          :current-page.sync="curPage"
          background
          layout="prev, pager, next"
          :page-size="pageSize"
          :total="this.tableData.length">
      </el-pagination>
```

```js
this.curPage = 1
```







## ref

组件引用





## 组件间通信

1） \$parent: 父组件实例。
2） \$children: 包含所有子组件实例。
3） $root: 组件所在的根实例。  



### 子传父

子 (ProblemFilter)

```js
// 方法名、数据
this.$emit('newFilter', this.problemTypes)
```



父

```html
<ProblemFilter @newFilter="doFilter"></ProblemFilter>
```

```js
doFilter : function (problemTypes){}
```





## 父传子

父

```html
<TagManageDialog v-bind:tagList="tagList"></TagManageDialog>
```



子

```js
props : {
    tagList:{
      type: Array,
      required:true
    }
}
```

```js
console.log(this.tagList)
```





Ps: 子组件中修改值，会影响父组件









# 第三方 Component



## md编辑器

https://github.com/hinesboy/mavonEditor

```
npm install mavon-editor --save
```



```html
		<mavon-editor
              placeholder="请输入题目内容..."
              :toolbars="toolbars"
              v-model="form.content"/>
        </el-form-item>
```

```js
  data() {
    return {
      form: {
        name: '',
        difficulty: '',
        content: ''
      },
      toolbars: {
        bold: false, // 粗体
        italic: false, // 斜体
        header: false, // 标题
        underline: false, // 下划线
        strikethrough: false, // 中划线
        mark: false, // 标记
        superscript: false, // 上角标
        subscript: false, // 下角标
        quote: false, // 引用
        ol: false, // 有序列表
        ul: false, // 无序列表
        link: false, // 链接
        imagelink: true, // 图片链接
        code: true, // code
        table: false, // 表格
        fullscreen: false, // 全屏编辑
        readmodel: false, // 沉浸式阅读
        htmlcode: false, // 展示html源码
        help: false, // 帮助
        /* 1.3.5 */
        undo: false, // 上一步
        redo: false, // 下一步
        trash: false, // 清空
        save: false, // 保存（触发events中的save事件）
        navigation: false, // 导航目录
        alignleft: false, // 左对齐
        aligncenter: false, // 居中
        alignright: false, // 右对齐
        /* 2.2.1 */
        subfield: true, // 单双栏模式
        preview: true // 预览
      }
    }
  }
```





### md 预览

```html
<mavon-editor
    :toolbars="false"
    :subfield="false"
    default-open="preview"
    v-model="this.content"></mavon-editor>
```







# css

```css
.el-main{
  background-image: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);
}
```



```css
.el-container{
  height: 100%;
}
```



```css
<el-aside width="150px"></el-aside>
```









# Data



## computed

在项目开发中，我们展示的数据往往需要经过一些处理。除了在模板中绑定表达式或者
利用过滤器外， Vue.js 还提供了计算属性这种方法，避免在模板中加入过重的业务逻辑，保证
模板的结构清晰和可维护性。  



```js
var vm = new Vue({
	el : '#app,
	data: {
		firstName : 'Gavin'，
		lastName: 'CLY'
	}
	computed : {
		fullName : function() {
		// this 指向 vm 实例
			return this.firstName + ' ' + this.lastName
		}
	}
	});
<p>{{ firstName }}</p> // Gavin
<p>{{ lastName }}</p> // CLY
<p>{{ fullName }}</p> // Gavin CLY
```





## data属性

vue实例中的data属性既可以是一个对象，也可以是一个函数

**组件中定义data属性，只能是一个函数**

**vue组件可能会有很多个实例，采用函数返回一个全新data形式，使每个实例对象的数据不会受到其他实例对象数据的污染**



```js
export default {
  name: 'App',
  data: function (){
    return {
      message: 'hello vue.js'
    }
  }
}
```





## this

In a method, this refers to the component that the method is attached to.  



```js
data: {
	numbers: [-5, 0, 2, -1, 1, 0.5]
},
methods: {
	getPositiveNumbers() {
	return this.numbers;
}
```





## :

```html
<el-input type="textarea" :autosize="true"></el-input>
```

true 属性前加 :





## get inside

```js
      for (let i=0; i<this.tagList.length;i++){
        if (tags.find((tag) => tag.id === this.tagList[i].id)){
            this.form.tags.push(this.tagList[i].name)
        }
      }
```









# Directive 指令



## v-if 与 v-show



`v-if`

true -- 加载到DOM中（能在html代码中看到）

false -- 不加载到DOM中

```vue
<div v-if="true">one</div>
<div v-if="false">two</div>
```



`v-show`

true -- 显示

false -- 不显示





###  v-if 更新不及时

```
// 强制刷新
this.$forceUpdate()
```









## v-else

```html
<div v-if="inner">inner</div>
<div v-else>not inner</div>
```







## v-bind

Mustache 语法不能作用在 HTML attribute 上，遇到这种情况应该使用 `v-bind` 指令：

```html
<div v-bind:id="dynamicId"></div>
```





缩写

```html
<a :href="url">...</a>
```

```html
<a :[key]="url"> ... </a>
```



Ps: 这是one-way data binding  

仅取决于内存中的dynamicId





## v-model

双向绑定 two-way data binding  

```html
    <input v-model="content">
    <p> {{content}}</p>
```

```js
  data: function (){
    return {
      names: ["Cola", "Amy", "Coco"],
      content : "Cola"
    }
  }
```











## v-on



```html
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```



```html
<a v-on:click="say"> hello </a>
```



```js
  methods :{
    say : function (){
      alert("helloooooo")
    }
  }
```







## v-for

```html
      <el-table-column
          align="center"
          prop="tags"
          label="标签">
        <template slot-scope="scope">
          <el-tag v-for="tag in scope.row.tags" :key="tag">
            {{ tag }}
          </el-tag>
        </template>
      </el-table-column>
```



### iteration index

```html
<template v-for="(tag, i) in tagList">
```





### key

有唯一标识就行

```html
      <template v-for="(tag, i) in tagList">
          <el-input
              class="input-new-tag"
              :key="i"
              :ref="'input'+i"
              v-if="editTag[i]"
              v-model="tagList[i]"
              size="small"></el-input>
      </template>
```





### 动态ref

```html
		<el-input
          class="input-new-tag"
          :key="i"
          :ref="'input'+i"
          v-if="editTag[i]"
          v-model="tagList[i]"
          size="small"></el-input>
```

Ps：必须在nextTick中才能正常访问$refs

```js
      this.$nextTick(() => {
        this.$refs['input'+i][0].$refs.input.focus()
      });
```







# concept





## DOM

Document Object Model



## hook function

和回调函数一个意思





## JSX

[JSX](https://facebook.github.io/jsx/) 是 JavaScript 的一个类似 XML 的扩展，有了它，我们可以用以下的方式来书写代码：

```js
render (h) {
	return (
		<div>
			<h1 on-click={this.handleClick}>Hello from JSX</h1>
			<p> Hello World </p>
		</div>
	)
}
```





## MVVM

Model-View View-Model  

which is based on the concept of two-way binding data to components and views  







## 响应式编程

保持状态和视图的同步







## vm

ViewModel 



## vue2 与 vue3

对于 Vue 3，你应该使用 npm 上可用的 Vue CLI v4.5 作为 @vue/cli。









# flex

Ps：不要用`element-ui`自带的flex

外面套一个`div`来操作

```html
<div id="tags">
    <el-checkbox
       v-for="name in tagList"
       :key="name"
       :label="name"
       border
       size="medium"
       @change="updateProblems"></el-checkbox>
</div>
```



```css
#tags{
  display: flex;
  flex-wrap: wrap;
}
```

![image-20230312110826227](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230312110826227.png)









# Javascript



## find

```js
      for (let i=0; i<this.tagList.length;i++){
        if (tags.find((tag) => tag.id === this.tagList[i].id)){
            this.selectedTags.push(this.tagList[i].name)
        }
      }
```







# main.js





## mount()







对于每个应用实例，`mount()` 仅能调用一次。



## 全局变量

```js
new Vue({
  render: h => h(App),
  data:{
    message: 'hello vue.js'
  }
}).$mount('#app')
```









# method

```js
	cur_change : function (){
      this.update_page()
    },
    update_page : function (){
      alert(this.pageSize)
    }
```











# 目录结构

```
├── build                      // 构建相关  
├── config                     // 配置相关
├── src                        // 源代码
│   ├── api                    // 所有请求
│   ├── assets                 // 主题 字体等静态资源
│   ├── components             // 全局公用组件
│   ├── directive              // 全局指令
│   ├── filtres                // 全局 filter
│   ├── icons                  // 项目所有 svg icons
│   ├── lang                   // 国际化 language
│   ├── mock                   // 项目mock 模拟数据
│   ├── router                 // 路由
│   ├── store                  // 全局 store管理
│   ├── styles                 // 全局样式
│   ├── utils                  // 全局公用方法
│   ├── vendor                 // 公用vendor
│   ├── views                   // view
│   ├── App.vue                // 入口页面
│   ├── main.js                // 入口 加载组件 初始化等
│   └── permission.js          // 权限管理
├── static                     // 第三方不打包资源
│   └── Tinymce                // 富文本
├── .babelrc                   // babel-loader 配置
├── eslintrc.js                // eslint 配置项
├── .gitignore                 // git 忽略项
├── favicon.ico                // favicon图标
├── index.html                 // html模板
└── package.json               // package.json

```





# proxy 端口

`vue.config.js`

```js
module.exports = {
    devServer: {
        port: 8081,
        host: '0.0.0.0',
        proxy: {
            '/api': {
                // url 这里会做拼接
                target: 'http://localhost:8080/',  //目标服务器端口
                changeOrigin: true,
                pathRewrite: {	  // 在proxy处重写url
                    '^/api': ''  // 表示删除url中的api
                }
            }
        }
    }
}
```

之所以要加 `api`

原因在于，我们只希望发往后端的请求才走proxy

对于前端的页面跳转，我们不需要proxy



`problem.js`

```js
export function getProblemList(){
    return axios.request({
        url: 'api/problem/getList',
        method:'get'
    })
}
```









# 权限验证

前端验证还是后端验证？

若后端验证，则每增加一个页面，后端就要动一下

若前端验证，则只在前端动就行

![image-20220103203722855](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220103203722855.png)





# 生命周期



```js
export default {
    created() {
        ...
    }
}
```

![img](https://v2.cn.vuejs.org/images/lifecycle.png)





# Table



## Filter 筛选



如果不用分页，则直接用`Table-column Attributes` 的`filter-method` 即可筛选

```
如果是多选的筛选项，对每一条数据会执行多次，任意一次返回 true 就会显示
```



如果同时还要分页，则是要用`Table Events` 的`filter-change` 

```html
		<el-table
          :data="showData"
          @filter-change="doDifficultyFilter"
          style="width: 100%">
        <el-table-column
            prop="id"
            label="ID">
        </el-table-column>
        <el-table-column
            align="center"
            prop="name"
            label="题目名称">
        </el-table-column>
        <el-table-column
            id="difficulty"
            :column-key="'difficulty'"
            :filters="[{ text:'简单', value: '简单'}, { text:'中等', value: '中等'}, { text:'困难', value: '困难'}]"
            align="right"
            prop="difficulty"
            label="难度">
        </el-table-column>
      </el-table>
```



要筛选的那一列

需要配置`:column-key` 和`filters`

```
当表格的筛选条件发生变化的时候会触发该事件
参数的值是一个对象，对象的 key 是 column 的 columnKey，对应的 value 为用户选择的筛选条件的数组
```



```html
		<el-table-column
            id="difficulty"
            :column-key="'difficulty'"
            :filters="[{ text:'简单', value: '简单'}, { text:'中等', value: '中等'}, { text:'困难', value: '困难'}]"
            align="right"
            prop="difficulty"
            label="难度">
        </el-table-column>
```



```js
    doDifficultyFilter : function (columns){
      let difficultySet = new Set(columns['difficulty'])

      // 无筛选
      if(difficultySet.size === 0){
        this.resetTableData()
      }else{
        this.tableData = []

        // 符合difficultySet内的problems都放入tableData
        for(let i=0;i<this.originData.length;i++){
          let curDifficulty = this.originData[i].difficulty
          if(difficultySet.has(curDifficulty)){
            this.tableData.push(this.originData[i]);
          }
        }
      }
	  // 更新分页数据，翻回第一页
      this.adjustPagination()
    }
```





## Page 分页







# Tag

## template

```html
      <el-table-column
          align="center"
          prop="tags"
          label="标签">
        <template slot-scope="scope">
          <el-tag v-for="tag in scope.row.tags" :key="tag">
            {{ tag }}
          </el-tag>
        </template>
      </el-table-column>
```







# vue-router



## 版本

```bash
npm install vue-router -s
```

```bash
# 对应上vue 2.6
npm install vue-router@3.5.2
```





main.js

```js
import VueRouter from 'vue-router';
Vue.use(VueRouter);
```







## router-view



### 局部router-view

`router.js`

```js
import NewProblem from "@/components/NewProblem.vue";
import Main from "@/components/Main.vue";
import ProblemList from "@/components/ProblemList.vue";

const routers = [
    {
        path: '/',
        component: Main,
        children: [
            {
                path: 'problem/list',
                component: ProblemList
            },
            {
                path: 'new/problem',
                component: NewProblem
            }
        ]
    }

]
export default routers
```

里面的 `children` 只会匹配嵌套在内层的 `router-view`







### 页面跳转

```js
  methods : {
    toProblemList : function (){
      this.$router.push('/')
    },
    toNewProblem : function (){
      this.$router.push('/new/problem')
    }
  }
```

Ps: url最前面的`/`不可省





### 默认页面

`router.js`

```js
import NewProblem from "@/components/NewProblem.vue";
import Main from "@/components/Main.vue";
import ProblemList from "@/components/ProblemList.vue";

const routers = [
    {
        path: '/',
        component: Main,
        children: [
            {
                path: '',
                component: ProblemList
            },
            {
                path: 'new/problem',
                component: NewProblem
            }
        ]
    }

]
export default routers
```

`problemList` 则是默认界面





### 共用表单



使用 `created`

```js
  created() {
    if(this.$route.query.type === 'update'){
      this.form.name = this.$route.query.problemData.name
      this.form.difficulty = this.$route.query.problemData.difficulty;
  }
```









### 跳转页面传递数据

```js
    editProblem(id){
      this.$router.push({
        path: '/new/problem',
        query:{
          id : id
        }
      })
    },
```

取数据

```js
  beforeCreate() {
    console.log(this.$route.query)
  }
```





## 重复点击路由 报错

`main.js`

```js
import VueRouter from 'vue-router';

const originalPush = VueRouter.prototype.push
VueRouter.prototype.push = function push(location) {
  return originalPush.call(this, location).catch(err => err)
}
```









# Webpack

官方的脚手架生成工具 `vue-cli`

`vue-cli` 总共提供了 5 种脚手架   

`webpack`、`webpack-simple  `、`browerify  `、`browerify-simple  `、`simple  `



```
vue init webpack myproject
```











# bug

## 编辑进去之后没办法新建





## mk down editor 报错
