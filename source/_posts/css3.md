---
title: CSS3
url: 85.html
id: 85
categories:
  - 技术
  - 前端
date: 2017-09-27 12:33:52
tags:
---

一、边框 
border-radius:100%; 
box-shadow:x偏移量，y偏移量，阴影模糊，阴影扩展，颜色，内外 
border-image:url() 70 repeat; 
二、颜色相关 
rgba    如：background:rgba(255,255,255,0.5); 
颜色渐变（线性渐变（linear）、**径向渐变(radial)**） 线性渐变 linear-gradient(方向，颜色（两个至多个）） 
例如：background-image:linear-gradient(to right,red,orange,yellow,green,blue,indigo,violet); 
三、文字与字体 
文本溢出text-overflow **text-overflow**只是用来说明文字溢出时用什么方式显示，要实现溢出时产生**省略号**的效果，还须定义**强制文本在一行内显示**（white-space:nowrap）及**溢出内容为隐藏**（overflow:hidden），只有这样才能实现**溢出文本显示省略号**的效果，代码如下：
```css
text-overflow: ellipsis; 
overflow: hidden; 
white-space: nowrap;
```

同时，**word-wrap**也可以用来设置**文本行为**，当前行超过指定容器的边界时是否断开转行。 嵌入字体@font-face 
例如 @font-face { font-family: "MOOC Font"; src: url("http://www.imooc.com/Amaranth-BoldItalic.otf"); } 直接使用font-family: "MOOC Font";   text-shadow: X-Offset Y-Offset blur color;

X-Offset：表示阴影的水平偏移距离，其值为正值时阴影向右偏移，反之向左偏移；

Y-Offset：是指阴影的垂直偏移距离，如果其值是正值时，阴影向下偏移，反之向上偏移；

Blur：是指阴影的模糊程度，其值不能是负值，如果值越大，阴影越模糊，反之阴影越清晰，如果不需要阴影模糊可以将Blur值设置为0；

Color：是指阴影的颜色，其可以使用rgba色。

四、与背景相关的样式
----------

background-origin
-----------------

设置元素背景图片的**原始起始位置**。 语法：

background-origin ： border-box | padding-box | content-box;

参数分别表示背景图片是从**边框**，还是**内边距（默认值）**，或者是**内容区域**开始显示。

background-clip
---------------

用来将背景图片做适当的**裁剪**以适应实际需要。 语法：

background-clip ： border-box | padding-box | content-box | no-clip

参数分别表示从**边框、**或**内填充**，或者**内容区域**向外裁剪背景。**no-clip**表示不裁切，和**参数border-box**显示同样的效果。`backgroud-clip`默认值为**border-box**。

 background-size
----------------

设置背景图片的大小，以**长度值**或**百分比**显示，还可以通过**cover**和**contain**来对图片进行伸缩。 语法：

background-size: auto | <长度值> | <百分比> | cover | contain

取值说明： **1、auto**：默认值，不改变背景图片的原始高度和宽度； **2、<长度值>**：成对出现如200px 50px，将背景图片宽高依次设置为前面两个值，当设置一个值时，将其作为图片宽度值来**等比缩放**； **3、<百分比>**：0％~100％之间的任何值，将背景图片宽高依次设置为所在元素宽高乘以前面百分比得出的数值，当设置一个值时同上； **4、cover**：顾名思义为**覆盖**，即将背景图片等比缩放以**填满整个容器**； **5、contain**：容纳，即将背景图片等比缩放至**某一边紧贴容器边缘为止**。

multiple backgrounds
--------------------

多重背景，也就是CSS2里**background**的属性外加**origin**、**clip**和**size**组成的新background的多次叠加，缩写时为用**逗号**隔开的每组值；用分解写法时，如果有多个背景图片，而其他属性只有一个（例如background-repeat只有一个），表明所有背景图片应用该属性值。 语法缩写如下：

background ： \[background-color\] | \[background-image\] | \[background-position\]\[/background-size\] | \[background-repeat\] | \[background-attachment\] | \[background-clip\] | \[background-origin\],...

**注意：**

1.  用逗号隔开每组 background 的缩写值；
2.  如果有 size 值，需要紧跟 position 并且用 "/" 隔开；
3.  如果有多个背景图片，而其他属性只有一个（例如 background-repeat 只有一个），表明所有背景图片应用该属性值。
4.  background-color 只能设置一个。

导航综合练习 .nav li{background:linear-gradient(to bottom,#dd2926,#a82724,#dd2926) no-repeat right / 1px 15px;}   五、CSS3选择器   六、变形与动画   七、布局样式相关

盒子模型content-box  border-box
---------------------------

box-sizing: border-box;
-----------------------

box-sizing: content-box;

[十天精通CSS3学后笔记](https://www.imooc.com/article/18400)