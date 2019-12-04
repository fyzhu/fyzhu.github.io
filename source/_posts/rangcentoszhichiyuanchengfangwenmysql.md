---
title: 让centos支持远程访问mysql
url: 71.html
id: 71
categories:
  - technology
  - Server
date: 2017-09-19 11:23:48
tags:
  - mysql
  - centos
---
Mysql为了安全性，在默认情况下用户只允许在本地登录，可是在有此情况下，还是需要使用用户进行远程连接，因此为了使其可以远程需要进行如下操作：

一、允许root用户在任何地方进行远程登录，并具有所有库任何操作权限，具体操作如下：
在本机先使用root用户登录mysql：
mysql -u root -p"youpassword"
进行授权操作：
mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION;
重载授权表：
FLUSH PRIVILEGES;
退出mysql数据库：
exit

二、允许root用户在一个特定的IP进行远程登录，并具有所有库任何操作权限，具体操作如下：
在本机先使用root用户登录mysql：
mysql -u root -p"youpassword"
进行授权操作：
GRANT ALL PRIVILEGES ON *.* TO root@"172.16.16.152" IDENTIFIED BY "youpassword" WITH GRANT OPTION;
重载授权表：
FLUSH PRIVILEGES;
退出mysql数据库：
exit

三、允许root用户在一个特定的IP进行远程登录，并具有所有库特定操作权限，具体操作如下：
在本机先使用root用户登录mysql：
mysql -u root -p"youpassword"
进行授权操作：
GRANT select，insert，update，delete ON *.* TO root@"172.16.16.152" IDENTIFIED BY "youpassword";
重载授权表：
FLUSH PRIVILEGES;
退出mysql数据库：
exit

四、删除用户授权，需要使用REVOKE命令，具体命令格式为：
REVOKE privileges ON 数据库[.表名] FROM user-name;
具体实例，先在本机登录mysql:
mysql -u root -p"youpassword"
进行授权操作：
GRANT select，insert，update，delete ON TEST-DB TO test-user@"172.16.16.152" IDENTIFIED BY "youpassword";
再进行删除授权操作：
REVOKE all on TEST-DB from test-user;
****注：该操作只是清除了用户对于TEST-DB的相关授权权限，但是这个“test-user”这个用户还是存在。
最后从用户表内清除用户：
DELETE FROM user WHERE user="test-user";
重载授权表：
FLUSH PRIVILEGES;
退出mysql数据库：
exit

五、MYSQL权限详细分类：
全局管理权限：
FILE: 在MySQL服务器上读写文件。
PROCESS: 显示或杀死属于其它用户的服务线程。
RELOAD: 重载访问控制表，刷新日志等。
SHUTDOWN: 关闭MySQL服务。
数据库/数据表/数据列权限：
ALTER: 修改已存在的数据表(例如增加/删除列)和索引。
CREATE: 建立新的数据库或数据表。
DELETE: 删除表的记录。
DROP: 删除数据表或数据库。
INDEX: 建立或删除索引。
INSERT: 增加表的记录。
SELECT: 显示/搜索表的记录。
UPDATE: 修改表中已存在的记录。
特别的权限：
ALL: 允许做任何事(和root一样)。
USAGE: 只允许登录--其它什么也不允许做。

转载至Linux公社：http://www.linuxidc.com/Linux/2013-06/86459.htm