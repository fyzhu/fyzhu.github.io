---
title: safari setInterval 不准的问题
categories:
  - 未分类
date: 2022-06-07 18:10:20
tags:
---
```js
 
var startTime = new Date().getTime(); 
var count = 0; 
setInterval(function(){ 
  var i = 0; 
  while(i++ < 100000000); 
}, 0); 
function fixed() { 
  count++; 
  var offset = new Date().getTime() - (startTime + count * 1000); 
  var nextTime = 1000 - offset; 
  if (nextTime < 0) nextTime = 0; 
  setTimeout(fixed, nextTime); 

  console.log(new Date().getTime() - (startTime + count * 1000)); 
} 
setTimeout(fixed, 1000); 

```
[参考](https://www.jb51.net/article/49913.htm)