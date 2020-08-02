---
title: git的基本使用
categories:
  - 未分类
date: 2020-04-30 15:55:57
tags: git
---
## git show 

## git remote 
```
git remote [-v | --verbose]
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=<fetch|push>] <name> <url>
git remote rename <old> <new>
git remote remove <name>
git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
git remote set-branches [--add] <name> <branch>…​
git remote get-url [--push] [--all] <name>
git remote set-url [--push] <name> <newurl> [<oldurl>]
git remote set-url --add [--push] <name> <newurl>
git remote set-url --delete [--push] <name> <url>
git remote [-v | --verbose] show [-n] <name>…​
git remote prune [-n | --dry-run] <name>…​
git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)…​]
```

## 检查当前文件状态 
git status
git status -s

## git diff

## 移除文件
git rm
## 移动文件
git mv
相当于
```
$ mv README.md README
$ git rm README.md
$ git add README
```
## git merge

## git gc

## 创建分支
git branch xxx

## 切换分支
git checkout xxx

## 放弃修改
### 未 add，撤消对文件的修改
git checkout -- file
git checkout .
### 已经 add，取消暂存的文件
git reset HEAD file
git reset HEAD .
### 已经 commit 
git reset --hard HEAD^
git reset --hard commitid

## 修改已提交的commit
git commit --amend

参考：https://www.jianshu.com/p/098d85a58bf1