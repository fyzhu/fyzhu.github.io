---
title: 从setTimeout()函数开始谈起
url: 1.html
id: 1
categories:
  - 技术
date: 2017-08-22 22:10:49
tags:
---

最近在阮一峰老师的网站学习es6，在promise小节下面看到下面的代码，作为小白的我看到这个代码的第一反应是setTimeout怎么有三个参数，上网一查才知道，setTimeout可以跟多个参数，第三个及之后的参数都是第一个参数（函数）的参数
--------------------------------------------------------------------------------------------------------------------------

下面是一个`Promise`对象的简单例子。

    function timeout(ms) {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, ms, 'done');
      });
    }
    
    timeout(100).then((value) => {
      console.log(value);
    });

定义和用法
-----

setTimeout() 方法用于在指定的毫秒数后调用函数或计算表达式。

### 语法

setTimeout(code,millisec)

  1.setTimeout()函数第一个参数

setTimeout(console.log(this),3000);//console.log(this)会立即执行

setTimeout('console.log(this)',3000);//console.log(this)加引号之后3s之后执行

setTimeout(function(){console.log(this)},3000);//console.log(this)3s之后执行

{

function test(){

console.log(this);

}

setTimeout(test,3000);//console.log(this)3s之后执行

}

{

function test(){

console.log(this);

}

setTimeout(test(),3000);//console.log(this)立即执行

}

{

function test(){

console.log(this);

}

setTimeout('test()',3000);//console.log(this)3s之后执行

}

总结：setTimeout里面的函数有三种正确写法 1.用引号引起来，2.放到匿名函数里，3.使用函数名直接调用，不加括号。   2.setTimeout()函数第一个参数this的作用域 参考：http://www.cnblogs.com/hutaoer/p/3423782.html 第一段代码：

var test = "in the window";
 
setTimeout(function() {alert('outer ' + test)}, 0); // 输出 outer in the window ，默认在window的全局作用域下
 
function f() {
 var test = 'in the f!'; // 局部变量，window作用域不可访问
 setTimeout('alert("inner " + test)', 0); // 输出 inner in the window, 虽然在f方法的中调用，但执行代码(字符串形式的代码)默认在window全局作用域下，test也指向全局的test
}
 
f();

第二段代码：

var test = "in the window";
 
setTimeout(function() {alert('outer' + test)}, 0); // outer in the window  ，没有问题，在全局下调用，访问全局中的test
 
function f() {
  var test = 'in the f!';
  setTimeout(function(){alert('inner '+ test)}, 0);  // inner in the f!  有问题，不是说好了执行函数中的this指向的是window吗？那test也应该对应window下                                                      //  的值才对，怎么test的值却是 f()中的值呢？？？？
}
 
f();

第三段代码：

var test = "in the window";

setTimeout(function() {
    alert('outer ' + test)
}, 0); // in the window

function f() {
    var test = 'in the f!';

    function ff() {
        alert('inner ' + test);// 能访问到f中的test局部变量
        alert('inner ' + this.test);//window中的test
    } 

    setTimeout(ff, 0); // inner in the f!
}

f();

  总结： 三种写法中， 1引号引起来的函数中的this指向和变量作用域都是window， 2匿名函数中的变量作用域是上下文，this指向是window， 3以函数名直接调用中的变量作用域是上下文，this指向是window。 第2和第3其实是一种写法，不同形式。 其实匿名函数中this应该指向词法作用域，这是javascript的一个错误，在箭头函数中已经修复了这个错误。   3.箭头函数中的this作用域 参考：https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001438565969057627e5435793645b7acaee3b6869d1374000