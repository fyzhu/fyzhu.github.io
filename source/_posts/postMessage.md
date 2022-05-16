---
title: postMessage
categories:
  - 未分类
date: 2022-05-16 22:31:06
tags:
---
postMessage 可用于解决以下方面的问题：

1. 页面和其打开的新窗口的数据传递
2. 页面与嵌套的 iframe 消息传递
3. 多窗口之间消息传递

## 发送
```js
otherWindow.postMessage(message, targetOrigin, [transfer]);
```
otherWindow

其他窗口的一个引用，比如 iframe 的 contentWindow 属性、执行 window.open 返回的窗口对象、或者是命名过或数值索引的 window.frames。

message

要发送的数据。它将会被结构化克隆算法序列化，所以无需自己序列化（部分低版本浏览器只支持字符串，所以发送的数据最好用JSON.stringify() 序列化）。

targetOrigin

通过 targetOrigin 属性来指定哪些窗口能接收到消息事件，其值可以是字符串“*”（表示无限制）或者一个 URI（如果要指定和当前窗口同源的话可设置为"/"）。在发送消息的时候，如果目标窗口的协议、主机地址或端口号这三者的任意一项不匹配 targetOrigin 提供的值，那么消息就不会发送。
## 接收
```js
window.addEventListener("message", (event)=>{
   var origin = event.origin;
   // 通常，onmessage()事件处理程序应当首先检测其中的origin属性，忽略来自未知源的消息
   if (origin !== "http://example.org:8080")
     return;
   // ...
}, false);
```
event 的属性有：

- data: 从其他 window 传递过来的数据副本。 
- origin: 调用 postMessage 时，消息发送窗口的 origin。例如：“http://example.com:8080”。
- source: 对发送消息的窗口对象的引用。可以使用此来在具有不同 origin 的两个窗口之间建立双向数据通信。 


————————————————  
版权声明：本文为CSDN博主「huangpb0624」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。  
原文链接：https://blog.csdn.net/huangpb123/article/details/83692019