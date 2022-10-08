---
title: centos 下chmod
url: 22.html
id: 22
categories:
  - technology
  - Server
date: 2017-08-31 14:36:06
tags:
---

chmod也可以用数字来表示权限如 chmod 777 file
语法为：chmod abc file
其中a,b,c各为一个数字，分别表示User、Group、及Other的权限。
r=4，w=2，x=1
若要rwx属性则4+2+1=7；
若要rw-属性则4+2=6；
若要r-x属性则4+1=5。

给文件夹及文件夹里面的所有文件加权限
chmod -R 777 folder