---
title: npm和yarn和pnpm
date: 2019-08-10 22:14:39
tags:
  - npm
  - yarn
  - pnpm
categories:
  - technology
  - front-end
---
## 全局操作

npm 加参数 -g/--global

yarn 加参数 global

## 查看已安装 npm 包
```
npm ls/list
npm ls/list xxx
npm list --depth=0 
npm list --depth=0 --global

yarn list
yarn list xxx
yarn global list 
```
## 查看 npm 包版本
```bash
npm info xxx 
npm view xxx version # 最新版本
npm view xxx versions # 所有已发布版本
```
## 安装npm包
```
npm install
npm i

yarn add

pnpm i
```
## 删除npm包
```
npm uninstall <package>

yarn remove <package>
```
## 查看可升级的包
```
npm outdated
```

黄色表示不符合我们指定的语意化版本范围 - 不需要升级

红色表示符合指定的语意化版本范围 - 需要升级
## 更新npm包
```
npm install <package>@latest
npm update <package>

yarn add <package>
yarn upgrade <package> --latest
```
## 配置镜像
```
npm config set registry https://registry.npm.taobao.org

yarn config set registry https://registry.npm.taobao.org -g

yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g
```
## 查看安装过程
```
npm i --timing=true --loglevel=verbose

yarn --verbose
```
