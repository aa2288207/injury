title: Windows Phone 模拟器中去掉右侧的帧速率计数器
categories:
  - WP8
date: 2013-06-28 14:39:26
tags:
  - WP8
---

在Windows Phone 7的模拟器中运行应用程序时，默认会在右侧显示帧速率计数器的内容，这是用来监控应用程序的性能。如下图：

[http://silverlightchina.net/uploads/allimg/120729/1954463C5-0.jpg](http://silverlightchina.net/uploads/allimg/120729/1954463C5-0.jpg)

文件 App.xaml.cs. 中找到该代码：

Application.Current.Host.Settings.EnableFrameRateCounter = true

将值赋为false，或者将整句话注销掉即可。