---
title: pm2的基本使用
date: 2019-08-25 22:00:49
categories:
  - technology
  - Server
tags:
 - pm2
---
### 启动
```bash
# start命令启动对应的node server文件
$ pm2 start ./build/server.js --name alisaname
```
参数
`--name`
`--watch`
启动npm命令
```bash
$ pm2 start npm --name "xxx" -- run start/dev
```

### 查看所有启动的进程列表
```
$ pm2 list
```
### 查看详细状态信息
```
$ pm2 show  <appname>/<id>
```
### 监控某个 node 进程的 cpu 和内存使用情况
```
$ pm2 monit <appname>/<id>
```
### 显示某个进程的信息
```
$ pm2 info <appname>/<id>
```
### 显示某个进程的日志
```
$ pm2 log <appname>/<id>
```
### 显示所有进程的日志信息
```
$ pm2 logs
```
### 监控运行这些进程的机器的状态
```
$ pm2 web
```
### 停止 指定/所有 进程
```
$ pm2 stop <appname>/<id>
$ pm2 stop all

```
### 重启 指定/所有 进程
```
$ pm2 restart <appname>/<id>
$ pm2 restart all
```
### 杀死 指定/所有 进程
```
$ pm2 delete <appname>/<id>
$ pm2 delete all
```
### 清空日志
```
$ pm2 flush
```
### 其他命令
```bash
$ pm2 update # Save processes, kill PM2 and restore processes
$ pm2 save # 保存当前应用列表
```
### 配置文件 process.pord.json
```
{
    "name": "egg",
    "script": "server.js",
    "cwd": "./",
    "exec_mode": "fork",
    "watch": false,
    "ignore_watch": [
        "node_modules",
        "logs"
    ],
    "instances": 4,
    "error_file": "logs/err.log",
    "out_file": "logs/out.log",
    "log_date_format": "YYYY-MM-DD HH:mm:ss"
    "env": {
        "NODE_ENV": "production"
    },
    "engines": {
        "node": ">=7.6"
    }
}
$ pm2 start process.prod.json
```
转载自https://juejin.im/post/5be406705188256dbb5176f94