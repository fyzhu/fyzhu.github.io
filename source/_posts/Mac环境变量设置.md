---
title: Mac环境变量设置
categories:
  - 未分类
date: 2021-06-04 09:48:28
tags:
---
### 设置环境变量
```bash
# export 变量名=变量值:变量值
export http_proxy=http://127.0.0.1:8123/
export ALL_PROXY=socks5://127.0.0.1:1086
```
等号前后不能有空格
用冒号分隔多个值

### 删除环境变量
```bash
# unset 变量名
unset http_proxy
unset ALL_PROXY
```
### 修改环境变量

```bash
# 在原有 PATH 上增加
export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>
```
### 查看环境变量
```bash
# 查看某一个，在变量名前加 $ 符
echo $PATH
# 查看所有
env
# 打开配置文件
open ~/.zshrc
```