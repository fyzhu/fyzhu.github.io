---
title: Mac禁止向日葵开机启动
categories:
  - 未分类
date: 2021-06-16 10:15:37
tags:
---
```
cd /Library/LaunchAgents
sudo vim com.oray.sunlogin.agent.plist
sudo vim com.oray.sunlogin.startup.plist

cd /Library/LaunchDaemons
sudo vim com.oray.sunlogin.helper.plist
sudo vim com.oray.sunlogin.plist
```

转载自：https://www.jianshu.com/p/a20efbcc61dd