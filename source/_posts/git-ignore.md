---
title: 'git如何忽略已经加入版本控制的文件'
date: 2019-07-20 09:28:32
tags: 
  - git
---
如果文件已经加入版本控制，再加入.gitignore文件也还是会提交到版本控制。
这时需要首先确保文件已经加入.gitignore文件
然后使用如下命令：
1. 文件
```
git rm --cached filename
```
2. 文件夹
```
git rm -r --cached foldername
```