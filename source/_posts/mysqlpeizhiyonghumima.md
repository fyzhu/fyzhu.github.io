---
title: mysql配置用户密码
url: 73.html
id: 73
categories:
  - 技术
  - 服务器
date: 2017-09-19 11:30:27
tags:
---

当初次在机器上安装完Mysql时,你可以匿名进行访问数据库或者以不带口令的root身份进入数据库.另外如果你是一个管理员,你还要进行一些用户的建立及授权,这又涉及到设置密码的问题.下面我们就讨论一下如何设置密码: 首先我们应该知道Mysql数据库中的口令存储必须用password()函数加密它.因为在user表中是以加密形式存储口令,而不是作为纯文本.如果你没有加密,直接在数据库中执行以下语句:

复制代码代码如下:

use mysql insert into user (host,user,password) values('%','user_name','your password'); flush privileges;

相信结果不会让你满意.因为服务器比较的是加密的值,所以服务器连接一定失败.这里需要说明的是flush privileges;这条命令起到了重新加载授权表.你也可以在shell下直接用mysqladmin -u root reload或者mysqladmin -u root flush-privileges来实现重载授权表. 在Mysql环境下,你可以使用以下语句进行设置密码:

复制代码代码如下:

1.insert into user(host,user,password) values('%','user\_name',password("your password"); 2.set password for user\_name = password("your password")

以上两种方法都必须进行重载授权表. 3.当然你也可以在创建一个用户时直接设置密码,grant语句将为你自动加密口令. 如 grant all on *.* to user_name@% identified by "your password"; 另外你也可以在shell环境下用mysqladmin程序来设置密码 如 mysqladmin -u root password "your password" 快点去试一下,没问题吧! **mysql如何设置密码** 有很多方法： 1.用root 进入mysql后 mysql>set password =password('你的密码'); mysql>flush privileges; 2.使用GRANT语句 mysql>grant all on *.* to 'root'@'localhost' IDENTIFIED BY '你的密码'with grant option ; www.jb51.net mysql>flush privileges; 3.进入mysql库修改user表 mysql>use mysql; mysql>update user set password=password('你的密码') where user='root'; mysql>flush privileges; 作者 matthio   转载至脚本之家：http://www.jb51.net/article/30867.htm