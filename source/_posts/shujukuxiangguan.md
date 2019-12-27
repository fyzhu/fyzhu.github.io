---
title: 数据库去重
url: 88.html
id: 88
categories:
  - technology
  - database
date: 2017-09-28 15:39:52
tags:
---

数据库去重
=====

使用distinct去重：
例：select distinct  column1,column2 ... from table_name where ....;
注意：1.distinct只能放在去重字段的最前面
            2.distinct  后的字段名全部算在去重条件中   也就是如果 column1  且  column2 必须都相同才能算作重复的记录

数据库子查询怎么写？ 字句查询出去重的数据，单独使用可以正常查出数据 主句想要统计一下数量，但是报错 select count(*) from (SELECT DISTINCT lat,longi from test where id=11); 这个语句为什么是错误的？？？