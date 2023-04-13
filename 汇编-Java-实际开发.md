---
title: 汇编-Java-实际开发
date: 2022-04-19 11:14:39
tags:
categories:
---



# 金额计算

金额计算不能用浮点数！！！

看一个例子

```java
System.out.println(0.03-0.02);
```

输出: 0.009999999999999998



解决：BigDecimal

```java
BigDecimal a = new BigDecimal("0.03");
BigDecimal b = new BigDecimal("0.02");
System.out.println(a.subtract(b));
```



# 变量



## 变量名

detail

brief

encoder

common

verify

quantity

nickname

acquired

invaliadate



group

member - 会员







## 缩写

oms - Order Management System 订单管理系统

ums - User Management System 用户管理系统

mbg - Mybatis Generator

dto - Data Transfer Object 数据传输对象



tel - 联系方式

intro - 介绍

prod - 产品

no - 编号









## 传参类型

Integer一定程度上可以避免SQL注入





## 路径命名

允许`/delete/sub-account`



## 变量命名

`module_task` 和 `task_module`的主要区别在于：

一个是有利于国人阅读，一个是外国人的英语习惯





## boolean默认值

![image-20220520100957468](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220520100957468.png)

![image-20220520101010033](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220520101010033.png)





# 编码风格

如果项目还是“中文”项目

那还是需要多加一些注释的

不能照搬国外程序员的编程思路



## 直接返回

```java
    public List<Department> getDepartmentList() {
        Integer parentId = Integer.valueOf((String)StpUtil.getLoginId());
        Integer companyId = userDao.getCompanyId(parentId);
        return departmentDao.getDepartmentList(companyId);
    }
```

函数名说清楚了，如果不需要额外的检查，直接返回就行





## 代码不要太长

![image-20220424153719619](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220424153719619.png)

像阅读理解一样，离谱



## 是否使用枚举类

![image-20220424154027347](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220424154027347.png)

别了。。

直接定义常量吧 







## 注释完备

反作用于恢复数据库！！！

命名一致也是！！太有用了







## 方法命名

```java
// 如果说这个serivce不复杂的话，确实省略宾语才是上上解
groupRepository.findByGroupName(groupName);
```

```java
listPermission()
```

```java
saveOrUpdate()
```



## 注释

![image-20220520164606383](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220520164606383.png)



![image-20220520164823926](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220520164823926.png)



![image-20220520165450802](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220520165450802.png)



# 架构设计

## controller需不需要业务逻辑

好处：

流程清晰，方便代码阅读，方便再次开发

各步骤划分清晰

todo放在controller也容易看



缺点：

流程改变的话，还得改动controller的代码



从另外一个方面来讲

service设计来就是定接口的

那么我在controller里定流程也是合理的！





这里还涉及到另外一个问题

controller层做前后置操作的话，@Transational放在哪

只能放到controller了

放各个service的话，已经进行的service数据库操作无法回滚





## 异常捕获

切面那里验证用户是否登录

一处捕获异常就行，可以全部相关接口获益



# 性能

## @Transational别乱用

影响性能





## 尽量减少HTTP请求







# 数据库

## 批量插入

mybatis

```sql
```

## id

重要字段id搞长 





## 备份

别的工程师改过数据库结构

数据库没有及时备份

sql语句是旧的

结构都不一样:)



## create_time和update_time

默认值为CURRENT_TIMESTAMP



设置updatetime列属性ON UPDATE CURRENT_TIMESTAMP

![image-20220428162452997](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220428162452997.png)



Ps：

得把0填上，不然会出错

![image-20220428162356399](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220428162356399.png)





## sql语句-查询字段

写清楚，别*

视图不是用来*的





## 为什么使用Integer

attempted to return null from a method with a primitive return type (int)

用Integer就不会报这个错误



## 批量插入

```sql
    <insert id="batchInsert">
        INSERT INTO user_permission_relation(user_id,permission_id) VALUES
        <foreach collection="batch" item="item" index="index" separator=",">
            (#{item.userId},#{item.permissionId})
        </foreach>
    </insert>
```





