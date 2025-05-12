---
title: redis的基本数据类型与常用方法
date: 2021/03/22 16:37:07 
tags: 
 - blog 
categories:
  - 编程
---



### 1.字符串 (string)

key-value类型的数据

案例：

```redis
set char test
# 1
get char
# "test"
```



### 2.哈希表 (hash)

类似于二维的json型数据

案例：

```
hset hash a b
# 1
hget hash a
# "b"
hset hash c d e f
# 2
hvals hash
#1） "b"
#2） "d"
#3） "f" 
```



### 3.列表 (list)

列表，可从头或者从尾push进数据，也可从头或者尾pop出数据，常用于队列

案例：

```
lpush queue a b c
# 3
rpush queue d e f
# 3
lrange queue 0 -1 # start end -1表示最后一位
# c
# b
# a
# d
# e
# f
```



### 4.集合 (set)

集合的值唯一，插入相同值时会失败，spop值时取值为乱序

案例：

```
sadd set 1 2 3
# 3
smembers set
# 1
# 2
# 3
spop 
# 2
spop 
# 3
spop
# 1
```



### 5.有序集合 (zset)

有序集合是有序集的集合，添加新成员时，score和 member 任意值重复均插入失败

案例：

```
zadd zset 1 baidu.com 2 google.com
# 2
zrange zset 0 -1 withscores
# baidu.com
# 1
# google.com
# 2
```

