---
title: Redis-demo
date: 2022-01-10 16:44:31
tags:
categories:
---



# 常用命令

连接redis

```
redis-cli
```



查询所有值

```
keys *
```



获取值

```
get key
```





```
set 
```



# 数据类型

## 数字

整数

```
incr
```

```
incrby
```





浮点数

```
incrbyfloat
```





## 字符串



追加

```
set key hello
append key " world!"
```



获取长度

```
strlen key
```











## 散列表

创建

```
hset key field value
```

```
hset car color white

hget car color
>"white"
```



是否存在

```
hexist key field
```



递增

```
hincrby key field
```



删除

```
hdel key field
```





获取所有field

```
hkeys car
>"color"
>"price"
```



获取所有value

```
hvals car
>"white"
>"60"
```







## 列表

双向链表

两端修改很快



```
lpush numbers 1
lpush numbers 2
lpush numbers 3
rpush numbers 0
rpush numbers -1
```

![image-20230131142740493](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230131142740493.png)





弹出两端的元素

```
lpop numbers
rpop numbers
```





获取片段

```
lrange numbers 0 2
>(1)3
>(2)2
```





获取所有

```
lrange numbers 0 -1
```

索引超出范围则到最右端元素，不会报错

和python很像





删除指定值

```
lrem key count value
```

删除count个value

当count>0时，从左往右删除

当count<0时，从右往左删除





通过index获取值

```
lindex key index
```

```
lset key index value
```





只保留部分

```
ltrim key start end
```

类range



插入

```
linsert key before|after pivot value
```

从左往右找到pivot







## 集合



```
sadd nums 0
```

```
srem nums 0
```

因为当前集合是无序的，所以随机pop一个元素

```
spop nums
```







查看

```
smembers nums
>(1) "0"
>(2) "1" 
```





是否exist

```
sismember nums 0
```





差集、交集、并集

```
sdiff key key key ...
```

多个值时，先计算key1-key2 再计算res-key3

![image-20230131144056646](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230131144056646.png)



```
sinter key key key ...
```









## 有序集合





# 进阶

## 过期时间

```
expire key seconds
```



查看剩余时间 (秒)

```
ttl key
```





## sort

可用于顺序输出集合、列表

```
sort key
```

```
sort key desc
```









# 概念

## 冒号

表示命名空间

