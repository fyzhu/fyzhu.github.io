---
title: MongoDB 快速上手
categories:
  - 未分类
date: 2021-05-09 12:30:05
tags:
---
### 连接
默认端口 27017
```shell
mongo
```
指定端口 27027
```shell
mongo --port 27027
```
连接远程主机上的 MongoDB 实例
```shell
mongo "mongodb://mongodb0.example.com:28015"

mongo --host mongodb0.example.com:28015

mongo --host mongodb0.example.com --port 28015

```
### 退出
```shell
quit()
```

### 切换数据库
```shell
use <database>
```
### 列出数据库
show dbs

### 列出数据表
show tables
### 查询数据
db.<collection>.find()