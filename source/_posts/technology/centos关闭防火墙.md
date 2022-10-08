---
title: centos关闭防火墙
date: 2019-03-11 22:06:14
categories:
  - technology
  - Server
tags: 
- centos
---
参考文档
防火墙设置
查看所有打开的端口： firewall-cmd --zone=public --list-ports
启动： systemctl start firewalld
关闭： systemctl stop firewalld
查看状态： systemctl status firewalld 
开机禁用  ： systemctl disable firewalld
开机启用  ： systemctl enable firewalld




关闭selinux

#修改配置文件 vi /etc/selinux/config

#SELINUX=enforcing #注释掉

#SELINUXTYPE=targeted #注释掉

SELINUX=disabled #增加

:wq! #保存退出

#使配置立即生效 setenforce 0

iptables

参考文档
https://www.cnblogs.com/moxiaoan/p/5683743.html