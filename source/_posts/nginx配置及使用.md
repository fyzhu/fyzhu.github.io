---
title: nginx配置及使用
categories:
  - 未分类
date: 2021-07-04 16:52:25
tags:
---
### 配置
401-7-4
![nginx 配置](https://img.mukewang.com/szimg/5fa518a400014c8019201080.jpg)

### 启动
nginx

### 停止
nginx -s stop

### 重载
nginx -s reload

### 检查配置s文件
nginx -t
### 跨域
```
server{
        listen 5000;
        server_name localhost;
        location = / {
            proxy_pass http://localhost:3000/;
        }
        location /test {
            proxy_pass http://localhost:3000/test;

            #   指定允许跨域的方法，*代表所有
            add_header Access-Control-Allow-Methods *;

            #   预检命令的缓存，如果不缓存每次会发送两次请求
            add_header Access-Control-Max-Age 3600;

            #   带cookie请求需要加上这个字段，并设置为true
            add_header Access-Control-Allow-Credentials true;

            #   表示允许这个域跨域调用（客户端发送请求的域名和端口） 
            #   $http_origin动态获取请求客户端请求的域   不用*的原因是带cookie的请求不支持*号
            add_header Access-Control-Allow-Origin $http_origin;

            #   表示请求头的字段 动态获取
            add_header Access-Control-Allow-Headers 
            $http_access_control_request_headers;

            #   OPTIONS预检命令，预检命令通过时才发送请求
            #   检查请求的类型是不是预检命令
            if ($request_method = OPTIONS){
                return 200;
            }
        }
    }
```
参考：https://www.cnblogs.com/PengfeiSong/p/12993446.html

### 导入配置文件
`include servers/*;`
相对于当前文件
### 配置多 server

```
{
    server {
        listen 80;
        server_name a.com;
        location = / {
            proxy_pass http://localhost:3000/;
        }
    }
    server {
        listen 80;
        server_name b.com;
        location = / {
            proxy_pass http://localhost:8000/;
        }
    }
}
```