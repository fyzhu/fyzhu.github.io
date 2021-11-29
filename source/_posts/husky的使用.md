---
title: 新版 husky 的使用
categories:
  - 未分类
date: 2021-06-30 20:08:28
tags:
---
新版 husky 实践

1. 安装 husky  
```bash
npm install -D husky
```
2. 在 packgae.json 中添加 prepare 脚本
```json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```
prepare 脚本会在 npm install（不带参数）之后自动执行。也就是说当我们执行 npm install 安装完项目依赖后会执行 husky install 命令，该命令会创建 .husky/ 目录并指定该目录为 git hooks 所在的目录。

3. 添加 git hooks，运行一下命令创建 git hooks
```
npx husky add .husky/pre-commit "npm run test"
```
运行完该命令后我们会看到.husky/目录下新增了一个名为pre-commit的shell脚本。也就是说在在执行git commit命令时会先执行pre-commit这个脚本。pre-commit脚本内容如下：
```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"
   
npm run test
```
可以看到该脚本的功能就是执行npm run test这个命令


参考：
https://zhuanlan.zhihu.com/p/366786798
