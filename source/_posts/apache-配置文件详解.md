---
title: apache 配置文件详解
date: 2019-02-21 13:13:05
tags:
---
1.允许其他主机访问
```
<VirtualHost *:80>
    <Directory "F:/wamp/www/test">
        Options FollowSymLinks
        AllowOverride All
        Order allow,deny
        Allow from all      #允许来自所有主机的访问
        Require all granted #2.4以上需要加这一句
    </Directory>
    ServerAdmin 826096331@qq.com
    DocumentRoot "F:/wamp/www/test"
    ServerName www.test.com
    DirectoryIndex index.php index.html
    ServerAlias test.com
    ErrorLog "logs/test.bin-error_log"
    CustomLog "logs/test.bin-access_log" common
</VirtualHost>
```
--------------------- 
作者：u013032788 
来源：CSDN 
原文：https://blog.csdn.net/u013032788/article/details/51395622 
版权声明：本文为博主原创文章，转载请附上博文链接！