---
title: react hooks
categories:
  - 未分类
date: 2021-01-13 19:54:28
tags:
---
函数式编程将那些跟数据计算无关的操作，都称为 "副效应" （side effect） 。如果函数内部直接包含产生副效应的操作，就不再是纯函数了，我们称之为不纯的函数。
钩子（hook）就是 React 函数组件的副效应解决方案
### useState
### useEffect
第一个参数是一个函数
第二个参数是一个数组（数组里的有一项变化就执行）（两个特例，1，不传。2，传一个空数组）

useEffect()的作用就是指定一个副效应函数，组件每渲染一次，该函数就自动执行一次。组件首次在网页 DOM 加载后，副效应函数也会执行。
1. 提高了代码复用（不用在mount和update里都写一遍函数）
2. 优化了关注点分离（业务逻辑都在各自的useEffect里，互不干扰）

只要是副效应，都可以使用useEffect()引入。它的常见用途有下面几种。

1. 获取数据（data fetching）
2. 事件监听或订阅（setting up a subscription）
3. 改变 DOM（changing the DOM）
4. 输出日志（logging）
![](https://img.mukewang.com/szimg/5ffedfaf00018a9919201080.jpg)
![副作用调用时机](https://img.mukewang.com/szimg/5ffee027000174c919201080.jpg)
![](https://img.mukewang.com/szimg/5ffee08c0001a6ae19201080.jpg)

参考：
http://www.ruanyifeng.com/blog/2020/09/react-hooks-useeffect-tutorial.html