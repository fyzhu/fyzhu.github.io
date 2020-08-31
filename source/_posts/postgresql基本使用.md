---
title: postgresql基本使用
categories:
  - 未分类
date: 2019-12-24 10:20:42
tags:
---
#### 切换postgres用户
`$ sudo su - postgres`
#### 登录PostgreSQL控制台
`$ psql`
`$ psql -U postgres`
#### 退出
`postgres-# \q`

#### 允许远程访问
1.修改 ```pg_hba.conf``` 在最后面添加
```
host    all             all             0.0.0.0/0               md5
```
centos 默认在 /var/lib/pgsql/10/data 下

windows 一般在 /program files/postgresql/10/data 下

 

2.查看 ```postgresql.conf``` 是否如下配置
```
listen_addresses = '*'
port = 5432
```