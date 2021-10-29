---
title: vscode 调试 js
categories:
  - 未分类
date: 2021-10-29 17:09:53
tags:
---
### 调试 npm script 命令
注意：此为 configurations 中的一条配置，具体看下一条
```json
{
  "name": "Launch via NPM",
  "type": "node",
  "request": "launch",
  "runtimeExecutable": "npm", //runtimeExecutable表示要使用的运行时，默认为node，这里我们配置成了npm
  "runtimeArgs": [
    "run-script", "dev"    //这里的dev就对应package.json中的scripts中的dev
  ],
  "port": 9229    //这个端口是调试的端口，不是项目启动的端口
},
```

### 调试指定 js 文件
```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "pwa-node",
      "request": "launch",
      "name": "Launch Program",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "program": "${workspaceFolder}/test/filelist.js"
    }
  ]
}

```
### 使用 nodemon 调试



参考：
https://www.cnblogs.com/little-ab/p/11796952.html