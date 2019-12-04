---
title: postgresql备份还原
tags:
  - PostgreSQL
url: 263.html
id: 263
categories:
  - technology
  - database
date: 2019-12-04 13:19:33
---

一、备份
1.命令行下备份为纯文本格式
切换为postgres用户（linux 命令）

su - postgres

备份到backupfile.bak

pg_dump dbname > backupfile.bak

windows下使用-U参数切换用户

pg_dump -h localhost -U postgres -p 5555 dbname > backupfile.bak

2.pgAdmin 4客户端备份为归档文件格式
二、还原
纯文本格式的脚本
使用psql

1.cd到postgresql安装目录，如：d:\program files\postgresql\10\bin>

2.执行 psql -U postgres -d dbname -p 5555 < backupfile.bak

另：使用CMD，不要使用powershell

不加-U（大写），windows下默认是administrator用户，-p是端口

归档文件格式（.sql文件，.backup文件）
使用pg_restore

参数：-d 数据库 -j 线程数（可以多线程提高速度） -v 详细模式（显示还原过程）-U（用户名，windows下需要加这项）

pg_restore --dbname=mydb --jobs=4 --verbose mydb.backup

简写：pg_restore -d mydb -j 4 -v mydb.backup

 

备注

命令行启动postgresql

pg_ctl start -D ../data

../data为你的数据存放路径