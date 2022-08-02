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

如果提示 `401 Unauthorized - GET https://registry.npmjs.org/-/whoami`，请先登录

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