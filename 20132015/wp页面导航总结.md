title: wp页面导航总结
id: 476
categories:
  - WP8
date: 2013-07-16 18:19:16
tags:
  - WP8
---

一、win8 App上的导航的使用（使用Frame进行页面之间传值）
1、与wp7不同，metro在页面间导航不用指明具体的uri，只需要将页面的类型当作参数传给navigated方法就可以
this.Frame.Navigate(typeof(BasicPage2));

说明：
Frame类主要负责导航和实现 Navigate, GoBack, and GoForward 等方法
Frame更像是多个page的容器

2、使用navigete在页面间传值时，使用第二个参数
this.Frame.Navigate(typeof(BasicPage2), "passValue");
3.在导航到接收页面时，通过事件的传入参数来接收值
protected override void OnNavigatedTo(NavigationEventArgs e)
{
string name = e.Parameter as string;
}
二、