## 时间带T

```java
@JsonFormat(timezone = "GMT+8",pattern="yyyy-MM-dd HH:mm:ss")
```



## 选取null的字段

一定要用is，而不能用=







## 批量操作时，一般需要回滚的







# 传参

## 不传递非空字段

```java
@JsonInclude(JsonInclude.Include.NON_NULL)
```

加在实体类上面，或者具体成员变量上都行

配合数据库的view视图，就不用另外新建实体类了





## 从request中获取json数据

```java
    public String getJsonFromRequest(HttpServletRequest req){
        BufferedReader streamReader;
        StringBuilder stringBuilder = new StringBuilder();
        try {
            streamReader = new BufferedReader( new InputStreamReader(req.getInputStream(), "UTF-8"));
            String str;
            while (true) {
                str = streamReader.readLine();
                if (str==null) {
                    break;
                }
                stringBuilder.append(str);
            }
        }
        catch (IOException e) {
            e.printStackTrace();
        }
        return stringBuilder.toString();
    }
```

报错：在进入AOP前，spring框架在使用 对象类型转换器(converter)时

已经使用过一次body了（获取body是以流的形式，且由此可知，这个类型转换是优先于AOP切面的）

所以在AOP切面处理时，想获取body体数据，发生"stream closed"异常



解决：

从joinPoint中获取

```java
System.out.println(JSON.toJSONString(joinPoint.getArgs()[0]));
```







这里有另外一个问题，没有json数据的该怎么处理

或者上传的接口该怎么处理





## Requestbody 为空

像page size这样有默认值的参数

如果前端不穿json过来

甚至Requestbody对应的对象都不会被实例化

也就是如果想用getter

都是报空指针的异常



解决：

if 判断 request 是否为空





## 仅传需要更新的数据？





## decimal

对应java是 `BigDecimal`

构造`BigDecimal` 最好使用字符串

直接使用浮点数的话会有误差（莫名其妙多很多数位）

还有，千万注意！

小数位不要设置为0





# 日志

[经验帖](https://github.com/EZLippi/practical-programming-books/blob/master/src/logging.md)



## 没有返回值

第一种情况：

没有return

解决：

在doAround里增加return

```java
result = joinPoint.proceed();
return result;
```



## 记录异常的日志时，前端没有收到返回值

第二种情况：

![image-20220509121750235](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220509121750235.png)

执行业务逻辑时抛出了异常

没有把返回结果赋值给result

导致前端收到的result是空的null

解决：

在catch里额外写逻辑



## 做切面日志时的异常捕获

使用try-catch的话



在方法后加 `throw Throwable` 的话，会把异常捕获交给ExceptionController来完成

但是这样一来就没办法做日志储存了



## 返回结果类不一样时，异常处理该怎么设计



```java
        try{
            buildWebLogByRequest(webLog);
        }catch (Throwable t){
            BusinessException e = (BusinessException) t;
            System.out.println(method.getReturnType().getName());
            if(method.getReturnType() == R.class){
                result = R.codeEnum(CodeEnum.FAILED).setCode(e.getCode()).setMessage(e.getMessage());
            }else{
                result = RQ.codeEnum(CodeEnum.FAILED).setCode(e.getCode()).setMessage(e.getMessage());
            }
            return result;
        }
```





## json请求参数与文件的区分



json和文件上传都是在inputstream中获取数据

解决：

利用请求头中的Content-Type来做区别

实在不行，让开发者在日志注解上表参数类型



然后还需另外在传参时做try-catch

防止系统异常，而返回“参数错误”

# 配置文件

命令行获取ip



# 问题场景

## 省份的数据库设计

![image-20220506181541967](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220506181541967.png)







# 问题

## 插入和修改哪个快





## 只查一个数据有必要联表吗



## 往同部门调，默许还是提示





## 日志时间和实际图片上传的时间不一致

