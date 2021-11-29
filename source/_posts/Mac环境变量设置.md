---
title: Mac环境变量设置
categories:
  - 未分类
date: 2021-06-04 09:48:28
tags:
---
### 设置环境变量
```bash
export http_proxy=http://127.0.0.1:8123/
export ALL_PROXY=socks5://127.0.0.1:1086
export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>
```
等号前后不能有空格
用冒号分隔

### 删除环境变量
```bash
unset http_proxy
unset ALL_PROXY
```
### 查看环境变量
```bash
# 查看某一个
echo $PATH
# 查看所有
env
```