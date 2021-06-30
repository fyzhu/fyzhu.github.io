---
title: pm2的基本使用
date: 2019-08-25 22:00:49
categories:
  - technology
  - Server
tags:
 - pm2
---
### 初始化
```bash
$ pm2 init
$ pm2 ecosystem
```
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
### 配置文件 
#### js 格式

请注意，使用 js 配置文件要求文件名结尾为 .config.js

例如：ecosystem.config.js
```js
module.exports = {
  apps : [{
    name: 'API',
    script: 'app.js',
    args: 'one two',
    instances: 1,
    autorestart: true,
    watch: false,
    max_memory_restart: '1G',
    env: {
      NODE_ENV: 'development'
    },
    env_production: {
      NODE_ENV: 'production'
    }
  }],

  deploy : {
    production : {
      user : 'node',
      host : '212.83.163.1',
      ref  : 'origin/master',
      repo : 'git@github.com:repo.git',
      path : '/var/www/production',
      'post-deploy' : 'npm install && pm2 reload ecosystem.config.js --env production'
    }
  }
};
```
#### json 格式
例如：process.pord.json

```json
{
    "name": "egg",
    "script": "server.js",
    "cwd": "./",
    "exec_mode": "cluster",
    "watch": false,
    "ignore_watch": [
        "node_modules",
        "logs"
    ],
    "instances": 4,
    "error_file": "logs/err.log",
    "out_file": "logs/out.log",
    "log_date_format": "YYYY-MM-DD HH:mm:ss",
    "env": {
        "NODE_ENV": "production"
    },
    "engines": {
        "node": ">=7.6"
    }
}

```
可以根据需要设置任意多个JSON应用程序声明。
```
{
  "apps": [
      {
      "name": "testOne",
      "script": " testOne/server.js",
      "instances": 1,
      "log_date_format": "YYYY-MM-DD HH:mm Z",
      "max_memory_restart": "500M"
    },
    {
      "name": "testTwo",
      "script": " testTwo/server.js",
      "instances": 1,
      "log_date_format": "YYYY-MM-DD HH:mm Z",
      "max_memory_restart": "500M"
    }
  ]
}
```
启动
```
$ pm2 start process.prod.json
```
#### 常用配置项说明

apps： json结构，apps是一个数组，每一个数组成员就是对应一个pm2中运行的应用；

name：应用程序名称；

cwd：应用程序所在的目录；

script：应用程序的脚本路径；

log_date_format： 指定日志日期格式，如YYYY-MM-DD HH：mm：ss；

error_file：自定义应用程序的错误日志文件，代码错误可在此文件查找；

out_file：自定义应用程序日志文件，如应用打印大量的标准输出，会导致pm2日志过大；

pid_file：自定义应用程序的pid文件；

interpreter：指定的脚本解释器；

interpreter_args：传递给解释器的参数；

exec_mode：应用程序启动模式，支持 fork 和 cluster 模式，默认是 fork；

instances： 应用启动实例个数，仅在 cluster 模式有效；

min_uptime：最小运行时间，这里设置的是60s即如果应用程序在60s内退出，pm2会认为程序异常退出，此时触发重启max_restarts设置数量；

max_restarts：设置应用程序异常退出重启的次数，默认15次（从0开始计数）；

autorestart ：默认为true, 发生异常的情况下自动重启；

cron_restart：定时启动，解决重启能解决的问题；

max_memory_restart：最大内存限制数，超出自动重启；

watch：是否启用监控模式，默认是false。如果设置成true，当应用程序变动时，pm2会自动重载。这里也可以设置你要监控的文件。

ignore_watch：忽略监听的文件夹，支持正则表达式；

merge_logs： 设置追加日志而不是新建日志；

exec_interpreter：应用程序的脚本类型，默认是nodejs；

autorestart：启用/禁用应用程序崩溃或退出时自动重启；

vizion：启用/禁用vizion特性(版本控制)；

env：环境变量，object类型；

force：默认false，如果true，可以重复启动一个脚本。pm2不建议这么做；

restart_delay：异常重启情况下，延时重启时间；

参考：

https://www.cnblogs.com/huiguo/p/12694542.html

https://juejin.im/post/5be406705188256dbb5176f94