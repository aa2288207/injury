title: Android 小部件(桌面插件)
categories:
  - Android
date: 2014-09-12 10:03:51
tags:
  - Android
---

哎，这个部件折腾死我了，通过各种资料总算弄的差不多了，就总结下吧，

一、小部件支持的控件

<span style="color: #000066;">Widget并不支持所有的布局和控件，而仅仅只是支持Android布局和控件的一个子集。</span>
<span style="color: #000066;">(01) App Widget支持的布局：</span>
<span style="color: #ff0000;">　　FrameLayout</span>
<span style="color: #ff0000;">　　LinearLayout</span>
<span style="color: #ff0000;">　　RelativeLayout</span>
<span style="color: #ff0000;">　　GridLayout</span>
<span style="color: #000066;">(02) App Widget支持的控件：</span>
<span style="color: #ff0000;">　　AnalogClock</span>
<span style="color: #ff0000;">　　Button</span>
<span style="color: #ff0000;">　　Chronometer</span>
<span style="color: #ff0000;">　　ImageButton</span>
<span style="color: #ff0000;">　　ImageView</span>
<span style="color: #ff0000;">　　ProgressBar</span>
<span style="color: #ff0000;">　　TextView</span>
<span style="color: #ff0000;">　　ViewFlipper</span>
<span style="color: #ff0000;">　　ListView</span>
<span style="color: #ff0000;">　　GridView</span>
<span style="color: #ff0000;">　　StackView</span>
<span style="color: #ff0000;">　　AdapterViewFlipper</span>

想要进一步了解可参考：http://www.cnblogs.com/skywang12345/p/3158310.html

二、小部件使用方法：可参考上面链接使用

但是使用中需注意几点：

1、widget第一次创建后删除，会造成Service停止，如果需要Service继续运作（使用Service刷新方式）则需要重新创建Service

//判断Service服务是否停止
private boolean isServiceRunning(Context context) {
ActivityManager manager = (ActivityManager) context.getSystemService(Context.ACTIVITY_SERVICE);
for (RunningServiceInfo service : manager.getRunningServices(Integer.MAX_VALUE)) {
if (ClassName.equals((service.service.getClassName()))) {
return true;
}
}
return false;
}

boolean f=isServiceRunning(context);
if(!f){
context.startService(EXAMPLE_SERVICE_INTENT);
}

2、由于widget支持的控件极少，于是在使用中需注意几点：

需要给TextView 赋值：

RemoteViews remoteView = new RemoteViews(context.getPackageName(), R.layout.layout_appwidget);

remoteView.setTextViewText(R.id.tv_widget_text,verse.text);  //第一个参数VIewID，第二个参数：赋的值

remoteView.setViewVisibility(R.id.rl_verse, View.VISIBLE); //控制显示

remoteView.setInt(R.id.btn_devotion, "setBackgroundColor",context.getResources().getColor(R.color.darkGray));

//设置Button字体颜色，介绍同上

remoteView.setTextColor(R.id.btn_verse, context.getResources().getColor(R.color.white));

**最后两个方法尤其重要，需要给Button重新设置背景，第一个参数ViewID，第二个参数尤为重要**
**<span style="color: #444444;">关键是第二个参数,是一个方法名字,比如这里是textView,那么textView会有很多方法,比如setBackground(), setText(), setTextColor()等等,第二个参数就填这个函数名,不要括号,</span>**
**<span style="color: #444444;">第三个参数就填第二个函数所用到的参数,比如如果是setTextColor(int), 第三个参数就带int进去(当然如果是这个你就必须用views.setInt(...)这个函数),</span>**
**<span style="color: #444444;">比如需要设置背景颜色用到Color ，就用context.getResources().getColor(R.color.darkGray)，如果设置背景图片，第二个参数需要改成setBackground，第三个参数context.getResources().getColor(R.drawable.img);</span>**

3.发送广播出

//这句第二个参数不要传递0否则接下来创建第二个时会有问题
PendingIntent pi = PendingIntent.getBroadcast(context,widgetId, intent, 0 );

4.

// 更新 widget
appWidgetManager.updateAppWidget(appID, remoteView);

也可以用下文代替：

ComponentName thisWidget = new ComponentName(context, ExampleAppWidgetProvider.class);
// 更新 widget
appWidgetManager.updateAppWidget(thisWidget, remoteView);

&nbsp;