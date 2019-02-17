---
title: 导航滚动悬浮
url: 116.html
id: 116
categories:
  - 未分类
date: 2017-11-08 10:35:29
tags:
---

做两个导航，第二个隐藏 下拉到一定位置，显示第二个，position:fixed $(function(){ $(window).scroll(function () {$(window).scroll(function () { var top = $(document).scrollTop(); var m=$(".nav"); if (top > m.offset().top) { m.next().css('display','block') }else{ m.next().css('display','none') } }) }