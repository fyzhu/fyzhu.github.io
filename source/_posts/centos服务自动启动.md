---
title: centos服务自动启动
categories:
  - 未分类
date: 2019-12-24 10:16:57
tags:
---
# 启动服务
## service 命令
`service start/stop/status/restart servicename`

## systemctl 命令

`systemctl start/stop/status/restart servicename`

# 开机启动
## chkconfig 命令
添加到 chkconfig 列表
`chkconfig --add servicename`
开启/关闭
`chkconfig servicename on/off`
查询当前所有自动启动的服务
`chkconfig --list`
查询指定的服务
`chkconfig --list servicename`

## systemctl 命令

`systemctl enable/disable servicename`