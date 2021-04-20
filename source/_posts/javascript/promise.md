---
title: promise如何解决回调地狱
categories:
  - technology
  - front-end
date: 2021-02-24
tags:
---
### promise如何解决回调地狱

![image-20210224154744243](C:\Users\Yvan\AppData\Roaming\Typora\typora-user-images\image-20210224154744243.png)

### promise 的状态

一般 Promise 在执行过程中，必然会处于以下几种状态之一。

1. 待定（pending）：初始状态，既没有被完成，也没有被拒绝。

2. 已完成（fulfilled）：操作成功完成。

3. 已拒绝（rejected）：操作失败。

### promise 的方法

#### all

**语法：** Promise.all（iterable）

**参数：** 一个可迭代对象，如 Array。

**描述：** 此方法对于汇总多个 promise 的结果很有用，在 ES6 中可以将多个 Promise.all 异步请求并行操作，返回结果一般有下面两种情况。

1. 当所有结果成功返回时按照请求顺序返回成功。
2. 当其中有一个失败方法时，则进入失败方法。

#### allSettled

Promise.allSettled 的语法及参数跟 Promise.all 类似，其参数接受一个 Promise 的数组，返回一个新的 Promise。唯一的不同在于，执行完之后不会失败，也就是说当 Promise.allSettled 全部处理完成后，我们可以拿到每个 Promise 的状态，而不管其是否处理成功。

```javascript
const resolved = Promise.resolve(2);

const rejected = Promise.reject(-1);

const allSettledPromise = Promise.allSettled([resolved, rejected]);

allSettledPromise.then(function (results) {

  console.log(results);

});

// 返回结果：

// [

//    { status: 'fulfilled', value: 2 },

//    { status: 'rejected', reason: -1 }

// ]

```



#### anny

**语法：** Promise.any（iterable）

**参数：** iterable 可迭代的对象，例如 Array。

**描述：** any 方法返回一个 Promise，只要参数 Promise 实例有一个变成 fulfilled 状态，最后 any 返回的实例就会变成 fulfilled 状态；如果所有参数 Promise 实例都变成 rejected 状态，包装实例就会变成 rejected 状态。

```js
const resolved = Promise.resolve(2);

const rejected = Promise.reject(-1);

const allSettledPromise = Promise.any([resolved, rejected]);

allSettledPromise.then(function (results) {

  console.log(results);

});

// 返回结果：

// 2

```



#### race

**语法：** Promise.race（iterable）

**参数：** iterable 可迭代的对象，例如 Array。

**描述：** race 方法返回一个 Promise，只要参数的 Promise 之中有一个实例率先改变状态，则 race 方法的返回状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给 race 方法的回调函数。

我们来看一下这个业务场景，对于图片的加载，特别适合用 race 方法来解决，将图片请求和超时判断放到一起，用 race 来实现图片的超时判断。请看代码片段。

```js
//请求某个图片资源

function requestImg(){

  var p = new Promise(function(resolve, reject){

    var img = new Image();

    img.onload = function(){ resolve(img); }

    img.src = 'http://www.baidu.com/img/flexible/logo/pc/result.png';

  });

  return p;

}

//延时函数，用于给请求计时

function timeout(){

  var p = new Promise(function(resolve, reject){

    setTimeout(function(){ reject('图片请求超时'); }, 5000);

  });

  return p;

}

Promise.race([requestImg(), timeout()])

.then(function(results){

  console.log(results);

})

.catch(function(reason){

  console.log(reason);

});	
```





