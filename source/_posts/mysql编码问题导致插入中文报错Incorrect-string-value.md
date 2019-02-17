---
title: 'mysql编码问题导致插入中文报错Incorrect string value:'
url: 249.html
id: 249
categories:
  - 技术
  - 数据库
date: 2018-05-22 23:35:28
tags:
---

设置数据库编码为中文

可能需要用到的命令

查看数据库编码方式的两个命令

1.status

2.show variables like &#8216;character%&#8217;;

+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+

| Variable_name | Value |

+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+

| character_set_client | latin1 |

| character_set_connection | latin1 |

| character_set_database | latin1 |

| character_set_filesystem | binary |

| character_set_results | latin1 |

| character_set_server | latin1 |

| character_set_system | utf8 |

| character_sets_dir | /usr/share/mysql/charsets/ |

设置编码的命令

1.  set names utf8 (设置客户端的编码格式，会给其中的三项设置为utf-8)

2.分别给每项设置编码

set character_set_connection = &#8216;utf8&#8217;;

set character_set_results = &#8216;utf8&#8217;;

set character_set_client = &#8216;utf8&#8217;;

单独给服务端设置编码

set character_set_server = &#8216;utf8&#8217;;

给表设置编码

alter table books default character set &#8216;utf8&#8217;;

给数据库设置编码

alter database cAuth default character set &#8216;utf8&#8217;;

网上搜有说设置为gbk的，但是我觉得最好还是用utf8

如果以上方法都试过还不行，那就删除表重新建，再建表的时候加一句设置编码

create table books(

id int not null auto_increment primary key,

isbn varchar(20) not null,

openid varchar(50) not null,

title varchar(100) not null,

image varchar(150) ,

alt varchar(100) not null,

publisher varchar(50) not null,

summary varchar(1000) not null,

price varchar(100) ,

rate float,

tags varchar(100),

author VARCHAR(100)

)default character

set utf8;

我的重建表之后就可以了

另外

安装目录下找到 my.ini

default-character-set=utf8

我的文件里没搜到这个

&nbsp;

<div>在设置了mysql的字符集之后还是会有很抱怨在console输入中文的时候还是会报错。这个主要是windows是中文的，中文系统dos的默认输入输出是gb2312编码，但是之前我们把client characterset设置成了utf8，然后mysql就将我们输入的gb2312的字符当作utf8来处理，然后就导致了错误。</div>
<div>一种解决方法是将client characterset设置成gb2312或者gbk，或者在使用中文前用命令set names gbk，这样能够暂时的让这个窗口正常接收中文字符。</div>