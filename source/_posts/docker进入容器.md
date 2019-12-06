---
title: docker进入容器
categories:
  - technology
  - Server
date: 2019-12-06 16:45:59
tags:
  - docker
---
```
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

OPTIONS说明：

-d :分离模式: 在后台运行

-i :即使没有附加也保持STDIN 打开

-t :分配一个伪终端
```
docker exec -it 1f2f04275f80 redis-cli
```