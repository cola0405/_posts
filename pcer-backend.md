---
title: pcer_backend
date: 2023-03-07 10:50:04
tags:
categories:
---







## component无法注入

默认扫 `com.pcer`







# controller

return `R` `RD`

详细在仓库找







# JDBC

## 性别存储

```java
@Data
@TableName("problem")
public class Problem implements Serializable {
    @TableId(type = IdType.AUTO)
    Integer id;

    String name;
    String difficulty;

    String [] d = {"简单","中等","困难"};
    void setDifficulty(String difficulty){
        this.difficulty =  d[Integer.parseInt(difficulty)];
    }
}
```





## insert

```xml
    <insert id="newProblem" parameterType="com.pcer.entity.Problem">
        insert into problem values(null, #{name}, #{difficulty}, #{content})
    </insert>
```



## update

```xml
    <update id="removeTag">
        update problem_tag_relation set is_valid = 0 where problem_id = #{problemId} and tag_id = #{tagId}
    </update>
```





## join

```xml
    <select id="getProblemTagNames" resultType="java.lang.String">
        select tag.name from (select tag_id from problem_tag_relation where problem_id = #{id} and is_valid = 1) as ptr
            join tag on ptr.tag_id = tag.id
    </select>
```







## 返回id







## 返回hashmap

没办法直接返回，只能自己转

```java
package com.pcer.util;

import com.pcer.dao.TagDao;
import com.pcer.entity.Tag;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import java.util.ArrayList;
import java.util.HashMap;

@Component
public class MapTool {
    @Resource
    TagDao tagDao;

    public HashMap<String, Integer> getTag2Id(){
        ArrayList<Tag> tagList = tagDao.getTagList();
        HashMap<String, Integer> tag2Id= new HashMap<>();
        for(Tag tag : tagList){
            tag2Id.put(tag.getName(), tag.getId());
        }
        return tag2Id;
    }
}

```







# 数据库

## 多tag 建表、数据访问

relation



就多次查询吧

```java
    public List<ProblemItem> getProblems() {
        ArrayList<ProblemItem> res = new ArrayList<>();
        List<Problem> problems = problemDao.getProblems();
        for(Problem problem : problems){
            ProblemItem p = new ProblemItem();
            p.setId(problem.getId());
            p.setName(problem.getName());
            p.setDifficulty(problem.getDifficulty());
            p.setTags(problemDao.getProblemTags());
            res.add(p);
        }
        return res;
    }
```







## 插入数据中文乱码

mybatis配置

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/pcer?serverTimezone=UTC&characterEncoding=utf8
```

加上编码设置就行





# dao



## 事务

利用事务处理，可以保证一组操作不会中途停止，它们会作为整体执行

如果没有错误发生，整组语句提交给（写到）数据库表

如果发生错误，则进行回退（撤销）以恢复数据库到某个已知且安全的状态  



```
start transaction;
delete ...
delete ...
commit;
```

当 `commit` 或 `rollback` 语句执行后，事务会自动关闭  



`savepoint` 回滚到 `savepoint`

```
savepoint delete1;
...
rollback to delete1;
```





## 事务问题

### 脏写（更新丢失）

就是我刚才明明写了一个数据值，结果过了一会却没了。

而它的本质就是事务 B 去修改了事务 A 修改过的值，但是此时事务 A 还没提交，所以事务 A 随时会回滚

导致事务 B 修改的值也没了，这就是脏写的定义。



### 脏读

它的本质是事务 B 去查询了事务 A 修改过的数据，但是此时事务 A 还没提交，

所以事务 A 随时会回滚导致事务 B 再次查询就读不到刚才事务 A 修改的数据了，这就是脏读。





service有多个sql查询

需要锁表，不然会脏读





### 不可重复读

在同一个事务内，两个相同的查询返回了不同的结果





### 幻读

你一个事务 A，先发送一条 SQL 语句，里面有一个条件，要查询一批数据出来

如 `SELECT * FROM table WHERE id > 10`。然后呢，它一开始查询出来了 10 条数据

接着这个时候，别的事务 B往表里插了几条数据，而且事务 B 还提交了，此时多了几行数据

幻读就是你一个事务用一样的 SQL 多次查询

结果每次查询都会发现查到一些之前没看到过的数据

注意，幻读特指的是你查询到了之前查询没看到过的数据，此时说明你是幻读了





Ps: 不可重复读重点在于**update和delete**，而幻读的重点在于**insert**



## 隔离级别

```
isolation=Isolation.READ_UNCOMMITTED
```

以操作同一行数据为前提，读事务允许其他读事务和写事务，未提交的写事务**禁止其他写事务（但允许其他读事务）**

此隔离级别可以防止更新丢失，但不能防止脏读、不可重复读、幻读。此隔离级别可以通过“排他写锁”实现



```
iIsolation.READ_COMMITTED
```

以操作同一行数据为前提，读事务允许其他读事务和写事务，未提交的写事务**禁止其他读事务和写事务**

此隔离级别可以防止更新丢失、脏读，但不能防止不可重复读、幻读。此隔离级别可以通过“瞬间共享读锁”和“排他写锁”实现



```
iIsolation.REPEATABLE_READ
```

**事务的默认隔离等级**

以操作同一行数据为前提，读事务**禁止其他写事务（但允许其他读事务）**，未提交的写事务**禁止其他读事务和写事务**

此隔离级别可以防止更新丢失、脏读、不可重复读，但**不能防止幻读**。此隔离级别可以通过“共享读锁”和“排他写锁”实现



```
iIsolation.SERIALIZABLE
```

提供严格的事务隔离。它要求事务序列化执行，事务只能一个接着一个地执行，不能并发执行。

此隔离级别**可以防止更新丢失、脏读、不可重复读、幻读**

如果仅仅通过“行级锁”是无法实现事务序列化的，必须通过其他机制保证新插入的数据不会被刚执行查询操作的事务访问到。
