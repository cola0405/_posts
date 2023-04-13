---
title: todolist-demo
date: 2022-01-16 20:44:22
tags:
categories:
---



# 运行

```bash
npm install --save-dev
npm run dev
```





# 笔记

## enter键入

```vue
<input @keyup.enter="addTodo">
```



## component 命名

```vue
<script>
export default {
    name:Todo
}
</script>
```





## 新增项





## 关闭eslint

实在太烦了

进package.json删了，然后



## component引入

```js
import Todo from '@/components/Todo'
```

不用在export中命名

除非你要起别名



## 默认import和export default

```js
import store from './store'
```

淦，一开始表示找不到，我还以为漏装了一个包，结果。。。

`./store`表示的是src下的目录

![image-20220116225345082](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220116225345082.png)



而且，如果目标目录下有index，且没有指定from哪一个js文件

此时，会默认from `index.js`

然后，再index.js中

```js
export {  
     realconsole
}  
```

然后

```js
import realconsole from './xxx'
```

但是，还需要注意export default，这叫默认导出

也就是

```js
export default new Vuex.Store({
  state,
  ...
})
```

此时，要import这个store的话

乱来都行

```js
import hello from './store'
```

（相当于可以外边给名字）





## props

父传子





## computed

函数，返回值





## style scoped

在vue文件中的style标签上，有一个特殊的属性：scoped。 当一个style标签拥有scoped属性时，它的CSS样式就只能作用于当前的组件



## v-model

实时获取值，赋值



## v-bind

v-bind是单向绑定，而v-model 是双向绑定







## 箭头函数

箭头函数表达式更适用于那些本来需要匿名函数的地方

```js
function funcName(params) {
   return params + 2;
 }
funcName(2);
```

可以简洁地表示为

```js
var funcName = (params) => params + 2
funcName(2);
```

如果只有一个参数，可以省略括号: 

```js
params => params + 2
```

如果不需要参数，则

```js
() =>{
  
}
```



如果该箭头函数有不止一条语句，则

```js
(params,...) =>{
  ...
}
```





## 匿名函数

简单声明一个函数

```js
function fn(){
    console.log("hello");
}
```

如果想让它匿名，成为没有名字的function

```js
function (){
    console.log("hello");
}
```

这样是会报错的

需要

```js
(function (){
    console.log("hello");
})
```

现在不会报错，但是改函数也不会被调用

应该再加一个括号

```js
(function (){
    console.log("hello");
})()
```

如果还想要传参

```js
(function (name){
    console.log("hello"+name);
})("cola")
```



应用场景

```js
var sub=document.querySelector("#sub");
sub.onclick=function(){
	alert("hello");
}
```

```js
var obj={
    fn:function(){
        return "hello";
    }
};
```

```js
var fn=function(){
    return "hello"
}
```

```js
setInterval(function(){
    console.log("hello");
},1000);
```

```js
function fn(){
    return function(){
        return "hello";
    }
}
```

