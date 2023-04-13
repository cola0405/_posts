---
title: Vue 跨域
date: 2021-06-07 13:09:21
tags:
categories:
---



找到devServer配置项

其所在位置分两种情况

1.如果使用

```bash
vue init webpack projectName
```

构建vue项目，则再/build/webpack.dev.conf.js中

然后其引用了/config/index中的value

2.如果使用

```
vue create <project-name>
```

```js
	devServer: {
    	port:8081,  // 代理端口
    	host: '0.0.0.0',
        proxy:{
            '/health-post':{
        		target:'http://localhost:8080/',  //目标服务器端口
        		changeOrigin:true,
        		pathRewrite: {
          		'^/health-post': '/health-post'  // 不可省
        }
        }
	}
```



请求成功的url

```
http://localhost:8081/health-post
```

就是vue的端口，而不是目标服务器端口（8080）

真正和服务器交互的是vue的代理