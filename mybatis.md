---
title: mybatis
date: 2023-03-06 17:30:23
tags:
categories:
---





## type 字段存储

数据库存储长度为1的`char`

```
0 -> 简单
1 -> 中等
2 -> 困难
```



`entity`

```java
@Data
@TableName("problem")
public class Problem implements Serializable {
    @TableId(type = IdType.AUTO)
    Integer id;

    String name;
    String difficulty;

    String [] d = {"简单","中等","困难"};
    public void setDifficulty(String difficulty) {
        this.difficulty = d[Integer.parseInt(difficulty)];
    }
}
```



