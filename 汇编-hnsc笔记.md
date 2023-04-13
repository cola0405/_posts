---
title: 汇编-hnsc笔记
date: 2022-01-04 15:38:22
tags:
categories:
---

# IntelliJ

## intellij 快捷键

```bash
command + delete  // 删除当前行
command + ,  // 设置
command + up + a // Find Action
run dashboard // 一键同时跑多个应用

```





## intellij 插件

```bash
Code Glance  // 代码预览
Free Mybatis plugin  // mapper生成，跳转
Rainbow Brackets // 彩色括号
```





## JDK16

删啦！！！！嘛问题都没有了





## 版本信息

版本信息在pom中都有





## Spring Boot 版本

去这个网站https://mvnrepository.com/search?q=spring-boot-starter，找到自己想要的spring-boot-starter版本，复制下来，替换到父版本下。



## maven 远程仓库

```bash
https://start.aliyun.com
```

## 激活

```
-javaagent:/Users/cola/software/ja-netfilter/ja-netfilter.jar
```





# Java





## 鉴权

sa-token

[demo](https://gitee.com/simple_one1/sa-token-demo)

[官方文档](https://sa-token.dev33.cn/doc/index.html#/use/jur-auth)





## 注释

Setting - Editor - Live Templetes

建一个comment组（右边的 + ，Templates group）

然后在组里加head和ctr

（之后，输入head，然后tab，注释就出来了）

head :

```java
/**
 * @author Cola
 * @description 
 * @date $date$
 * @email 1020151695@qq.com
 */
```

ctr :

```java
/**
 * @description 查看面试邀请列表
 * @author cola
 * @url /interview/inviteList
 * @method GET
 */
```

然后这里的 $date$

还需要"Edit variables"

然后 "define" 里选择Java

（表示应用该快捷注释在Java文件中）



## spring boot web

莫名其妙响应不了请求

莫名其妙启动不了

问题多半出在pom里

```xml
			 <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
```

有了这个就不需要原始的starter了

也不需要额外的spring-web（不然web应用跑都跑不动）







## Spring boot定时任务

[demo](https://gitee.com/simple_one1/spring-boot-schedule-demo)



## log 导致应用启动失败

（找找错误提示）



## swagger



https://blog.csdn.net/zhangcongyi420/article/details/119151683





## knife4j



## 封装自己的Request对象

```java
@ApiOperation("查看面试邀请列表")
@GetMapping("/inviteList")
@ResponseBody
public RQL getInterviewInviteList(GetInterviewInviteListRequest request, @NotBlank(message = "token未找到") @RequestHeader("token") String token) {
    List<InterviewItemResp> respList=interviewService.getInterviewInviteList(request.getPositionId(),request.getPage(),request.getSize(),token);
    return RQL.codeEnum(CodeEnum.SUCCESS).putData(respList);
}
```

可以设置默认值

```java
@Data
public class GetInterviewInviteListRequest {
    private Integer page = 1;

    private Integer size = 10;

    private Long positionId;
}
```



## 分页

PageHelper

```xml
				<dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper-spring-boot-starter</artifactId>
            <version>1.2.13</version>
        </dependency>
```



只有紧跟在`PageHelper.startPage`方法后的**第一个**Mybatis的**查询（Select）**方法会被分页。

```java
PageHelper.startPage(page,size);
List<CompInterview> compInterviewList = compInterviewMapper.selectAllComInterviewByPositionId(positionId);
```



```java
	@Select("select * from comp_interview where position_id=#{positionId}")
    List<CompInterview> selectAllComInterviewByPositionId(@Param("positionId") Long positionId);
```





## token

```bash
{"ret":40001,"message":"header缺失:token"}
```

解决：

从用户登录成功那的“返回示例”那拿的（没过期）

Postman 在headers中添加token

```bash
XLK5CVhOlFKlgjGwvXBe21HfAmQL8qftEbHSBVvn3axD1jJaiMbdOXwlGaU1FqIBNdDUa44qWWLfwERogBEKllxmjcVMAY6kI6MvXioTZ8Rc6UySDtpb8X0PKzJ8JnBb
```

结果：

```json
{
    "ret": 200,
    "message": "成功",
    "data": []
}
```





## 后端拿token有什么用

sa-token 解析token

```java
        if (SaTempUtil.parseToken(token, Long.class) != null) {
            uid = SaTempUtil.parseToken(token, Long.class);
        }else if (StpUtil.getLoginId() != null) {
            uid = Long.parseLong(StpUtil.getLoginId().toString());
        }
```





## post请求传参

post请求一般不用form-data（显式）

而是通过json形式

![](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106113743600.png)

然后后端

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class InterviewReinviteRequest {

    @NotNull(message = "面试id不能为空")
    private Long interviewId;
}
```

```java
public RQL interviewReInvite(@Valid @RequestBody InterviewReinviteRequest interviewReinviteRequest){
  ...
}
```

拿post里的数据需要封装request类



## 参数命名

表示消息的未读状态

我用的是

```java
Integer messageStatus;
```

原因是考虑到以后可能会有 “已读未回” 消息的情况

为了可扩展性吧

牺牲了可读性

```java
Boolean unRead;
```







## @Service 加在哪

Impl







## total

是本应返回的当前用户的全部信息的总数

而不是传到前端的信息数



## ArrayList.sort()

最终还是在sql语句中进行逆序

```sql
... order by time dec
```







## LocalDateTime

无时区，更复合心智。



## yyyy-MM-dd

因为YYYY是week-based-year，表示：当天所在的周属于的年份，一周从周日开始，周六结束，只要本周跨年，那么这周就算入下一年。

正确的应该是：

```bash
yyyy-MM-dd
```



## LocalDateTime 做request里的参数

```java
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss",timezone = "GMT+8")
    private LocalDateTime interviewTime;
```



## 应用启动接口

![image-20220114110941196](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220114110941196.png)





## pojo是什么

Plain Ordinary Java Object

可以把POJO作为支持业务逻辑的协助类



## 不用指定parametertype

```xml
    <insert id="addMessage">
        insert into user_message values(null,#{userMessage.receiverId},#{userMessage.senderId},#{userMessage.title},#{userMessage.content},#{userMessage.isValid},now(),#{userMessage.readed},null)
    </insert>
```



## 请求命名

```html
http://localhost:9989/company/get/interviewing/list
```





## 接口里default 关键字

接口里的



## 怎么抛异常

```java
throws new Exception();
```



## enum无法继承类

但还是可以实现接口

然后接口中用defaut 方法

就可以相当于继承类了



## 可变参数

```java
xxx(Object... strs){
  for(String str : strs){
  	System.out.println(str);
  }
}
```



## controller层

request放在controller层

放controller包



## util不够多





## JWT

Json web token





## 添加cookie

```java
		@RequestMapping(value = "/setCookies",method = RequestMethod.GET)
    public  String setCookies(HttpServletResponse response){
        //HttpServerletRequest 装请求信息类
        //HttpServerletRespionse 装相应信息的类
        Cookie cookie=new Cookie("sessionId","CookieTestInfo");
        response.addCookie(cookie);
        return "添加cookies信息成功";
    }

```





# git

## git修改comment

修改最后一次的提交

```bash
git commit --amend
```

```bash
git push --force
```



## push代码前

沿着流程走一遍，看哪里还存在注释等的问题

## git 取消commit

```bash
git reset --soft HEAD^

# --hard 表示commit和修改的代码都回退到上一个版本
# --soft 只是撤销commit
```



## 我拉下来跑一遍

![image-20220112164200687](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220112164200687.png)



## 每次写代码之前我都会pull





## push 到指定分支

```bash
git push origin dev:test
```



## gitignore不生效





## stable版本的分支

版本管理





# 系统设计



## 站内消息的内容怎么存

![image-20220110100928854](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220110100928854.png)



content 存json

```json
{
    "username": "cola",
    "companyName": "n公司",
    "positionName": "JAVA高级开发工程师",
    "interviewTime": "2022-01-22 15:00:00",
    "addr": "郑州市龙子湖金水区",
    "contact": "HRBP先生",
    "phone":"13012341234",
    "companyInfoPage":"https://www.baidu.com/"
}
```

再加一个字段template，表示不同类型的消息

传html代码真不现实。。





## 该接口面向的用户是谁

是单单普通用户

还是这个系统的全部用户，包括企业用户、教培机构、管理员



## 多人用一个账户正常吗

按正常逻辑，这怎么可以呢。。。

但在hnsc里是正常的，公司里，一个账号多个人用



## 多端

保证信息显示准确

切换页面时就要重新获取一次用户信息



## 分开的请求

一个功能分成两个接口的弊端

A请求成功了，B请求没成功，那gg了

尽量不分开来，一个接口完成一个功能



## 不信任前端

重要数据，我们必须从数据库拿

而不是让前端传回来用

前端主要要传的就只有要求和凭证



## 兼容性

长期项目的话，兼容性应该放在更前一点

涉及到政府的话，他们的机器各种各样的机型

IE。。。

2.5.x vue 老，是可以兼容到IE10，但是更老的就不行了



## 封装发送消息的工具类

尽可能把收集数据的过程也集成到工具类里来

让使用者用起来简单





## UI图

别自己想！！！

都看看UI图

这些UI图在制作之初，都是经过思考的

而且是产品经理的意思，相当于官方文档

（可能有错误，但是）



## 所以这就是Java继承特性的有用之处吗！！！

邀请和重新邀请

不同功能，但是字段特别相似



## 对于不同种类的消息

jsonstring存数据

那么，一张表就够了



## 空间换性能

多存个字段就多存个字段

查询更麻烦



## 为什么不能信任前端

账号被盗，hacker拿了token乱来

那完了







# 代码习惯

## 取数据都放在前边





## 插入数据失败要抛异常

```java
CodeEnum.failed_send_user_message.assertNotEquals(messagesMapper.addMessage(userMessage),1);
```





## 操作redis失败要抛异常

```java
        try{
            updateMessageCountInRedis(receiverId);
        }catch (Exception e){
            CodeEnum.failed_get_messageCount_from_redis.assertIsFalse(false);
        }
```





## 找bug

多动脑，多实践调试

而不是问为什么

问题列一个清单

一个一个解决

而不是单纯提出问题问为什么







## entity

别着急写entity

具体看接口需要什么

## 已经被userId搞了一个多钟了

哈哈哈

我一定命名清楚！！！







# sql



## mysql null字段占的字节多吗

没关系~~~

mysql数据口内部通过算法能解决



## mysql 多条件嵌套

```sql
and (status != -1 or status != 3)
```



## 多种情况的update

mybatis 支持if



## sql日期的比较

直接比

```sql
time < now()
```

如果在xml中，则需要用转移或者CDATA（xml中规定的，而不是mybatis）

```xml
<![CDATA[ select s.* from xxx s where s.status<5 ]]>
```



## mybatis 生成

free mybatis plugin 不能用了





## Mybatis 变量别名

```xml
	<resultMap id="messageOverview" type="com.hnsc.cloud.controller.response.MessageOverviewResp">
        <result column="id" property="messageId"></result>
        <result column="title" property="title"></result>
        <result column="create_time" property="createTime"></result>
        <result column="readed" property="readed"></result>
    </resultMap>
    <select id="getMessagesOverview" resultMap="messageOverview">
        select * from user_message where user_id = #{userId} order by create_time desc
    </select>
```

别用result啦！！！

直接sql 的 as 就可以取别名



## 复杂SQL语句

尽量不在一个查询之后，再进行迭代查询

绝大部分情况都是可以合成一个sql的

用好join







## left join

![image-20211231101503642](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211231101503642.png)

![image-20211231101531918](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211231101531918.png)



## mysql 用户密码

加密后的

![image-20220113155804627](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220113155804627.png)



## mybatis resultType是String

```xml
resultType="java.lang.String"
```





## Long 和long，Integer 和 int

这是包装类和数据类型的区别

包装类除了数据类型之外还封装了一些其他方法

比如说与字符串的转换



## String



## 删除mapper，但是xml里的语句还在。。。

先从mapper跳到xml删了sql语句

再删mapper里的方法





## mybatis 返回主键

insert会自动填充

要不就用注释

```java
    @Options(useGeneratedKeys=true, keyProperty="id", keyColumn="id")
    int insertInterview(@Param("compInterview") CompInterview compInterview);
```

再不行就xml

```xml
<insert id="insertInterview" parameterType="com.hnsc.cloud.entity.CompInterview" useGeneratedKeys="true" keyProperty="id" keyColumn="id">
 ...
</insert>
```







## mybatis boolean映射

数据库的0和1可以映射成false和true



## 异常回滚

```
@Transactional(rollbackFor = Exception.class)
```



## update left join

是无效的





## mybatis collection

可以嵌套把多个项给映射到一个list对象上！

而不是简单的同类型赋值



## mysql 连续两次join

不可以的



## mybbatis 摆脱resultmap

直接 sql 的 as 就可以取别名



## sql join时where后面的选择哪张表的参数很重要



选取的不对，会有重复项



## 新建数据库chartset

chartset: utf8

collation: utf8_bin





## mybatis date处理

含有的空格会转换成T

![image-20220112144106935](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220112144106935.png)

解决：

实体类 - 变量处添加注解

```java
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")
    private LocalDateTime interviewTime;
```



## sql 查到一条就返回







## mapper 和表对应好！！

从service开始迁移



## 唯一表示，索引

快



## 两次排序

```bash
order status,time
```

先按status 升序，再按照time升序

```bash
order status desc,time
```



# mybatis plus



## xml模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.sm.dao.UserMapper">

</mapper>
```





## entity名与表名

可以用`@TableName`注解描述映射关系



# satoken



## 自带token

同一浏览器、postman的话

satoken会自动在cookie中添加token



## satoken允许多端登录

不会出现token的冲突



## headers

```
satoken + 返回的token
```



# 测试



## 构建的那个

![image-20220112172453451](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220112172453451.png)



## 计数

![image-20220113093036576](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220113093036576.png)

一个请求减1

别忘了大于0，因为消息数量应该恒为正数



## count 始终不对

原因是前端可能也正在测试

把数据给改了！

我还没刷新数据库



## postman没登录也能成功请求

那是因为该web应用在redis里存了session

postman也支持保存session



## 线上环境500了

连上去看日志





## 测试环境的数据库不一样

测试有自己



## 冒烟测试前后端都要跑？

有人跑了冒烟测试用例就行

冒烟测试是UI操作的







## 多动动脑子

别总是问为什么

多推敲，论证，逻辑推理，实验



## payload

**IP packet data payload.** An IP packet consists of an [Ethernet](https://www.techtarget.com/searchnetworking/definition/Ethernet), IP and TCP header. This information helps the packet adhere to the communication protocol standard and reach its destination on the network. 

The payload portion of the packet contains the data that a user or device wants to send

# 图床

```java
try {
    url = ossUtil.upload(ossPath, file,1000*60*60*24);
} catch (Exception e) {
    CodeEnum.error_upload_institution.newException();
    log.error("上传表格失败。", e);
    e.printStackTrace();
}
file.delete();  // 删除
```

上传到oss，返回url





# Nacos

(Naming Configuration Service)

注册中心+配置中心



Nacos=Eureka+Config+Bus



## 服务发现

![image-20211230105332635](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20211230105332635.png)

Nacos 可以把哪个provider告诉给客户端知道





# 开会



## 接口设计

讨论接口设计

首先，观点要表数清楚

确保大家明白你是什么意思



其次，参考别人的网站是怎么做的

他们已经是考虑详尽的

意见极其不和时，参考别人的网站就像



无意义的争辩很浪费时间

谁都无法说服对方

直接摆例子是最有效的



## 数据库设计

宏滨提出来说要把两张表合成一张

小黑不太同意

已知合成一张表确实是优化

此时有效的沟通就是

小黑就尽力举出合成一张表可能会出现的问题

如果都能解决，那就合并！没啥好说的







# Redis

## redis 删除对象

因为调试的原因，redis里存了错误的数据

需要像连接数据库一样连接到redis进行操作



## redis 删除单个key

```bash
del key
```



## redis 远程连接

```bash
redis-cli -h host -p port -a password
```



## redis 查看所有keys

```bash
keys *
```



```bash
get key
```



## redis 是可以存数字的

！！



## 放redis 的条件

查询量大

长久不变





# 测试环境

8.134.82.101

root Hnsc123456

