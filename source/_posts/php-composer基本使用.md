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
#### 使用阿里镜像
```
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
```
#### 全局设置
```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```
参考：https://pkg.phpcomposer.com/
#### 当前项目
```
composer config repo.packagist composer https://packagist.phpcomposer.com
```
上述命令将会在当前项目中的composer.json文件的末尾自动添加镜像的配置信息（我们也可以自己手工添加）：
```
"repositories": {

    "packagist": {

        "type": "composer",

        "url": "https://packagist.phpcomposer.com"

    }

}
```
### 列出现有配置
```
composer config -g --list
```
参考：https://docs.phpcomposer.com/03-cli.html#config

参考：https://www.php.cn/tool/composer/428026.html