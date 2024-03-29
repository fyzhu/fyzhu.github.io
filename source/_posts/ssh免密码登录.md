---
title: ssh免密码登录
categories:
  - 未分类
date: 2019-12-27 14:39:37
tags:
---
查看服务器和本地是否存在密钥，
密钥存放目录一般为当前用户家目录下的.ssh里  
windows：

`C:\Users\***\.ssh`  

linux：

`/***/.ssh` 一般为： `/root/.ssh`  

如果没有，创建密钥  
```bash
ssh-keygen -t rsa # 一直默认回车就可以
ssh-keygen -t ed25519 -C "your@email.com" # github 等仓库
```
## 终端下 ssh 命令登录
把本地公钥添加到服务器的 .ssh/authorized_key 里  
> 如果没有 `authorized_key` 这个文件，手动创建  

### 手动 copy
#### Windows Command Line
```bash
type %userprofile%\.ssh\id_ed25519.pub | clip
```
#### Git Bash on Windows / Windows PowerShell:

```bash
cat ~/.ssh/id_ed25519.pub | clip
```
#### macOS
```bash
pbcopy < ~/.ssh/<YOUR KEY>.pub
```
#### GNU/Linux (requires the xclip package):
```bash
xclip -sel clip < ~/.ssh/id_ed25519.pub
```
### 命令 copy

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub root@xxx.com
```

ssh root@ip 就可以免密码登录了

## 使用 xshell 等 ssh 工具登录
1. 把服务器的公钥下载到本地
2. 登录时需要填写用户名 (root)
3. 选择登录方式为public Key
4. 选择第一步下载的公钥

[参考](https://cloud.tencent.com/developer/article/1780788)