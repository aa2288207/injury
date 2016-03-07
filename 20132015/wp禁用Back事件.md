title: wp 禁用Back事件
id: 399
categories:
  - WP8
date: 2013-06-20 16:49:56
tags:
  - WP8
---

在开发过程中，因为页面是无状态的，可能会导致页面的回退操作逆向业务需求而禁用回退

两步可以轻松搞定

第一 在XAML文件注册事件：

BackKeyPress="PhoneApplicationPage_BackKeyPress"&gt;

第二在后台实现方法
private void PhoneApplicationPage_BackKeyPress(object sender, System.ComponentModel.CancelEventArgs e)
{
e.Cancel = true;
}

或者直接实现重

protected override void OnBackKeyPress(System.ComponentModel.CancelEventArgs e)
{
e.Cancel = true;
}