title: OnItemClickListener和OnItemLongClickListener区别
categories:
  - Android
date: 2014-07-08 03:05:28
tags:
  - Android
---

一直搞不明白这两个的用法，这下经过整理总结差不多了吧：

1.OnItemClickListener和OnItemLongClickListener在使用含有button或checkbox的listview时，必须把两者的focusable=“false”，否则失效，

2.如果两者同时使用时，OnItemLongClickListener返回false ，则先执行OnItemLongClickListener，再执行OnClickListener，否则OnItemClickListener被覆盖