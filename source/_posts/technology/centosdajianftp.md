---
title: centos搭建ftp
url: 118.html
id: 118
categories:
  - technology
  - Server
date: 2017-11-20 14:04:53
tags:
---

目前Linux大部分部署的FTP服务器都是vsftpd，至于为什么，暂时没什么必要深究。 1.安装vsftpd

    # yum check-update
    # yum -y install vsftpd

2.配置参数

    # vi /etc/vsftpd/vsftpd.conf

修改为如下参数

    anonymous_enable=NO
    chroot_local_user=YES
    allow_writeable_chroot=YES
    pasv_enable=YES
    pasv_min_port=40000
    pasv_max_port=40100

关于参数具体意思：

[vsftpd 配置:chroot\_local\_user与chroot\_list\_enable详解](http://blog.csdn.net/bluishglc/article/details/42398811)

3.重启ftp

    # systemctl restart vsftpd.service
    # systemctl enable vsftpd.service

4.修改防火墙配置

    # firewall-cmd --permanent --add-service=ftp
    # firewall-cmd --reload
    # setsebool -P ftp_home_dir on

5.为ftp创建一个用户test1（指定目录为/home/www，不允许远程登录shell）

    # useradd -d /home/www -m test1 -s /sbin/nologin
    # cd /home/www
    # chmod -R 777 *

6.为ftp用户设置一个密码

    # passwd test1

这样搭建的ftp默认只能按照主动方式连接，连接时请修改一下ftp设置 阿里云服务器记得开启21端口