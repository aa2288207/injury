title: Android 中控件（如Button)设置drawableLeft方法
categories:
  - Android
date: 2015-03-12 07:40:36
tags:
  - Android
---

1.在XML中使用
android:drawableLeft="@drawable/icon"

2.代码中动态变化
Drawable drawable= getResources().getDrawable(R.drawable.drawable);
/// 这一步必须要做,否则不会显示.
drawable.setBounds(0, 0, drawable.getMinimumWidth(), drawable.getMinimumHeight());
editview.setCompoundDrawables(drawable,null,null,null); //可以设置右，上下，在相应位置设置drawable可以

转自：http://ntsoft.blog.163.com/blog/static/11635392012787504479/