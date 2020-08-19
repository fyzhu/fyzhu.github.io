---
title: windows服务器添加远程控制用户
categories:
  - 未分类
date: 2020-08-18 14:27:39
tags:
---
#### 添加用户
两种方式
1. 控制面板-用户帐户-用户帐户-管理其他帐户-添加用户账户
2. 服务器管理器-工具-计算机管理-系统工具-本地用户和组-用户-右键新用户-记得右键设置密码
#### 赋予远程控制组
两种方式
1. 上一步第二种方法直接右键用户选属性-隶属于选项卡-添加 Remote Desktop Users 组
2. 右键这台电脑-属性-更改设置-远程选项卡-选择用户-添加相应用户


参考：
https://blog.csdn.net/zhuge_Spring/article/details/107005114
补充：
ie增强的安全配置如何关闭
https://jingyan.baidu.com/article/ce09321b63a43c2bfe858f5f.html