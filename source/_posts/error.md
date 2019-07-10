---
title: git error
date: 2019-07-10 14:37:18
tags:
---
## 问题原因
windows下和linux（mac)下换行符不一致导致的

## 解决反法
```
$ git config --global core.autocrlf false  //禁用自动转换    
```
