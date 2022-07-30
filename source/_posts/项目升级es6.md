---
title: 项目升级es6
categories:
  - 未分类
date: 2022-07-30 23:47:36
tags:
---
本文主要记录 require 升级为 import 遇到的问题

## __dirname is not defined in ES module scope
```js
import path from 'path';
import {fileURLToPath} from 'url';

const __filename = fileURLToPath(import.meta.url);

// 👇️ "/home/john/Desktop/javascript"
const __dirname = path.dirname(__filename);
console.log('directory-name 👉️', __dirname);

// 👇️ "/home/borislav/Desktop/javascript/dist/index.html"
console.log(path.join(__dirname, '/dist', 'index.html'));

```
## import json file
```js
import json from "./foo.json" assert { type: "json" };
import("foo.json", { assert: { type: "json" } });
```
  
## import 条件导入
```js
if (condition) { // 报错
  import moduleA from './moduleA';
}

```
### import 函数
```js
import('./moduleA .js')
.then(moduleA => {
  console.log(moduleA);
});

```
```js
if(condition){
 import('moduleA').then(...);
}

```