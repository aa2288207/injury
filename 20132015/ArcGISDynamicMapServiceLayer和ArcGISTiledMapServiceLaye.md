title: ArcGISDynamicMapServiceLayer和ArcGISTiledMapServiceLaye区别
categories:
  - ArcGIS
date: 2014-03-21 03:22:46
tags:
  - ArcGIS
---

<div>
ArcGISDynamicMapServiceLayer以ArcGISTiledMapServiceLaye方式使用

</div>
<div>

ArcGIS客户端API（Javascript/Flex/Silverlight）中，我们最常打交道的是ArcGISDynamicMapServiceLayer和ArcGISTiledMapServiceLayer两个类，基本每个地图中都要用到。它们都可以直接将服务器端发布的地图服务（MapService

）作为图层，加载到客户端程序中，分别对应了动态地图服务和缓存地图服务。这两种图层类型各有优缺点。

ArcGISDynamicMapServiceLayer（动态地图服务）通常用于实时显示经常变化的数据，支持控制单个图层可见性，可动态投影。但缺点是显示效果较差，整个服务出图较慢；ArcGISTiledMapServiceLayer可以直接加载服务器端的缓存地图服务，显示效果好，速度快，

但它的缺点正是ArcGISDynamicMapServiceLayer的优点，即不支持动态投影，不能控制图层可见性，服务器端需要提前生成缓存等。

这里尝试自己来在客户端封装一个类，创建一种新的客户端图层类型。它能够综合以上两个图

</div>
<div>

层的优点，而克服其各自的缺点。大致总结一下我们要达到的目的：

[![QQ截图20140321112449](http://holdlg.coding.io/wp-content/uploads/2014/03/QQ截图20140321112449-300x182.jpg)](http://holdlg.coding.io/wp-content/uploads/2014/03/QQ截图20140321112449.jpg)

</div>
<div>
<div>

讨论具体的实现代码，只说明一下实现思路。

</div>
</div>