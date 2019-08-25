---
title: pm2的使用
date: 2019-08-25 22:00:49
tags:
 - pm2
---
#### 启动
```
// start命令启动对应的node server文件
$ pm2 start ./build/server.js --name alisaname

```
#### 查看详细状态信息
```
$ pm2 show  (appname|id)
```
#### 查看所有启动的进程列表
```
$ pm2 list
```
#### 监控每个 node 进程的 cpu 和内存使用情况
```
$ pm2 monit
```
#### 显示所有进程的日志信息
```
$ pm2 logs
```
#### 监控运行这些进程的机器的状态
```
$ pm2 web
```
#### 停止 指定/所有 进程
```
// 停止id为0的进程
$ pm2 stop 0
// 停止所有进程
$ pm2 stop all

```
#### 重启 指定/所有 进程
```
// 重启id为0的进程
$ pm2 restart 0
// 重启所有进程
$ pm2 restart all
```
#### 杀死 指定/所有 进程
```
// 杀死id为0的进程
$ pm2 delete 0
// 杀死所有进程
$ pm2 delete all
```

转载自https://juejin.im/post/5be406705188256dbb5176f9