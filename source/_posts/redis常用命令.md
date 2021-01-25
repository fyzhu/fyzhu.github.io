---
title: redis常用命令
categories:
  - technology
  - Server
date: 2019-12-06 16:50:12
tags: redis
---
连接
```
redis-cli -h host -p port -a password
```
显示所有
```
keys *
```
设置一个
```
set key value
```
获取一个
```
get key
```
删除一个
```
del key
```
清空当前数据库
```
flushdb
```
clear all database
```
flushall
```
获取类型
```
type key
```
获取哈希表中的所有域（field）
```
HKEYS key 
```

获取 hash 值
```
HGET KEY_NAME FIELD_NAME 
```
获取 hash 值
```
HGET KEY_NAME FIELD_NAME 
```
参考：
https://www.runoob.com/redis/redis-tutorial.html