---
title: 常用css
categories:
  - 未分类
date: 2020-08-13 17:45:37
tags:
---
### 超出部分显示省略号
```
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```
参考：https://blog.csdn.net/zhumengzj/article/details/80801556
### 三角形
![Triangle Up](https://img.jbzj.com/file_images/article/201310/201310290941121.jpg?201392994443)
```

#triangle-up {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid red;
}

```
![Triangle Top Left](https://img.jbzj.com/file_images/article/201310/201310290942025.jpg?201392994926)
```

#triangle-topleft {
    width: 0;
    height: 0;
    border-top: 100px solid red;
    border-right: 100px solid transparent;
}

```