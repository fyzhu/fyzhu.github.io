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

常用
git remote add origin git@xxx.com:/home/git/test.git
```

## 检查当前文件状态 
```
git status
git status -s
```

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

## git gc

## 分支操作
### 拉取分支
git fetch origin
### 创建分支
```
git branch xxx
git branch -a
```
### 切换分支
```js
git checkout xxx
// 创建并切换（远程）分支
git checkout -b dev（本地分支名） origin/dev（远程分支名）
// 在此之前确保有远程分支，git fetch 一下
```
### 合并分支
git merge xxx

## 暂存修改
```
git stash
git stash pop
```
## 放弃修改
### 未 add，撤消对文件的修改
```
git checkout -- file
git checkout .
```
### 已经 add，取消暂存的文件
```
git reset HEAD file
git reset HEAD .
```
### 已经 commit 
注意：此操作会丢弃修改
```
git reset --hard HEAD^
git reset --hard commitid
```
## 修改已提交的commit
```
git commit --amend
```
## 修改配置信息
```
git config user.name
git config --global user.email
```
参考：https://www.jianshu.com/p/098d85a58bf1