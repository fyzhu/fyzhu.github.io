---
title: centos下php安装扩展
categories:
  - 未分类
date: 2020-07-03 10:44:46
tags:
  - centos
  - php
---
### 背景
centos7.5
使用宝塔安装php7.3
宝塔安装的 php 没有 fileinfo 扩展

### 安装扩展
#### 下载扩展
可以单独下载扩展，也可以下载整个php

下载整个php：把版本换为你需要的版本
```
# wget -O php-7.3.19.tar.gz http://cn2.php.net/get/php-7.3.19.tar.gz/from/this/mirror
```

#### 解压
```
# tar -zxvf php-7.3.19.tar.gz
```
#### 进入扩展目录
```
# cd php-7.3.19/ext/fileinfo/
```

#### 生成配置
1. 在扩展目录 (fileinfo) 下运行你安装的 php bin 目录下的 phpize 

```
[fileinfo]# /www/server/php/73/bin/phpize
```
2. 配置
   
```
[fileinfo]# ./configure --with-php-config=/www/server/php/73/bin/php-config
```
#### 编译并安装

```
# make && make install
```
#### 更改配置文件 php.ini
   
把 extension=fileinfo 前面的分号去掉
也可以使用命令，类似

```
# echo "extension = oauth.so" >> /www/server/php/73/etc/php.ini
```
#### 重载php

```
# /etc/init.d/php-fpm-73 reload
```
#### 检查是否安装成功

```
# php -m|grep -i fileinfo
```


参考文章1：https://blog.csdn.net/qivan/article/details/64439911
参考文章2：https://www.php.cn/topic/bt/429078.html