---
title: mariadb支持远程访问
date: 2019-03-11 22:05:58
categories:
  - technology
  - database
tags: 
  - mysql
  - mariaDB
---

参考文档https://www.cnblogs.com/24la/p/mariadb-remoting-access.html

首先配置允许访问的用户，采用授权的方式给用户权限

1
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY '123456' WITH GRANT OPTION;
 说明：root是登陆数据库的用户，123456是登陆数据库的密码，*就是意味着任何来源任何主机反正就是权限很大的样子。

最后配置好权限之后不应该忘记刷新使之生效

1
flush privileges;
 再次访问就可以了吧。