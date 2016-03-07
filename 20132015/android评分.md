title: android 评分，跳转手机APP市场
categories:
  - Android
date: 2015-06-16 07:40:03
tags:
  - Android
---

语法：
1、打开所有app上传的市场：market://search?q=pname:app的包名
2、打开指定的市场：http://market.android.com/details?id=app的包名

```
eg:
Uri uri=Uri.parse("market://search?q=pname:www.holdlg.com")
Intent intent=new Intent(Intent.ACTION_VIEW,Uri.parse(uri));
startActivity(intent);
```