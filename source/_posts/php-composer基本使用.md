---
title: php composer基本使用
categories:
  - 未分类
date: 2020-06-02 20:13:30
tags: 
  - php 
  - composer
---
composer update 慢
### 设置镜像
```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```
参考：https://pkg.phpcomposer.com/

### 列出现有配置
```
composer config -g --list
```
参考：https://docs.phpcomposer.com/03-cli.html#config