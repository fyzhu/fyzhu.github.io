---
title: JS 类
categories:
  - technology
  - front-end
date: 2021-03-10
tags:
---
### es5 与 es6 类的区别

1. es5 类定义的方法是可枚举的，es6 类定义的方法不可枚举
2. es5 构造函数可以作为函数单独执行，es6 类不可以单独执行，必须使用 new 关键字
3. es6 类不存在变量提升（hoist），这一点与 ES5 完全不同。

类的 get 和 set 

存值函数和取值函数是设置在属性(访问器属性)的 Descriptor 对象上的

```js
class CustomHTMLElement {
  constructor(element) {
    this.element = element;
  }

  get html() {
    return this.element.innerHTML;
  }

  set html(value) {
    this.element.innerHTML = value;
  }
}

var descriptor = Object.getOwnPropertyDescriptor(
  CustomHTMLElement.prototype, "html"
);

"get" in descriptor  // true
"set" in descriptor  // true
```

