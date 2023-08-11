---
title: docker的基本使用
categories:
  - 未分类
date: 2020-07-03 08:47:04
tags:
---
# docker 命令
## docker pull 
获取 image
## docker build 
创建 image
## docker images 
列出 images
## docker tag  
```bash
docker tag 旧镜像名  新镜像名 
```
## docker rmi 
删除 image
## docker commit 
保存改动为新的 image
## docker run 
运行 container
## docker inspect 
获取容器/镜像的元数据。
```bash
docker inspect 容器名称 查看容器IP
```
## docker ps 
列出运行中的 containers
```bash
docker ps -a #列出所有的 containers
```
## docker start 
启动 containers
## docker stop 
停止 containers
## docker rm 
删除 container
## docker cp 
在 host 和 container 之间拷贝文件

将主机 /www/test 目录拷贝到容器 96f7f14e99ab 的 /www 目录下。
```bash
docker cp /www/test 96f7f14e99ab:/www/
```
将容器 96f7f14e99ab 的 /www 目录拷贝到主机的 /tmp 目录中。
```bash
docker cp  96f7f14e99ab:/www /tmp/
```
![docker 命令1](https://img.mukewang.com/5efdebd800014a8619201080.jpg)
![docker 命令2](https://img.mukewang.com/5efdec250001eb8419201080.jpg)

### Dockerfile 语法

![Dockerfile 语法1](https://img.mukewang.com/5efdeeec00018f3e19201080.jpg)
![Dockerfile 语法2](https://img.mukewang.com/5efdef1b0001ff5b19201080.jpg)

### 网络
bridge 网络
host 网络

参考：https://www.jb51.net/article/149173.htm