---
title: docker的基本使用
categories:
  - 未分类
date: 2020-07-03 08:47:04
tags:
---
### docker 命令
1. docker pull 获取 image
2. docker build 创建 image
3. docker images 列出 images
4. docker tag  旧镜像名  新镜像名 
5. docker rmi 删除 image
6. docker commit 保存改动为新的 image
7. docker run 运行 container
8. docker inspect 容器名称 查看容器IP
9. docker ps 列出 containers
10. docker stop 停止 containers
11. docker rm 删除 container
12. docker cp 在 host 和 container 之间拷贝文件
![docker 命令1](https://img.mukewang.com/5efdebd800014a8619201080.jpg)
![docker 命令2](https://img.mukewang.com/5efdec250001eb8419201080.jpg)

### Dockerfile 语法

![Dockerfile 语法1](https://img.mukewang.com/5efdeeec00018f3e19201080.jpg)
![Dockerfile 语法2](https://img.mukewang.com/5efdef1b0001ff5b19201080.jpg)

### 网络
bridge 网络
host 网络

参考：https://www.jb51.net/article/149173.htm