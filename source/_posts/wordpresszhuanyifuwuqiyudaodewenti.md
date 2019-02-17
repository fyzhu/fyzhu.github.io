---
title: wordpress转移服务器遇到的问题
url: 59.html
id: 59
categories:
  - 未分类
date: 2017-09-14 11:33:39
tags:
---

1.更换数据库，数据库配置在wp-config.php里

2.更换域名，修改数据库里wp_options表里的 siteurl（option_id=1)和home(最新版本中option_id一般为2）的链接

3.找回密码，邮箱无法发送邮件，报错

无法发送电子邮件 可能原因：您的主机禁用了mail()函数

Linux服务器安装sendmail

Centos

Yum install sendmail

Ubuntu

Apt-get install sendmail

不报错了，但是还是无法收到邮件

更改数据库wp_users表

把密码字段修改为hello的MD5值

5d41402abc4b2a76b9719d911017c592

可以用hello登录，然后在后台更改密码。