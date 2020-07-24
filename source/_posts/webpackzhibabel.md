---
title: webpack之babel
url: 32.html
id: 32
categories:
  - 技术
  - 前端
date: 2017-08-31 23:17:35
tags:
---
```
loader: 'babel-loader',//由babel变为babel-loader 
exclude:__dirname +'/node_modules/',//这种方式更快 
include:__dirname+'/src/',//这种方式更快  
exclude:path.resolve(__dirname ,'node_modules'),  
include:path.resolve(__dirname ,'src'),
```