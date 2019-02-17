---
title: 纯CSS绘制三角形（各种角度）
url: 143.html
id: 143
categories:
  - 技术
  - 前端
date: 2018-01-10 11:12:49
tags:
---

CSS三角形绘制方法，学会了这个，其它的也就简单。

我们的网页因为 CSS 而呈现千变万化的风格。这一看似简单的样式语言在使用中非常灵活，只要你发挥创意就能实现很多比人想象不到的效果。特别是随着 CSS3 的广泛使用，更多新奇的 CSS 作品涌现出来。 今天给大家带来 CSS 三角形绘制方法 ![](http://files.jb51.net/file_images/article/201310/201310290941121.jpg?201392994443)

复制代码代码如下:

#triangle-up { width: 0; height: 0; border-left: 50px solid transparent; border-right: 50px solid transparent; border-bottom: 100px solid red; }

![](http://files.jb51.net/file_images/article/201310/201310290941322.jpg?201392994757)

复制代码代码如下:

#triangle-down { width: 0; height: 0; border-left: 50px solid transparent; border-right: 50px solid transparent; border-top: 100px solid red; }

![](http://files.jb51.net/file_images/article/201310/201310290941433.jpg?201392994835)

复制代码代码如下:

#triangle-left { width: 0; height: 0; border-top: 50px solid transparent; border-right: 100px solid red; border-bottom: 50px solid transparent; }

![](http://files.jb51.net/file_images/article/201310/201310290941534.jpg?20139299495)

复制代码代码如下:

#triangle-right { width: 0; height: 0; border-top: 50px solid transparent; border-left: 100px solid red; border-bottom: 50px solid transparent; }

![](http://files.jb51.net/file_images/article/201310/201310290942025.jpg?201392994926)

复制代码代码如下:

#triangle-topleft { width: 0; height: 0; border-top: 100px solid red; border-right: 100px solid transparent; }

![](http://files.jb51.net/file_images/article/201310/201310290942136.jpg?201392994948)

复制代码代码如下:

#triangle-topright { width: 0; height: 0; border-top: 100px solid red; border-left: 100px solid transparent; }

![](http://files.jb51.net/file_images/article/201310/201310290942227.jpg?20139299509)

复制代码代码如下:

#triangle-bottomleft { width: 0; height: 0; border-bottom: 100px solid red; border-right: 100px solid transparent; }

![](http://files.jb51.net/file_images/article/201310/201310290942328.jpg?201392995028)

复制代码代码如下:

#triangle-bottomright { width: 0; height: 0; border-bottom: 100px solid red; border-left: 100px solid transparent; }

转载自http://www.jb51.net/article/42513.htm