title: Android 弹出对话框
categories:
  - Android
date: 2013-09-13 16:23:53
tags:
  - Android
---

<span>android Dailog(对话框)
<wbr />1. <wbr />创建
<wbr /> a. <wbr />new AlertDialog.Builder(Context <wbr /> context)
<wbr /> b. <wbr />一些设置
<wbr /> c. <wbr />create()创建
<wbr /> d. <wbr />show()显示
<wbr /> e. <wbr />dismiss()退出对话框</span>

<span> <wbr />2. <wbr />常用方法
<wbr /> setIcon:设置图标
<wbr /> setTitle:设置标题
<wbr /> setPositiveButton:设置 确定按钮
<wbr /> setNegativeButton:设置 取消按钮
<wbr /> setNeutralButton:设置 忽略按钮
<wbr /> setCancelable(Boolean arg0)//按回退键是否可以取消</span>

<span> <wbr /> <wbr />3. <wbr />可选但唯一的方法
<wbr /> setMessage 设置显示消息
<wbr /> setItems <wbr /> <wbr /> 显示单选列表,选择后对话框退出
<wbr /> setSingleChoiceItems 显示单选列表,选择后对话框不退出
<wbr /> setMultiChoiceItems <wbr /> 显示多选列表,选择后对话框不退出
<wbr /> <wbr /> 使用方法：</span>

&nbsp;

在onKeyDown(int keyCode, KeyEvent event)方法中调用此方法

public boolean onKeyDown(int keyCode, KeyEvent event) {
if (keyCode == KeyEvent.KEYCODE_BACK &amp;&amp; event.getRepeatCount() == 0) {
dialog();
}
return false;
}

创建对话框方法dialog()，实现有选择性的，确定/取消、

protected void dialog() {
AlertDialog.Builder builder = new Builder(Main.this);
builder.setMessage("确认退出吗？");

builder.setTitle("提示");

builder.setPositiveButton("确认", new OnClickListener() {

@Override
public void onClick(DialogInterface dialog, int which) {
dialog.dismiss();

Main.this.finish();
}
});

builder.setNegativeButton("取消", new OnClickListener() {

@Override
public void onClick(DialogInterface dialog, int which) {
dialog.dismiss();
}
});

builder.create().show();
}

实现效果：![](http://pic002.cnblogs.com/images/2010/133128/2010111511252588.png)

二、改变了对话框的图表，添加了三个按钮

Dialog dialog = new AlertDialog.Builder(this).setIcon(
android.R.drawable.btn_star).setTitle("喜好调查").setMessage(
"你喜欢李连杰的电影吗？").setPositiveButton("很喜欢",
new OnClickListener() {

@Override
public void onClick(DialogInterface dialog, int which) {
// TODO Auto-generated method stub
Toast.makeText(Main.this, "我很喜欢他的电影。",
Toast.LENGTH_LONG).show();
}
}).setNegativeButton("不喜欢", new OnClickListener() {

@Override
public void onClick(DialogInterface dialog, int which) {
// TODO Auto-generated method stub
Toast.makeText(Main.this, "我不喜欢他的电影。", Toast.LENGTH_LONG)
.show();
}
}).setNeutralButton("一般", new OnClickListener() {

@Override
public void onClick(DialogInterface dialog, int which) {
// TODO Auto-generated method stub
Toast.makeText(Main.this, "谈不上喜欢不喜欢。", Toast.LENGTH_LONG)
.show();
}
}).create();

dialog.show();

实现效果：![](http://pic002.cnblogs.com/images/2010/133128/2010111511254541.png)

三、信息内容是一个简单的View类型

new AlertDialog.Builder(this).setTitle("请输入").setIcon(
android.R.drawable.ic_dialog_info).setView(
new EditText(this)).setPositiveButton("确定", null)
.setNegativeButton("取消", null).show();

实现效果：![](http://pic002.cnblogs.com/images/2010/133128/2010111511261716.png)