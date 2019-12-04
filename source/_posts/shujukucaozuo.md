---
title: 数据库操作
url: 97.html
id: 97
categories:
  - technology
  - database
date: 2017-09-29 10:55:56
tags:
---

DELETE   语句每次删除一行，并在事务日志中为所删除的每行记录一项。 TRUNCATE   TABLE   通过释放存储表数据所用的数据页来删除数据，并且只在事务日志中记录页的释放。 **修改表名** mysql> alter table student rename person; Query OK, 0 rows affected (0.03 sec) **修改字段的数据类型** mysql> alter table person modify name varchar(20); Query OK, 0 rows affected (0.18 sec) Records: 0 Duplicates: 0 Warnings: 0 此处modify后面的name为字段名，我们将原来的varchar(25)改为varchar(20) **修改字段名** mysql> alter table person change stu_name name varchar(25); Query OK, 0 rows affected (0.20 sec) Records: 0 Duplicates: 0 Warnings: 0