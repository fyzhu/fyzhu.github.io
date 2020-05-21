---
title: axios发送application/x-www-form-urlencoded类型的请求
categories:
  - 未分类
date: 2020-05-21 15:02:05
tags:
---
axios 默认发送 json
想要发送 application/x-www-form-urlencoded 类型的数据
可以使用 qs 这个 node module 包
```
import qs from 'qs';
const data = { name:'xxx' , age:'25'};  // 我们传的是 js 对象
const options = {
  method: 'POST',
  headers: { 'content-type': 'application/x-www-form-urlencoded' },
  data: qs.stringify(data),   // 用 qs 将js对象转换为字符串 'name=edward&age=25'
  url: 'http://www.xxx.com'
}; 
axios(options);
```


参考地址：
https://www.cnblogs.com/edwardwzw/p/11694903.html