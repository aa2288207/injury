title: Android中级教程之----Log详解
categories:
  - Android
date: 2013-09-16 10:25:09
tags:
  - Android
---

android.util.Log常用的方法有以下**5**个：**Log.v()** **Log.d()** **Log.i() Log.w()** 以及 **Log.e()** 。根据首字母对应**VERBOSE**，**DEBUG,INFO, WARN，ERROR。**

1、Log.v 的调试颜色为**黑色**的，任何消息都会输出，这里的v代表verbose啰嗦的意思，平时使用就是Log.v("","");

2、Log.d的输出颜色是**蓝色**的，仅输出debug调试的意思，但他会输出上层的信息，过滤起来可以通过DDMS的Logcat标签来选择.

3、Log.i的输出为**绿色**，一般提示性的消息information，它不会输出Log.v和Log.d的信息，但会显示i、w和e的信息

4、Log.w的意思为**橙色**，可以看作为warning警告，一般需要我们注意优化Android代码，同时选择它后还会输出Log.e的信息。

5、Log.e为红色，可以想到error错误，这里仅显示红色的错误信息，这些错误就需要我们认真的分析，查看栈的信息了。

下面是我做的一个简单的**LogDemo**(**Step By Step):**

**Step 1**:准备工作(打开**LogCat**视窗)．

启动**Eclipse**,在**Window-&gt;Show View**会出来一个对话框，当我们点击**Ok**按钮时，会在控制台窗口出现**LogCat**视窗.如下图：

&nbsp;

![](http://p.blog.csdn.net/images/p_blog_csdn_net/Android_Tutor/EntryImages/20091226/log1.jpg) ![](http://p.blog.csdn.net/images/p_blog_csdn_net/Android_Tutor/EntryImages/20091226/log3.jpg)

&nbsp;

**Step 2**:新建一个**Android**工程，命名为**LogDemo**.

&nbsp;

**Step 3:**设计**UI**界面，我们在这里就加了一个**Button**按钮(点击按钮出现**Log**日志信息)．

**Main.xml**代码如下:

&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout xmlns:android="[http://schemas.android.com/apk/res/android](http://schemas.android.com/apk/res/android)"
android:orientation="vertical"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
&gt;
&lt;TextView
android:layout_width="fill_parent"
android:layout_height="wrap_content"
android:text="@string/hello"
/&gt;
**&lt;Button
android:id="@+id/bt"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Presse Me Look Log"
/&gt;
**&lt;/LinearLayout&gt;

**Step 4**:设计主类**LogDemo.java**,代码如下:

&nbsp;

package com.android.test;

import android.app.Activity;
import android.os.Bundle;
**import android.util.Log;
import android.view.View;
import android.widget.Button;**

public class **LogDemo** extends Activity {

**private static final String ACTIVITY_TAG="LogDemo";**
**private Button bt;**
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.main);
//通过findViewById找到Button资源
**   bt = (Button)findViewById(R.id.bt);**
//增加事件响应
**   bt.setOnClickListener(new Button.OnClickListener(){
**    @Override
**   public void onClick(View v) {
Log.v(LogDemo.ACTIVITY_TAG, "This is Verbose.");
Log.d(LogDemo.ACTIVITY_TAG, "This is Debug.");
Log.i(LogDemo.ACTIVITY_TAG, "This is Information");
Log.w(LogDemo.ACTIVITY_TAG, "This is Warnning.");
Log.e(LogDemo.ACTIVITY_TAG, "This is Error.");
}
**        **
});**
}

}

&nbsp;

**Step 5**:运行**LogDemo**工程，效果如下:

&nbsp;

![](http://p.blog.csdn.net/images/p_blog_csdn_net/Android_Tutor/EntryImages/20091226/log4.jpg)

&nbsp;

当我们点击按钮时，会触发事件，在Logcat视窗下有如下效果:

&nbsp;

![](http://p.blog.csdn.net/images/p_blog_csdn_net/Android_Tutor/EntryImages/20091226/log5.jpg)

&nbsp;