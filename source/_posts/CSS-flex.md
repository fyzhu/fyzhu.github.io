---
title: CSS-flex
categories:
  - 未分类
date: 2021-06-07 10:45:33
tags:
---

## 容器的属性

### flex-direction 属性

规定灵活项目的方向

flex-direction: row|row-reverse|column|column-reverse|initial|inherit;
|  value   | description  |
|:-----|:-----|
|row	|默认值。灵活的项目将水平显示，正如一个行一样。	|
row-reverse	|与 row 相同，但是以相反的顺序。	
column	|灵活的项目将垂直显示，正如一个列一样。	
column-reverse |与 column 相同，但是以相反的顺序。

### flex-wrap 属性

规定flex容器是单行或者多行，同时横轴的方向决定了新行堆叠的方向。

flex-wrap: nowrap|wrap|wrap-reverse|initial|inherit;


### flex-flow 属性

是 flex-direction 和 flex-wrap 属性的复合属性。默认值为row nowrap。

flex-flow: flex-direction flex-wrap|initial|inherit;


### justify-content
justify-content属性定义了项目在主轴上的对齐方式。

justify-content: flex-start | flex-end | center | space-between | space-around;
### align-items
定义项目在交叉轴上如何对齐。

align-items: flex-start | flex-end | center | baseline | stretch;
### align-content
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。


## 项目的属性

### order

定义项目的排列顺序。数值越小，排列越靠前，默认为0。

### flex-grow 属性

用于设置或检索弹性盒子的扩展比率。

flex-grow: number|initial|inherit;

### flex-shrink 属性

指定了 flex 元素的收缩规则。flex 元素仅在默认宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值。

flex-shrink: number|initial|inherit;


### flex-basis 属性

用于设置或检索弹性盒伸缩基准值

### flex

flex: flex-grow flex-shrink flex-basis|auto|initial|inherit;

### align-self属性

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。