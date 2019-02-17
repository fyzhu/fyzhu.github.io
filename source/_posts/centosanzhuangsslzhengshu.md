---
title: centos安装ssl证书
url: 94.html
id: 94
categories:
  - 技术
  - 服务器
date: 2017-09-28 18:40:00
tags:
---

一为apache启用ssl，首先我们需要为Apache安装mod\_ssl模块提供TLS/SSL功能： https是通过mod\_ssl实现的，因此检查并安装mod_ssl：

1

\[iyunv@Centos ~\]# ls /etc/httpd/modules/ | grep "mod\_ssl"   #默认没有安装mod\_ssl # yum list all mod\_ssl   #查看mod\_ssl的安装包信息 yum install -y mod\_ssl  #安装mod\_ssl

检查mod_ssl是安装结果

1 2

rpm -qc mod\_ssl /etc/httpd/conf.d/ssl.conf      #mod\_ssl的配置文件存放位置

接下来我们修改httpd的SSL配置

1

cd /etc/httpd/conf.d #进入HTTPD的SSL配置目录 vim ssl.conf #编辑SSL配置文件

      转载至https://www.iyunv.com/thread-84322-1-1.html     总结： 1.安装mod_ssl模块 2.vim ssl.conf #编辑SSL配置文件 文件路径以及名称可能不一样 我的路径以及名称/etc/httpd/conf.d/ssl.conf