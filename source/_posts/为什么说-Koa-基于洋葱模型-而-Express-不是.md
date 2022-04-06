---
title: '为什么说 Koa 基于洋葱模型,而 Express 不是'
categories:
  - 未分类
date: 2022-04-06 19:12:48
tags:
---
最近看光哥的文章，说 Express 是洋葱圈模型。我记得 Koa 是洋葱圈模型，而且这是其与 Express 不同的地方之一。  
于是搜索引擎搜索了一通，只有说 Koa 是洋葱圈模型的，没有说 Express 是洋葱圈模型的。  
而且一般都会提供下面的代码证明 Koa 是洋葱圈模型。
```js
// koa-app.js
 
const Koa = require('koa2');
const app = new Koa();
 
app.use(async (ctx, next) => {
  console.log('第一层洋葱 - 开始')
  await next();
  console.log('第一层洋葱 - 结束')
});
 
app.use(async (ctx, next) => {
  console.log('第二层洋葱 - 开始')
  await next();
  console.log('第二层洋葱 - 结束')
});
 
app.use(async ctx => {
  console.log('第三层洋葱 - 开始')
  ctx.body = 'Hello World';
  console.log('第三层洋葱 - 结束')
});

app.listen(3000)
```
控制台打印如下
```
第一层洋葱 - 开始
  第二层洋葱 - 开始
    第三层洋葱 - 开始
    第三层洋葱 - 结束
  第二层洋葱 - 结束
第一层洋葱 - 结束
```
看样子真像那么回事

于是我用 Express 试了一下
```js
var express = require("express");
var app = express();

app.use((req, res, next) => {
  console.log('第一层洋葱 - 开始');
  next();
  console.log('第一层洋葱 - 结束');
});
app.use((req, res, next) => {
  console.log('  第二层洋葱 - 开始');
  next();
  console.log('  第二层洋葱 - 结束');
});
app.use((req, res, next) => {
  console.log('    第三层洋葱 - 开始');
  next();
  console.log('    第三层洋葱 - 结束');
});

app.listen(3000);

```
控制台打印和 koa 的例子是一样的  
什么，难道 Express 也是洋葱模型

其实，以上例子并不能说明 Koa 是洋葱圈模型，洋葱圈模型的关键是，在`请求返回之前`，你的请求是不是经过中间件两次，而且按照先进后出的顺序。

Koa 模型  
进洋葱 -> 出洋葱 -> 返回请求  
Express 模型  
进洋葱 -> 返回请求 -> 出洋葱

以下代码才真正能体现 Koa 的洋葱模型
```js
const Koa = require("koa2");
const app = new Koa();
const indent = (n) => new Array(n).join("&nbsp;");
app.use(async (ctx, next) => {
  ctx.body = "<h3>第一层洋葱 - 开始</h3>";
  await next();
  ctx.body += "<h3>第一层洋葱 - 结束</h3>";
});

app.use(async (ctx, next) => {
  ctx.body += `<h3>${indent(4)}第二层洋葱 - 开始</h3>`;
  await next();
  ctx.body += `<h3>${indent(4)}第二层洋葱 - 结束</h3>`;
});

app.use(async (ctx, next) => {
  ctx.body += `<h3>${indent(8)}第三层洋葱 - 开始</h3>`;
  next();
  ctx.body += `<h3>${indent(8)}第三层洋葱 - 结束</h3>`;
});
app.use((ctx) => {
  ctx.body += `<h3>${indent(12)}koa 核心业务</h3>`;
});

app.listen(3000);

```
浏览器显示结果


```
第一层洋葱 - 开始
   第二层洋葱 - 开始
       第三层洋葱 - 开始
           koa 核心业务
       第三层洋葱 - 结束
   第二层洋葱 - 结束
第一层洋葱 - 结束
```

```js
var express = require("express");
var app = express();

const indent = (n) => new Array(n).join("&nbsp;");

app.use((req, res, next) => {
  res.body = "<h3>第一层洋葱 - 开始</h3>";
  next();
  res.body += "<h3>第一层洋葱 - 结束</h3>";
});
app.use((req, res, next) => {
  res.body += `<h3>${indent(4)}第二层洋葱 - 开始</h3>`;
  next();
  res.body += `<h3>${indent(4)}第二层洋葱 - 结束</h3>`;
});
app.use((req, res, next) => {
  res.body += `<h3>${indent(8)}第三层洋葱 - 开始</h3>`;
  next();
  res.body += `<h3>${indent(8)}第三层洋葱 - 结束</h3>`;
});
app.use((req, res) => {
  res.body += `<h3>${indent(12)}核心业务</h3>`;
  res.send(res.body);
});
app.listen(3000);

```
浏览器显示
```
第一层洋葱 - 开始
   第二层洋葱 - 开始
       第三层洋葱 - 开始
           核心业务
```