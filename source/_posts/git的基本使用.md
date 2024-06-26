---
title: git的基本使用
categories:
  - 未分类
date: 2020-04-30 15:55:57
tags: git
---
## branch 与 tag 重名
heads/v21.08  
tags/v21.08

## log
```bash
git log --author=''
git log -p xxx
```
## show 

## remote 
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

## status
检查当前文件状态 
```
git status
git status -s
```

## diff

## rm
移除文件
git rm
## mv
移动文件
git mv
相当于
```
$ mv README.md README
$ git rm README.md
$ git add README
```

## gc

## 分支操作 
### 拉取分支
```bash
git fetch origin xxx

# 以下命令相当于 git pull upstream x.x.x
git fetch upstream x.x.x
git log -p FETCH_HEAD 
git merge FETCH_HEAD
```

### 创建分支
```
git branch xxx
git branch -a
```
### 重命名分支
```bash
# 在当前分支时
git branch -m newName 
# 不在当前分支时
git branch -m oldName  newName
```
### 切换分支
```bash
git checkout xxx
# 创建并切换（远程）分支
git checkout -b dev（本地分支名） origin/dev（远程分支名）
# 在此之前确保有远程分支，git fetch 一下
```
### 合并分支
git merge xxx
### 推送分支
```
git push origin x.x.x
```
### 删除分支
删除本地（先切换到其他分支）
```bash
git branch -d xxx
git branch -D xxx # 强制删除
```
删除远程
```bash
git push origin -d xxx
```
## 暂存修改
```
git stash
git stash pop
git stash list
git stash show
```
[Git(六)：git stash 命令](https://zhuanlan.zhihu.com/p/117553180)
## ！放弃修改
###  untracked files
```
git clean -fd
```
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

```bash
git reset # 默认为 mixed 模式
git reset --soft
git reset --hard HEAD^ # 注意：此操作会丢弃修改
git reset --hard commitid # 注意：此操作会丢弃修改
```
强制提交 reset 操作至远端

```bash
git push -f origin master
```
However, you should avoid doing this if anyone else is working with your remote repository and has pulled your changes.

In that case, it would be better to `revert` the commits that you don't want, then pushing as normal.
```bash
git revert commit_hash
```
## 修改已提交的 commit
### 修改最新的 commit
```
git commit --amend
git commit --amend --reset-author
git commit --amend --reset-author --no-edit
```
### 修改任意一条 commit
git rebase
[juejin](https://juejin.cn/post/6844903806224826375)
[github](https://docs.github.com/en/get-started/using-git/about-git-rebase#an-example-of-using-git-rebase)
## 修改配置信息
```
git config --global --list
git config user.name
git config --global user.email
```
## reset
![git reset from jianshu](https://upload-images.jianshu.io/upload_images/4428238-fcad08ebe26933a6.png?imageMogr2/auto-orient/strip|imageView2/2/w/638/format/webp)
### 不加参数
保留工作目录，并清空暂存区

reset 如果不加参数，那么默认使用 `--mixed` 参数。它的行为是：保留工作目录，并且清空暂存区。也就是说，工作目录的修改、暂存区的内容以及由 reset 所导致的新的文件差异，都会被放进工作目录。简而言之，就是「把所有差异都混合（mixed）放在工作目录中」。

### hard
重置stage区和工作目录
### soft
保留工作目录，并把重置 HEAD 所带来的新的差异放进暂存区
## tag
### 查看
git tag

### 切换
git checkout xxx
### 增加
```
git tag v0.0.1  
git push origin v0.0.1
```
### 删除
```bash
git tag -d v0.0.1  
git push origin -d v0.0.1
git push origin -d heads/v0.0.1 # tag 和 branch 同名
```
## rebase
```bash
git rebase master
```
```bash
# master --- A --- B
git rebase --onto master A B
# 从 A(不包含) 到 B 的部分会被 rebase 到 master
# master 到 A 的部分可以视为被删除了
```
[git-rebase](https://git-scm.com/docs/git-rebase)
[git rebase，看这一篇就够了](https://juejin.cn/post/6969101234338791432)
## cherry-pick

`git cherry-pick` 命令的作用，就是将指定的提交（commit）应用于其他分支。

```bash
$ git cherry-pick <commitHash>
```
Cherry pick 支持一次转移多个提交。
```bash
$ git cherry-pick <HashA> <HashB>
```
上面的命令将 A 和 B 两个提交应用到当前分支。这会在当前分支生成两个对应的新提交。

如果想要转移一系列的连续提交，可以使用下面的简便语法。
```bash
$ git cherry-pick A..B 
```
上面的命令可以转移从 A 到 B 的所有提交。它们必须按照正确的顺序放置：提交 A 必须早于提交 B，否则命令将失败，但不会报错。

注意，使用上面的命令，提交 A 将不会包含在 Cherry pick 中。如果要包含提交 A，可以使用下面的语法。
```bash
$ git cherry-pick A^..B 
```
[git cherry-pick 教程](http://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)
## 参考

[Git 修改已提交的commit注释](https://www.jianshu.com/p/098d85a58bf1)

[Git Reset 三种模式](https://www.jianshu.com/p/c2ec5f06cf1a)

[git 删除本地分支和删除远程分支](https://www.cnblogs.com/liyong888/p/9822410.html)  

[git 分支命名规范](https://www.cnblogs.com/yorkyang/p/9147309.html)

[git commit和issue关联](https://www.jianshu.com/p/f381af75ab85)