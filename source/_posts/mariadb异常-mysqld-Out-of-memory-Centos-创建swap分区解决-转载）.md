---
title: 'mariadb异常 mysqld: Out of memory Centos 创建swap分区解决(转载）'
url: 236.html
id: 236
categories:
  - 技术
  - 数据库
date: 2018-05-10 14:45:20
tags:
---

最近几天,[服务器](http://www.yangshengliang.com/webserver "服务器")异常，常报500错误，数据库无法连接，网站不能访问。查看mariadb日志，打开： /var/log/mariadb/mariadb.log
<pre class="crayon-plain-tag">160915&nbsp;19:44:22&nbsp;InnoDB:&nbsp;Fatal&nbsp;error:&nbsp;cannot&nbsp;allocate&nbsp;memory&nbsp;for&nbsp;the&nbsp;buffer&nbsp;pool
160915&nbsp;19:44:22&nbsp;[ERROR]&nbsp;Plugin&nbsp;'InnoDB'&nbsp;init&nbsp;function&nbsp;returned&nbsp;error.
160915&nbsp;19:44:22&nbsp;[ERROR]&nbsp;Plugin&nbsp;'InnoDB'&nbsp;registration&nbsp;as&nbsp;a&nbsp;STORAGE&nbsp;ENGINE&nbsp;failed.
160915&nbsp;19:44:22&nbsp;[ERROR]&nbsp;mysqld:&nbsp;Out&nbsp;of&nbsp;memory&nbsp;(Needed&nbsp;128917504&nbsp;bytes)
160915&nbsp;19:44:22&nbsp;[ERROR]&nbsp;mysqld:&nbsp;Out&nbsp;of&nbsp;memory&nbsp;(Needed&nbsp;96681984&nbsp;bytes)
160915&nbsp;19:44:22&nbsp;[ERROR]&nbsp;mysqld:&nbsp;Out&nbsp;of&nbsp;memory&nbsp;(Needed&nbsp;72499200&nbsp;bytes)</pre>

是内存不够，购买是阿里云主机1G内存，不够用了,可以创建swap分区来解决。

创建4g swap分区

<table class="syntaxhighlighter bash" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
</td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2">`dd` `if``=``/dev/zero` `of=``/var/swap` `bs=1024 count=4194304 `</div>
<div class="line number2 index1 alt1">`mkswap ``/var/swap`</div>
</div>
</td>
</tr>
</tbody>
</table>

激活swap分区

<table class="syntaxhighlighter bash" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
</td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2">`swapon ``/var/swap`</div>
</div>
</td>
</tr>
</tbody>
</table>

设置自动挂载

<table class="syntaxhighlighter bash" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
</td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2">`vi` `/etc/fstab`</div>
<div class="line number2 index1 alt1">`/var/swap`               `swap                    swap    defaults        0 0`</div>
</div>
</td>
</tr>
</tbody>
</table>

重启服务器

<table class="syntaxhighlighter bash" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
</td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2">`shutdown` `-r now`</div>
</div>
</td>
</tr>
</tbody>
</table>

查看内存使用状态

<table class="syntaxhighlighter bash" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
</td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2">`free` `-m`</div>
</div>
</td>
</tr>
</tbody>
</table>
<table class="syntaxhighlighter bash" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div>
</td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2">`              ``total        used        ``free`      `shared  buff``/cache`   `available`</div>
<div class="line number2 index1 alt1">`Mem:            991         347         261          40         382         382`</div>
<div class="line number3 index2 alt2">`Swap:          4096           0        4096`</div>
</div>
</td>
</tr>
</tbody>
</table>

创建swap分区成功，再没因内存不够而maridb自动关闭了。

<div>

**原文链接地址:** [mariadb异常 mysqld: Out of memory Centos 创建swap分区解决](https://www.yangshengliang.com/webserver/626.html)

</div>