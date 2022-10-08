---
title: webpack入门
url: 34.html
id: 34
categories:
  - technology
  - front-end
date: 2017-09-01 20:10:22
tags:
---

默认配置文件
webpack.config.js 
webpack命令参数 
```
--config webpack.config.js//指定配置文件 
--progress //打包进度 
--display-modules 
--colors 
--display-reason 
```
配置文件webpack.config.js中的参数 
entry 指定入口文件，可以是字符串、数组、对象 
output 指定输出 
路径，文件名 
path、filename、publicPath \[name\]\[hash\]\[chunkhash\] 
plugins 指定插件，是数组，
如：html-webpack-plugin 需要先安装 npm install ，然后引用require() 
module:{loaders:{}}