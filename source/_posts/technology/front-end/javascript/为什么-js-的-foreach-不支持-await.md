---
title: 为什么 js 的 forEach 不支持 await
categories:
  - technology
  - front-end
  - js
date: 2022-01-27 17:49:15
tags:
---
## 问题

为什么 forEach 不行，而 普通 for 循环 和 for…of 却正常呢？

我们得先从 [forEach 的源码](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#polyfill) 看起：
```js
// Production steps of ECMA-262, Edition 5, 15.4.4.18
// Reference: http://es5.github.io/#x15.4.4.18
if (!Array.prototype.forEach) {

  Array.prototype.forEach = function(callback/*, thisArg*/) {

    var T, k;

    if (this == null) {
      throw new TypeError('this is null or not defined');
    }

    // 1. Let O be the result of calling toObject() passing the
    // |this| value as the argument.
    var O = Object(this);

    // 2. Let lenValue be the result of calling the Get() internal
    // method of O with the argument "length".
    // 3. Let len be toUint32(lenValue).
    var len = O.length >>> 0;

    // 4. If isCallable(callback) is false, throw a TypeError exception. 
    // See: http://es5.github.com/#x9.11
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    // 5. If thisArg was supplied, let T be thisArg; else let
    // T be undefined.
    if (arguments.length > 1) {
      T = arguments[1];
    }

    // 6. Let k be 0.
    k = 0;

    // 7. Repeat while k < len.
    while (k < len) {

      var kValue;

      // a. Let Pk be ToString(k).
      //    This is implicit for LHS operands of the in operator.
      // b. Let kPresent be the result of calling the HasProperty
      //    internal method of O with argument Pk.
      //    This step can be combined with c.
      // c. If kPresent is true, then
      if (k in O) {

        // i. Let kValue be the result of calling the Get internal
        // method of O with argument Pk.
        kValue = O[k];

        // ii. Call the Call internal method of callback with T as
        // the this value and argument list containing kValue, k, and O.
        callback.call(T, kValue, k, O);
      }
      // d. Increase k by 1.
      k++;
    }
    // 8. return undefined.
  };
}
```
摘抄最重要的部分：

```js
/* 
O 为传入数组
len 为传入数组长度
callback 为传入回调函数
*/
while (k < len) {
  var kValue; 
  if (k in O) { 
    kValue = O[k]; 
    callback.call(T, kValue, k, O);
  } 
  k++;
}
```
可以看到 `callback.call(T, kValue, k, O);` 这一句，callback 其实是我们传入的一个被 async 封装的 promise 对象，而 Array.prototype.forEach 内部并未对这个 promise 对象做任何处理，只是忽略它。

## 解决方案

如果我们尝试把 Array.prototype.forEach 改造一下，让它不要忽视，就可以达到效果了，如下：

 ```js
Array.prototype.forEach = async function(callback/*, thisArg*/) {
  // ………
  await callback.call(T, kValue, k, O);
  // ………
};
```

你总不能去侵入式的改造Array.prototype.forEach吧！所以最简单的办法就是抛弃 forEach，使用 for…of 或者 for 循环！

## [参考](https://www.cnblogs.com/xjnotxj/p/10629900.html)