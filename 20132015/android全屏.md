title: Android 设置全屏
categories:
  - Android
date: 2015-05-07 07:57:38
tags:
  - Android
---

设置全屏隐藏标题栏和电池信息

# 设置全屏
```
requestWindowFeature(Window.FEATURE_NO_TITLE);//取消标题栏
this.getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,WindowManager.LayoutParams.FLAG_FULLSCREEN);// 去掉通知栏
```

# 设置非全屏

```
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN);// 取消全屏设置
```
    