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

loader: 'babel-loader',//由bael变为babel-loader exclude:\_\_dirname +'/node\_modules/',//这种方式更快 include:\_\_dirname+'/src/',//这种方式更快 // exclude:path.resolve(\_\_dirname ,'node\_modules'), // include:path.resolve(\_\_dirname ,'src'),