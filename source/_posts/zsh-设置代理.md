---
title: zsh 设置代理
categories:
  - 未分类
date: 2021-10-03 21:29:14
tags:
---
在 `~/.zshrc` 文件里添加如下代码
```
alias setproxy="export ALL_PROXY=http://127.0.0.1:15236"
alias unsetproxy="unset ALL_PROXY"
```
```bash
# 设置代理
setproxy
# 取消代理
unsetproxy
```
[参考](https://blog.csdn.net/weixin_44259233/article/details/108403620)