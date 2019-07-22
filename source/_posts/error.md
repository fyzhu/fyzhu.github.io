---
title: 不同操作系统下回车符不同导致的git warning
date: 2019-07-10 14:37:18
tags:
 - git
---
## 问题描述
windows下git报错warning: LF will be replaced by CRLF in ***. The file will have its original line endings in your working directory.

## 问题原因
windows下和linux（mac)下换行符不一致导致的

## 解决方法
```
$ git config --global core.autocrlf false  //禁用自动转换    
```
