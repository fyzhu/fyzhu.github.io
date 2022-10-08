---
title: node-sass 踩坑之旅
categories:
  - 未分类
date: 2020-04-19 17:08:09
tags:
---
## 下载慢
npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/
yarn config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/ -g
参考：https://www.jb51.net/article/122820.htm

## 报错 
Error: Node Sass does not yet support your current environment

原因：node 版本更换导致的

解决方法：
1. 更换回原 node 版本
2. npm rebuild node-sass
3. 卸载 node-sass 重新安装


参考：https://blog.csdn.net/yaya07755/article/details/96834875
