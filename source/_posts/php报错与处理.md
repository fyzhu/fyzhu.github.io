---
title: php报错与处理
categories:
  - 未分类
date: 2020-07-03 11:19:12
tags: php
---

1. failed to open stream: Permission denied

可能原因：没有目录权限
解决方案：更改目录所有者为www
```
# chown -R www:www folername
```
2. failed to open stream: No such file or directory

```
# composer install
```

