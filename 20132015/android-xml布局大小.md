title: Android  获取xml布局大小
categories:
  - Android
date: 2014-08-27 03:41:48
tags:
  - Android
---

```
View view = getLayoutInflater().inflate(R.layout.item_book,null);
view.setLayoutParams(new LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT));
int w = View.MeasureSpec.makeMeasureSpec(0,View.MeasureSpec.UNSPECIFIED);
int h = View.MeasureSpec.makeMeasureSpec(0,View.MeasureSpec.UNSPECIFIED);
view.measure(w, h);
int width =view.getMeasuredWidth()+40;

屏幕宽度：getResources().getDisplayMetrics().widthPixels
int colnum = (int) (((getResources().getDisplayMetrics().widthPixels )) / width);
```