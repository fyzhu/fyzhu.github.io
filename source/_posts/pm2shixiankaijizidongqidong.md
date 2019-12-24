---
title: pm2实现开机自动启动
url: 170.html
id: 170
categories:
  - technology
  - Server
date: 2018-01-25 18:52:20
tags:
  - pm2
---

可以通过`pm2 startup`来实现开机自启动。细节可[参考](http://pm2.keymetrics.io/docs/usage/startup/)。大致流程如下

1.  通过`pm2 save`保存当前进程状态。
2.  通过`pm2 startup [platform]`生成开机自启动的命令。

例如： 
1. 使用pm2启动node ：# pm2 start /home/wwwroot/web.js --watch 
2. dump这些进程列表：# pm2 save 
3. 生成自启动脚本：# pm2 startup centos

转载
https://www.cnblogs.com/chyingp/p/pm2-documentation.html