---
title: Mac下使用mysql
date: 2019-07-13 12:07:49
tags: 
 - mysql
 - Mac
---

## 安装

1. 去官网下载安装
2. 使用 homebrew 安装

## 启动服务
```
$ mysql.server start
```
## 设置密码
homebrew安装默认是没有密码的
```
mysql> alter user 'root'@'localhost' identified with mysql_native_password by '123456';
Query OK, 0 rows affected (0.10 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.01 sec)
```