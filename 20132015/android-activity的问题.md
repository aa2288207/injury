title: ' android启动activity文本框不获得焦点(初始化页面不弹出软键盘)'
categories:
  - Android
date: 2013-09-27 15:54:44
tags:
  - Android
---

针对此原因，我们可以有以下两种方案：

1、不让文本框获得焦点；
2、获得焦点不弹出输入框；

来看第一种方法，我们可以抢占文本框的焦点，如在其父窗体中加入：

&lt;LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
**android:focusable="true"**
** android:focusableInTouchMode="true"**
tools:context=".MainActivity" &gt;

&lt;EditText
android:id="@+id/etMsg"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
/&gt;
&lt;/LinearLayout&gt;

&nbsp;

第二种：

在activity中加入：`android:windowSoftInputMode = ``"stateHidden"`