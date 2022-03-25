---
title: Pixel
categories:
  - 未分类
date: 2022-02-09 16:39:22
tags:
---
### 题记

1. 1 px 问题是如何产生的？
2. 为什么会有 二倍图，三倍图？
3. 苹果公司所说的 Retina 屏是啥？
4. 屏幕清晰度由哪个参数决定，分辨率越高就一定越清晰吗？
5. 屏幕尺寸相同可以通过分辨率判断屏幕清晰度，屏幕尺寸不同，如何判断哪块屏幕更清晰？

### pt
物理单位  
1 pt = 1/72 inch  
1 inch = 72 pt  
72 pt = 96 px  
绝对长度单位，多用于打印  


### inch
1 inch = 2.54 cm 

### px
1px 问题
获取设备像素比  
js  
window.devicePixelRatio  
css  
-webkit-min-device-pixel-ratio
### dpr (devicePixelRatio)
设备像素比
![dpi 和 dpr](https://img-blog.csdnimg.cn/20190612152430172.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZWxpXzIwMTc=,size_16,color_FFFFFF,t_70)
window.devicePixelRatio是设备物理像素和设备独立像素（device-independent pixels，dips）之间的比率。是一个约数？
window.devicePixelRatio = 物理像素 / 设备独立像素 
### DIP (Device Independent Pixel) 
设备独立像素（Device Independent Pixel）：与设备无关的逻辑像素  
css 像素是逻辑像素，并不是真实像素  
Windows / Mac 电脑都可以设置设备独立像素

### dpi (dots per inch)
和 ppi 基本相同
### ppi (pixels per inch)
![ppi 计算公式](https://images2015.cnblogs.com/blog/984702/201704/984702-20170412161418626-799396908.png)

ppi在120-160之间的手机被归为低密度手机，160-240被归为中密度，240-320被归为高密度，320以上被归为超高密度（例如苹果公司的Retina显示屏）
![](https://images2015.cnblogs.com/blog/984702/201704/984702-20170412163336783-427220997.png)
### 总结
CSS 只与设备独立像素有关系，尺寸相同，设备独立像素相同的屏幕，网页上的同一张图片显示的尺寸是相同的，只不过清晰度会有所不同。所以会有二倍图，三倍图。
宽 100px 的图片在 1:1 的屏幕上css设置为 100px，在 2:1 的屏幕上可以使用200px 的图片，css 同样设置为 100px 。  
设备独立像素 (DIP) 是与设备无关的，可以调整的逻辑像素。


### 参考：  
1. [1 pt 的图形大小与其在屏幕上显示出的大小之间有什么关系？](https://www.zhihu.com/question/19851058)

2. [pt](http://www.w3chtml.com/css3/units/length/pt.html)

3. [设备像素比（devicePixelRatio）](https://blog.csdn.net/xueli_2017/article/details/91492971)

4. [CSS像素、设备独立像素、设备像素之间关系](https://www.cnblogs.com/jiangzilong/p/6700023.html)