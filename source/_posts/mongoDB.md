---
title: MongoDB 快速上手
categories:
  - 未分类
date: 2021-05-09 12:30:05
tags:
---
### 连接
默认端口 27017
```bash
mongo
```
指定端口 27027
```bash
mongo --port 27027
```
连接远程主机上的 MongoDB 实例
```bash
mongo "mongodb://mongodb0.example.com:28015"

mongo --host mongodb0.example.com:28015

mongo --host mongodb0.example.com --port 28015

```
### 退出
```bash
quit()
```
### 列出数据库
```
show dbs
```

### 切换数据库
```bash
use <database>
```
### 列出数据表
```
show tables
```
### 查询数据
```
db.<collection>.find()
db.<collection>.find().count()
db.<collection>.find().pretty()
```
### 启动

#### osx
安装完成后，我们可以把 MongoDB 的二进制命令文件目录（安装目录/bin）添加到 PATH 路径中：
```bash
export PATH=/usr/local/mongodb/bin:$PATH
```
启动：
```bash
mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork
```
- --dbpath 设置数据存放目录
- --logpath 设置日志存放目录
- --fork 在后台运行
查看 mongod 服务是否启动：
```bash
ps aux | grep -v grep | grep mongod
```
[OSX MongoDB](https://www.runoob.com/mongodb/mongodb-osx-install.html)
#### windows

启动

1. 进入 bin 目录中执行 mongod.exe 文件 或 把 bin 目录添加到 path

```bash
C:\mongodb\bin\mongod --dbpath c:\data\db
```

2. 如果已存在 MongoDB 服务，可以使用 net 命令启动
```bash
net start MongoDB
```   
  
3. 服务面板启动


[Windows MongoDB](https://www.runoob.com/mongodb/mongodb-window-install.html)