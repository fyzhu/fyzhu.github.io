---
title: arcgis layer.when 和 view.when 以及 MapImageLayer
date: 2019-02-17 19:54:54
tags: arcgis
---
MapImageLayer加载完之后需要view.goto(layer.fullExtent)才能显示

arcgis js 中 layer.when 和 view.when的执行顺序

当无baseMap时，layer.when先执行，view.when后执行，在view.when中执行view.goto，MapImageLayer正常显示


当有baseMap时，baseMap加载需要时间，加载完baseMap再加载layer，view.when先执行，layer.when后执行

当baseMap为天地图时，view.goto有问题，使用view.extent = layer.fullExtent; MapImageLayer有时候会不显示

