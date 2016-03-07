title: Android 自定义checkbox
categories:
  - Android
date: 2014-01-03 05:38:15
tags:
  - Android
---

1.首先在drawable文件夹中添加drawable文件checkbox_style.xml。

&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;selector xmlns:android="[http://schemas.android.com/apk/res/android](http://schemas.android.com/apk/res/android)"&gt;
&lt;item android:drawable="@drawable/checkbox_pressed" android:state_checked="true"&gt;&lt;/item&gt;
&lt;item android:drawable="@drawable/checkbox_normal" android:state_checked="false"&gt;&lt;/item&gt;
&lt;item android:drawable="@drawable/checkbox_normal"&gt;&lt;/item&gt;
&lt;/selector&gt;

2.在values文件夹下的styles.xml文件中添加CustomCheckboxTheme样式。

&lt;style name="CustomCheckboxTheme" parent="@android:style/Widget.CompoundButton.CheckBox"&gt;
&lt;item name="android:button"&gt;@drawable/checkbox_style&lt;/item&gt;
&lt;/style&gt;

3.在布局文件中使用CustomCheckboxTheme样式。

&lt;CheckBox
android:id="@+id/checkbox_organic"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
style="@style/CustomCheckboxTheme"
android:text="@string/checkbox_organic" &gt;
&lt;/CheckBox&gt;

使用到的图片资源

![](http://hi.csdn.net/attachment/201112/27/0_1324978367qQx1.gif)checkbox_normal.png

![](http://hi.csdn.net/attachment/201112/27/0_1324978373H8U6.gif)checkbox_pressed.png

&nbsp;