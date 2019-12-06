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