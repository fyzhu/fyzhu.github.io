---
title: fiddler学习笔记
categories:
  - 未分类
date: 2020-05-22 15:23:27
tags:
---
## 1.2 两种模式
1. streaming 流模式 （浏览器模式）实时的
2. buffering 缓冲模式 把所有的数据准备好之后才返回给客户端 可以控制最后的服务器响应


![fiddler 使用场景](https://img4.mukewang.com/5ec780180001c60b12800720.jpg)

```
res.write()
res.end()
```
## 1.3 使用场景
![fiddler 使用场景](https://img2.mukewang.com/5ec781f00001b90b12800720.jpg)

## 2.1 工具条常用功能
1. 备注
2. 重放
3. 清除
4. 调试
5. 模式切换
6. 解析
7. 保持会话
8. 过滤请求（只看chrome）

## 2.2 状态栏操作
1. capturing 是否工作
2. 过滤会话
3. 会话数量
4. 会话详细地址

## 问题
1. 捕获HTTPS（参考教程）
2. 捕获chrome浏览器，安装插件 SwithyOmega
3. 不能捕获js，可能是缓存的问题，勾选禁用缓存

![捕获js](https://img-blog.csdnimg.cn/20190627112123574.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTEwNjg3MDI=,size_16,color_FFFFFF,t_70)

课程地址
https://www.imooc.com/learn/37
教程地址
https://kb.cnblogs.com/page/130367/#introduce