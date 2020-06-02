---
title: git的基本使用
categories:
  - 未分类
date: 2020-04-30 15:55:57
tags: git
---
## git show 

## git remote 

## git status

## git diff

## git merge

## git gc

## 创建分支
git branch xxx

## 切换分支
git checkout xxx

## 放弃修改
### 未 add
git checkout -- file
git checkout .
### 已经 add
git reset HEAD file
git reset HEAD .
### 已经 commit 
git reset --hard HEAD^
git reset --hard commitid