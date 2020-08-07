---
title: composer的安装
categories:
  - 未分类
date: 2020-08-06 10:23:24
tags:
---
#### 下载安装脚本
1. 使用命令下载，并重命名为 composer-setup.php
```
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
```
2. 浏览器下载，并重命名为 composer-setup.php
直接访问以下地址
https://install.phpcomposer.com/installer

#### 执行安装过程
此步骤会生成 composer.phar
```
php composer-setup.php
```
#### 删除安装脚本
可以手动删除，也可以使用以下命令删除
```
php -r "unlink('composer-setup.php');"
```

#### 局部安装
将上述步骤生成的 composer.phar 文件复制到任意目录（比如项目根目录下），然后通过 php composer.phar 指令即可使用 Composer 了！
#### 全局安装（windows)

1. 将 composer.phar 复制到 PHP 的安装目录下面，也就是和 php.exe 在同一级目录。
2. 在 PHP 安装目录下新建一个 composer.bat 文件，并将下列代码保存到此文件中。
`@php "%~dp0composer.phar" %*`
3. 最后重新打开一个命令行窗口试一试执行 composer --version 看看是否正确输出版本号。


参考
https://pkg.phpcomposer.com/#how-to-install-composer