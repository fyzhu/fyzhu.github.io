---
title: centos关闭防火墙
date: 2029-03-11 22:06:14
tags: question
---
参考文档
防火墙设置

#停止firewall服务 systemctl stop firewalld.service

#禁止firewall开机启动 systemctl disable firewalld.service




关闭selinux

#修改配置文件 vi /etc/selinux/config

#SELINUX=enforcing #注释掉

#SELINUXTYPE=targeted #注释掉

SELINUX=disabled #增加

:wq! #保存退出

#使配置立即生效 setenforce 0

iptables