---
title: js 代码注释规范
categories:
  - 未分类
date: 2020-06-02 15:55:57
tags: js
---
## 文件注释
```
/*!
 * jRaiser 2 Javascript Library
 * waterfall - v1.0.0 (2013-03-15T14:55:51+0800)
 * http://jraiser.org/ | Released under MIT license
 */
```
## 普通注释
### 单行注释
总是在单行注释符后留一个空格。
```
// this is comment
```
如果某段代码有功能未实现，或者有待完善，必须添加“TODO”标记，“TODO”前后应留一个空格。
```
// TODO 未处理IE6-8的兼容性
function setOpacity(node, val) {
    node.style.opacity = val;
}
```
### 多行注释
总是在多行注释的结束符前留一个空格（使星号对齐）。
```
/*
  this is comment
 */
```
## 文档注释
### 模块注释
```
/**
 * 模块说明
 * @module 模块名
 */
```
### 类注释
```
/**
 * 类说明
 * @class 类名
 * @constructor
 */
```
### 方法注释
```
/**
 * 方法说明
 * @method 方法名
 * @for 所属类名
 * @param {参数类型} 参数名 参数说明
 * @return {返回值类型} 返回值说明
 */
```

https://www.cnblogs.com/chris-oil/p/4067415.html