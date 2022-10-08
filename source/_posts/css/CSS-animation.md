---
title: CSS-animation
categories:
  - technology
  - front-end
  - css
date: 2021-06-04 10:00:16
tags:
---
animation: name duration timing-function delay iteration-count direction fill-mode play-state;

## animation-name	
指定要绑定到选择器的关键帧的名称

## animation-duration	
动画指定需要多少秒或毫秒完成

## animation-timing-function	
设置动画将如何完成一个周期

## animation-delay	
设置动画在启动前的延迟间隔。

## animation-iteration-count	
定义动画的播放次数。

|  value   | description  |
|  ----  | ----  |
|n|	一个数字，定义应该播放多少次动画	|
|infinite|	指定动画应该播放无限次（永远）|


## animation-direction	
指定是否应该轮流反向播放动画。

## animation-fill-mode	
规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。

## animation-play-state	
指定动画是否正在运行或已暂停。

## @keyframes
```css
@keyframes name
{
    from {background: red;}
    to {background: yellow;}
}

@keyframes name
{
    0%   {background: red;}
    25%  {background: yellow;}
    50%  {background: blue;}
    100% {background: green;}
}
```