title: Android 事件监听器
categories:
  - Android
date: 2013-09-12 13:32:19
tags:
  - Android
---

单击事件(View.OnClickListener):用户触碰某个组件或者方向键被按下时产生该事件，该事件处理方法OnClick()

焦点事件（View.OnFocusChangeListener）组件得到或者失去焦点时产生该事件，处理方法OnFocusChange()

按键事件（View.OnKeyListener）用户按下或者释放设备某个按键时产生，处理方法OnKey()

触碰事件(View.OnTouchListener)设备具有触摸功能，触碰屏幕发生该事件，处理方法OnTouch()

创建上下文菜单事件(View.OnCreateContextMenuListener)创建上下文菜单时产生该事件，处理方法onCreateContextMenu()

&nbsp;

事件处理步骤：

1、创建事件监听器

2、响应事件组件注册事件监听器

3、在事件处理方法中实现代码

OnCreate方法中：

获取要触发的控件对象，mEdit1.setOnKeyListener(new OnKeyListener())

{

按键方法

public boolen OnKey(View v,int keyCode,KeyEvent envent)

{

return false

&nbsp;

}

}

&nbsp;

&nbsp;