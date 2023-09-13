---
title: git commit 规范
categories:
  - 未分类
date: 2020-05-18 16:35:00
tags: git
---
## Commit message格式
```
<type>: <subject>
```
注意冒号后面有空格。

### type
用于说明 commit 的类别，只允许使用下面7个标识。

feat：新功能（feature）  
fix：修补 bug  
docs：文档（documentation）  
style：格式 不影响代码含义的改动，例如去掉空格、改变缩进、增删分号  
refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）  
perf：提高性能的改动  
test：增加测试  
chore：构建过程或辅助工具的变动  
ci：与CI（持续集成服务）有关的改动  
如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中。

### subject
subject 是 commit 目的的简短描述，不超过50个字符，且结尾不加句号（.）。
————————————————
版权声明：本文为CSDN博主「行者向阳」的原创文章，遵循CC 4.0 BY-SA版权协议。
原文链接：https://blog.csdn.net/y491887095/java/article/details/80594043

[AngularJS's commit message convention](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)