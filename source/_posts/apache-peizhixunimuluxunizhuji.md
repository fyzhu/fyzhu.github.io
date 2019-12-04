---
title: Apache 配置虚拟目录、虚拟主机
url: 61.html
id: 61
tags:
  - apache
categories:
  - technology
  - Server
date: 2017-09-14 12:06:00
---

修改httpd.conf的配置 通过whereis httpd找到这个文件 我的在/etc/httpd/conf下 
## 一、虚拟目录 
找到<IfModule>这块，加入下面的代码

```
# 虚拟目录，访问D盘下面的web目录
<IfModule dir_module>
    # 设置缺省载入页面
    DirectoryIndex index.html index.htm index.php
    # 设置站点别名，别名与访问路径是相关的，取任何名称都可以（除特殊）
    Alias /myweb "D:/web"
    <Directory D:/web>
    # 设置访问权限
        Order allow,deny
	Allow from all
    </Directory>
</IfModule>
```

修改完成后重启Apache服务器 在浏览器中输入：http://localhost/myweb/xx.php 来访问 D:/web 下的文件 
## 二、虚拟主机
```
#配置我们自己的虚拟主机
<VirtualHost *:80>
    #修改文档根路径
    DocumentRoot "D:/Program Files (x86)/myenv/apache2.2.25/htdocs"
    #主机名称
    ServerName myvirtualhost.com
    #欢迎页面
    DirectoryIndex index.html
    <Directory "D:/Program Files (x86)/myenv/apache2.2.25/htdocs">
	Options -Indexes FollowSymLinks
	AllowOverride None
	Order allow,deny
	Allow from all
    </Directory>
    #错误日志存放位置
    ErrorLog "logs/myvirtualhost.com-error.log"
    CustomLog "logs/myvirtualhost.com-access.log" common
</VirtualHost>
```

版权声明：本文为CSDN博主「u010175124」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u010175124/article/details/18220495