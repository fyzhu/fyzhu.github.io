---
title: php 修改上传文件大小限制
categories:
  - 未分类
date: 2020-06-03 17:02:34
tags: php
---
## 找到php.ini文件
Linux默认文件路径为/etc/php.ini，如果/etc/下找不到此文件，请使用附加方法1
如果找不到etc文件夹，请使用附加方法2寻找并修改
## 修改upload_max_filesize 
打开php.ini，搜索upload_max_filesize，形如upload_max_filesize=2，即允许上传2M大小到文件，修改为合适大小就可以。
## 重启apache
sudo service httpd restart




## 附加方法1：寻找php.ini
在网站根目录下新建一个php文件，命名为phpinfo.php
打开这个文件输入以下代码
<?php
phpinfo();//末尾有分号

访问这个文件即可查看到php.ini的具体路径
访问地址http://ip(如：127.0.0.1)/phpinfo.php
## 附加方法2：寻找并修改php.ini
	1打开终端
	输入 sudo vi /etc/php.ini  //php.ini的最终路径，以实际为准
	2搜索upload_max_filesize的位置
	输入 /upload_max_filesize 回车，此时会定位到upload_max_filesize，如果有多个匹配项，请找到形如upload_max_filesize=2M到位置
	3修改
	输入i进入修改模式
将光标移动到需要修改到位置，删除并修改
	4保存并退出
	输入:wq回车 //注意冒号
	5继续接下来到步骤，重启Apache

