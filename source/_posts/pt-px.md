---
title: pt & px
categories:
  - 未分类
date: 2022-02-09 16:39:22
tags:
---
### pt
物理单位  
1 pt = 1/72 inch  
1 pt 里如果包含 2 px ，那么是二倍屏
1 pt 里如果包含 3 px ，那么是三倍屏

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

window.devicePixelRatio是设备物理像素和设备独立像素（device-independent pixels，dips）之间的比率。是一个约数？
window.devicePixelRatio = 物理像素 / 设备独立像素 
### DIP (Device Independent Pixel) 
设备独立像素（Device Independent Pixel）：与设备无关的逻辑像素  
css 像素是逻辑像素，并不是真实像素  
Windows / Mac 电脑都可以设置设备独立像素

### dpi (dots per inch)

### ppi (pixels per inch)


参考：  
[1 pt 的图形大小与其在屏幕上显示出的大小之间有什么关系？](https://www.zhihu.com/question/19851058)  
[设备像素比（devicePixelRatio）](https://blog.csdn.net/xueli_2017/article/details/91492971)