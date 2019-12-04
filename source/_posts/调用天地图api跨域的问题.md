---
title: 调用天地图api跨域的问题
date: 2019-07-22 10:42:21
categories:
  - technology
  - GIS
tags:
 - 跨域
 - map
---
#### 调用天地图api跨域的问题
自2019年1月1日，访问天地图api需要使用token，一个token只能在一个域名下使用，开发时最好每人申请一个token，自己用自己的token就不会有跨域问题了
##### 问题描述
使用token调用天地图api获取地图瓦片时出现跨域问题
##### 问题产生原因
多个域名使用同一个token调用天地图api
##### 解决方案
每个域名申请一个token