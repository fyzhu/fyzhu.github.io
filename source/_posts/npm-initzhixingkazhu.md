---
title: npm list -g报错
url: 26.html
id: 26
categories:
  - 技术
  - 前端
date: 2017-08-31 16:05:29
tags:
  - npm
  - js
---

是因为prefix没有设置导致的。
在安装完nodejs后，通过npm下载全局模块默认安装到以下目录：
```
C:\Users\_username_\AppData\Roaming\npm
```

运行下面的命令设置全局模块存放路径：
```
npm config set prefix "C:\Users\_username_"
```


或者修改.npmrc文件，默认在 `C:\Users\_username_` 下

将默认值改为： 
```
prefix=C:\Users\_username_ 
```
注意斜杠\ 
```
npm config set prefix C:/Users/_username_
```
不加引号的话需要写成右斜杠，最好不要用有空格的文件夹