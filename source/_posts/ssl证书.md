---
title: ssl证书
categories:
  - 未分类
date: 2021-12-23 18:23:17
tags:
---
### 自签证书
参考 https://www.jianshu.com/p/d22baeae50ea
### 浏览器报错 ERR_SSL_PROTOCOL_ERROR
或 curl 报错 wrong version number

修改 nginx 配置

listen 443 ssl;

### 浏览器报错 ERR_CERT_INVALID

输入 thisisunsafe 

参考： https://segmentfault.com/a/1190000021843971