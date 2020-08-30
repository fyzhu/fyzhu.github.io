---
title: npm和yarn
date: 2019-08-10 22:14:39
tags:
  - npm
  - yarn
categories:
  - technology
  - front-end
---
## 全局操作

npm 加参数 -g/--global

yarn 加参数 global

## 查看npm包
```
npm list
npm list --depth=0 
npm list --depth=0 --global

yarn list
yarn list global
```
## 安装npm包
```
npm install
npm i

yarn add
```
## 删除npm包
```
npm uninstall <package>

yarn remove <package>
```
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