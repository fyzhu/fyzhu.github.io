---
title: Apache 配置虚拟目录、虚拟主机
url: 61.html
id: 61
tags:
  - apache
categories:
  - 技术
  - 服务器
date: 2017-09-14 12:06:00
---

修改httpd.conf的配置 通过whereis httpd找到这个文件 我的在/etc/httpd/conf下 一、虚拟目录 找到<IfModule>这块，加入下面的代码

**\[plain\]** [view plain](http://blog.csdn.net/u010175124/article/details/18220495# "view plain") [copy](http://blog.csdn.net/u010175124/article/details/18220495# "copy")

 [print](http://blog.csdn.net/u010175124/article/details/18220495# "print")[?](http://blog.csdn.net/u010175124/article/details/18220495# "?")

1.  # 虚拟目录，访问D盘下面的web目录
2.  <IfModule dir_module>
3.      # 设置缺省载入页面
4.      DirectoryIndex index.html index.htm index.php
5.      # 设置站点别名，别名与访问路径是相关的，取任何名称都可以（除特殊）
6.      Alias /myweb "D:/web"
7.      <Directory D:/web>
8.      # 设置访问权限
9.          Order allow,deny
10.      Allow from all
11.      </Directory>
12.  </IfModule>

修改完成后重启Apache服务器 在浏览器中输入：http://localhost/myweb/xx.php 来访问 D:/web 下的文件 二、虚拟主机 Virtualhost httpd.conf里添加以下代码   NameVirtualHost *  表示在apache监听的所有IP和所有端口(此时只有80)上做多域名虚拟主机，如果只是IP可以不用写这一句 <VirtualHost *> 具体配置 </VirtualHost> <VirtualHost 127.0.0.2:80> DocumentRoot d:/AppServ/www2 ServerName 127.0.0.2:80 < /VirtualHost> <VirtualHost 127.0.0.3:80> DocumentRoot d:/AppServ/www3 ServerName 127.0.0.3:80 </V irtualHost>...   然后相应的配置好各个目录属性，下面是一个目录属性的典型配置： <Directory "d:/AppServ/www2"> Options Indexes FollowSymLinks Multiviews AllowOverride All Order Allow,Deny Allow from all </Directory> <Directory "d:/AppServ/www3"> Options Indexes FollowSymLinks Multiviews AllowOverride All Order Allow,Deny Allow from all </Directory>   direcory可以配置到virtualhost里面 <VirtualHost *:80> DocumentRoot /var/www/html/zhuyunfeng.com ServerName [www.zhuyunfeng.com](http://www.zhuyunfeng.com) ServerAlias [www.zhuyunfeng.com](http://www.zhuyunfeng.com) <Directory "/var/www/html/zhuyunfeng.com"> Options Indexes FollowSymLinks AllowOverride all Order allow,deny Allow from all </Directory> </VirtualHost>