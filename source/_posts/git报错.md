---
title: git报错The following untracked working tree files would be overwritten by checkout
categories:
  - technology
date: 2019-12-04 14:30:24
tags:
  - git
---
解决方式：
```
git clean -d -fx
```
删除 一些 没有 git add 的 文件；

git clean 参数 

    -n 显示将要删除的文件和目录；

    -x -----删除忽略文件已经对git来说不识别的文件

    -d -----删除未被添加到git的路径中的文件

    -f -----强制运行

转载自：https://blog.csdn.net/u013452337/article/details/81360210