---
title: Apache 配置虚拟主机三种方式
url: 92.html
id: 92
categories:
  - 技术
  - 服务器
date: 2017-09-28 15:41:05
tags:
---

一、基于IP 1. 假设服务器有个IP地址为192.168.1.10，使用ifconfig在同一个网络接口eth0上绑定3个IP：

\[root@localhost root\]# ifconfig eth0:1 192.168.1.11 \[root@localhost root\]# ifconfig eth0:2 192.168.1.12 \[root@localhost root\]# ifconfig eth0:3 192.168.1.13

2\. 修改hosts文件，添加三个域名与之一一对应：

192.168.1.11   www.test1.com 192.168.1.12   www.test2.com 192.168.1.13   www.test3.com

3\. 建立虚拟主机存放网页的根目录，如在/www目录下建立test1、test2、test3文件夹，其中分别存放1.html、2.html、3.html

/www/test1/1.html /www/test2/2.html /www/test3/3.html

4\. 在httpd.conf中将附加配置文件httpd-vhosts.conf包含进来，接着在httpd-vhosts.conf中写入如下配置：  

![复制代码](http://common.cnblogs.com/images/copycode.gif)

<VirtualHost 192.168.1.11:80> ServerName www.test1.com DocumentRoot /www/test1/ <Directory "/www/test1"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow From All </Directory> </VirtualHost> <VirtualHost 192.168.1.12:80> ServerName www.test1.com DocumentRoot /www/test2/ <Directory "/www/test2"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow From All </Directory> </VirtualHost> <VirtualHost 192.168.1.13:80> ServerName www.test1.com DocumentRoot /www/test3/ <Directory "/www/test3"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow From All </Directory> </VirtualHost>

![复制代码](http://common.cnblogs.com/images/copycode.gif)

5\. 大功告成，测试下每个虚拟主机，分别访问www.test1.com、www.test2.com、www.test3.com   二、基于主机名 1. 设置域名映射同一个IP，修改hosts：

192.168.1.10  www.test1.com 192.168.1.10  www.test2.com 192.168.1.10  www.test3.com

2\. 跟上面一样，建立虚拟主机存放网页的根目录

/www/test1/1.html /www/test2/2.html /www/test3/3.html

3\. 在httpd.conf中将附加配置文件httpd-vhosts.conf包含进来，接着在httpd-vhosts.conf中写入如下配置：

 

　　为了使用基于域名的虚拟主机，必须指定服务器IP地址（和可能的端口）来使主机接受请求。可以用NameVirtualHost指令来进行配置。 如果服务器上所有的IP地址都会用到， 你可以用*作为NameVirtualHost的参数。在NameVirtualHost指令中指明IP地址并不会使服务器自动侦听那个IP地址。 这里设定的IP地址必须对应服务器上的一个网络接口。　　下一步就是为你建立的每个虚拟主机设定<VirtualHost>配置块，<VirtualHost>的参数与NameVirtualHost指令的参数是一样的。每个<VirtualHost>定义块中，至少都会有一个ServerName指令来指定伺服哪个主机和一个DocumentRoot指令来说明这个主机的内容存在于文件系统的什么地方。 如果在现有的web服务器上增加虚拟主机，必须也为现存的主机建造一个<VirtualHost>定义块。其中ServerName和DocumentRoot所包含的内容应该与全局的保持一致，且要放在配置文件的最前面，扮演默认主机的角色。

![复制代码](http://common.cnblogs.com/images/copycode.gif)

NameVirtualHost *:80 <VirtualHost *:80>

ServerName * DocumentRoot /www/ </VirtualHost> <VirtualHost *:80> ServerName www.test1.com DocumentRoot /www/test1/ <Directory "/www/test1"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow from all </Directory> </VirtualHost>  

<VirtualHost *:80> ServerName www.test2.com DocumentRoot /www/test2/ <Directory "/www/test2"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow from all </Directory> </VirtualHost>

<VirtualHost *:80> ServerName www.test3.com DocumentRoot /www/test3/ <Directory "/www/test3"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow from all </Directory> </VirtualHost>

![复制代码](http://common.cnblogs.com/images/copycode.gif)

 4\. 大功告成，测试下每个虚拟主机，分别访问www.test1.com、www.test2.com、www.test3.com  

三、基于端口

1.  修改配置文件

将原来的 Listen 80 改为 Listen 80 Listen 8080 2. 更改虚拟主机设置：

![复制代码](http://common.cnblogs.com/images/copycode.gif)

<VirtualHost 192.168.1.10:80> DocumentRoot /var/www/test1/ ServerName www.test1.com </VirtualHost> <VirtualHost 192.168.1.10:8080> DocumentRoot /var/www/test2 ServerName www.test2.com </VirtualHost>

![复制代码](http://common.cnblogs.com/images/copycode.gif)

转载至http://www.cnblogs.com/hi-bazinga/archive/2012/04/23/2466605.html