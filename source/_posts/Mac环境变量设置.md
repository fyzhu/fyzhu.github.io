---
title: Mac环境变量设置
categories:
  - 未分类
date: 2021-06-04 09:48:28
tags:
---
### 设置环境变量

export http_proxy=http://127.0.0.1:8123/

export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>

等号前后不能有空格
用冒号分隔

### 删除环境变量

unset http_proxy

### 查看环境变量
echo $PATH

env