---
title: 汇编-lpcs笔记
date: 2022-03-28 12:56:00
tags:
categories:
---

# Postman

## 上传文件

[demo](https://gitee.com/simple_one1/spring-boot-file-upload-download)

### 前端

添加headers

```
Content-Type : multipart/form-data
```

form-data

```
file : select file
```



### 后端

```java
	@PostMapping("/upload")
    @ResponseBody
    public String upload(@RequestParam("file") MultipartFile file) {
        if (file.isEmpty()) {
            return "上传失败，请选择文件";
        }

        String fileName = file.getOriginalFilename();
        String filePath = "D:\\download\\temp\\";
        File dest = new File(filePath + fileName);
        try {
            file.transferTo(dest);
            System.out.println("上传成功");
            return "上传成功";
        } catch (IOException e) {
            e.printStackTrace();
        }
        return "上传失败！";
    }
```





## 传递数组

![image-20220328111911725](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220328111911725.png)





# 数据库

## 多个数据源

[demo](https://gitee.com/simple_one1/multi-datasource-demo)

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
public class MultiDatasourceDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(MultiDatasourceDemoApplication.class, args);
    }

}
```

别的地方按照demo就行











### sqlite

```
CREATE TABLE user(
name varchar(50)
);
```

```
insert into user(name)values("cola");
```



#### 报错

```
Consider marking one of the beans as @Primary
updating the consumer to accept multiple beans
or using @Qualifier to identify the bean that should be consumed
```

解决：

数据源没有对应配置好



```
Cannot use both: sqlSessionTemplate and sqlSessionFactory together. sqlSessionFactory is ignored.
```



#### lpcs

```sql
CREATE TABLE camera(
	id int AUTO_INCREMENT PRIMARY KEY,
    name varchar(50),
	camera_ip varchar(50)
);
```

```sql
CREATE TABLE screen(
	id int AUTO_INCREMENT PRIMARY KEY,
    name varchar(50),
	screen_id varchar(50)
);
```





# Mysql

## 密码





## 启动和关闭



### Ubuntu

```
service mysql start
```

```
mysqladmin shutdown
```



## Windows

`任务管理器` - `服务` - `重新启动`



## 环境变量

```
C:\Program Files\MySQL\MySQL Server 8.0\bin
```







# Java

## 删除文件

```java
file.delete();
```

Ps：

删除前保证所有inputStream都关闭



## 数据校验+exception handler

```java
import javax.validation.Valid;


	@PostMapping("/program/json/upload")
    @SaCheckLogin
    public R uploadProgramJson(@Valid @RequestBody UploadProgramJsonReq req) throws Exception {
        programService.uploadProgramInfo(req);
        return R.success();
    }
```



```java
import lombok.Data;
import javax.validation.constraints.NotBlank;

@Data
public class UploadProgramJsonReq {
    @NotBlank(message = "节目名字不能为空")
    String programName;

    @NotBlank(message = "节目json不能为空")
    String programJson;
}
```





```java
import org.springframework.web.bind.MethodArgumentNotValidException;


	@ExceptionHandler(value = MethodArgumentNotValidException.class)
    @ResponseBody
    public R validatorHandler(MethodArgumentNotValidException e){
        return R.codeEnum(CodeEnum.fail.code, e.getBindingResult().getFieldError().getDefaultMessage());
    }
```







# docker

## 安装

[教程](https://serverspace.io/support/help/how-to-install-docker-on-ubuntu-18-04-lts/#:~:text=Installing%20Docker%20on%20Ubuntu%2018.04%20Docker%20can%20be,repositories%20or%20install%20it%20from%20Docker%E2%80%99s%20official%20repository.)



## mysql

```
docker run -it --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
```



### 执行sql

使用workbench

不一定要把文件放进去







# Vue

## 镜像

```
npm install --registry=https://registry.npm.taobao.org
```



## npm install 报错

一般是那个包有问题

很大可能是网络原因

```
npm uninstall node-sass
```

然后配置镜像

```
npm config set registry https://registry.npm.taobao.org
```

```
npm config set SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/
```

在安装就没问题了





# 数据库字段

## screen

新增字段：

`设备宽` 

`设备高`



## camera

新增字段：

`型号`

`状态`



## 灯控

`id` `brightness` 





# 文本处理

## 双引号转单引号

`ctrl`+`r`

replace



## 去除换行符

https://uutool.cn/nl-trim-all/







# 问题



## 数据库mysql保存json





## md5计算

demo



## mybatis-plus配置类

demo

```

```







## sql语句含特殊符号

单引号

```xml
	<insert id="insertImageInfo" >
        insert into program_image(image_name, user_id, image_size, md5, content)
        values('${imageInfo.imageName}', ${imageInfo.userId}, ${imageInfo.imageSize}, '${imageInfo.md5}', 			'${imageInfo.content}')
    </insert>
```





## json

转化demo

```java
JSONObject programJson = JSONObject.parseObject(programJsonStr);
```





## 资源请求

模糊匹配映射

demo

