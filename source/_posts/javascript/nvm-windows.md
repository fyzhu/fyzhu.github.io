---
title: nvm-windows踩坑之旅
date: 2020-04-17 11:27:25
tags:
---
### 下载地址
https://github.com/coreybutler/nvm-windows/releases

### 安装路径不要有空格
nvm-windows 对空格支持的不是很好，安装路径最好不要有空格
作者说会在1.1.8这个版本解决这个问题
This issue should be resolved as of version 1.1.8. Please note I'm woefully behind in cutting this new release, but am working on a new release process. In the meantime, it's possible to download the source or use a patched version from https://github.com/s-h-a-d-o-w/nvm-windows/releases (from the person who submitted the fix).

### 使用淘宝镜像
如果用 nvm 安装 node 和 npm 很慢，可以配置 nvm 使用淘宝镜像
nvm node_mirror https://npm.taobao.org/mirrors/node/
nvm npm_mirror https://npm.taobao.org/mirrors/npm/