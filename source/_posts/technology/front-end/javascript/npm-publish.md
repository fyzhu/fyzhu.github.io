---
title: npm publish
categories:
  - 未分类
date: 2020-06-24 15:03:25
tags:
---

### 创建用户
1. npm 官网创建 
2. npm add user 创建

### 登录

```bash
npm login
```
### 查看当前登录账户



```bash
npm who am i
npm whoami
``` 
### 发布

```bash
npm publish --access=public # 首次发布
npm publish
```
### 删除

npm包发布，通常不建议删除（假如有某某用户已经使用了你的npm包，这时候删除npm包是很没道理的）。

```bash
npm unpublish 依赖包名称 --force
```

### 版本管理
```
npm version prerelease
npm version prepatch
npm version preminor
npm version premajor
npm version patch
npm version minor
npm version major
```

[npm version](https://blog.csdn.net/weixin_40817115/article/details/90384398)

### 常见报错
#### 401
如果提示 `401 Unauthorized - GET https://registry.npmjs.org/-/whoami`，请先登录
#### 403
`403 Forbidden - PUT https://registry.npmjs.org/xxxx - You do not have permission to publish "xxx"`
可能包名冲突
1. 更换包名
2. 添加 scope，如：`@fyzhu/xxx`
#### 402
`402 Payment Required - PUT https://registry.npmjs.org/xxx - You must sign up for private packages`
发私有包需要付费，可以发公共包
```
npm publish --access=public 
```
