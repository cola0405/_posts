---
title: axois
date: 2021-06-07 11:36:37
tags:
categories:
---



```vue
<script>
export default {
        name: "Register",
        data(){
            return{
                messageInfo:"",
            }
        },
        methods:{
            register(){
                axios.post('/register', {
                    "username":this.username,
                    "password":this.password,
                    "password1":this.password,
                }).then((res)=>{
                    console.log(res)
                    this.messageInfo=res.data.message
                })
            }
        },
    }
</script>	
```

#### Post指定form-data

```vue
<script>
	axios({
        method: 'post',
        url: 'http://localhost:8080/health-post',
        headers: {
          'Content-Type': 'multipart/form-data'
        },
        withCredentials: true,
        data: formData
      }).then((res) => {
      })
</script>
```



Spring Boot 接收数据

```java
    @RequestMapping("/health-post")
    public Object healthPost(@RequestParam Map<String,String> params){
        for (String key : params.keySet()){
            System.out.println(key+"is"+params.get(key));
        }
        return "Good";
    }
```



---

#### axios headers

```js
Axios.request({
     url: "http://example.com",
     method: "get",
     headers:{
         Cookie: "cookie1=value; cookie2=value; cookie3=value;"
     } 
})
```



axios统一添加headers

在main.js

```js
import axios from 'axios'
axios.interceptors.request.use(
  config => {
    config.headers.common = {
      'xxxxxxxxxx': 'oooooooooooooo'
    }
    return config
  },
  err => {})
```

---

```js
	axios({
        withCredentials: true,
        maxRedirects: 0,
        method: 'get',
        url: '/admin/getExcel',
        timeout: 4000
      }).then((res) => {
        console.log(res)
      }, ErrorEvent => {
        this.$message('请求数据失败')
      })
```

---

#### axois post 列表 json Array

前端

```js
	axios({
        withCredentials: true,
        method: 'post',
        url: '/admin/getExcel',
        headers: {
          'Content-Type': 'application/json'
        },
        timeout: 4000,
        data: this.tableData
      }).then((res) => {
        console.log(res)
      }, ErrorEvent => {
        this.$message('请求数据失败')
      })
```

后端 Spring Boot

```java
    @RequestMapping("/admin/getExcel")
    @ResponseBody
    public Object getExcel(@RequestBody JSONArray re) {
        System.out.println(re);
        return "ok";
    }
```

