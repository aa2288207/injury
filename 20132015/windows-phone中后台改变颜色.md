title: windows phone中后台改变颜色
categories:
  - WP8
date: 2013-09-05 12:53:03
tags:
  - WP8
---

改变字体颜色：txtQuestion.Foreground = new SolidColorBrush(Colors.Black);

改变图片背景：
<pre>ImageBrush brush=new ImageBrush（）；
brush.ImageSource=new BitmapImage(new Uri("wrox.png",UriKind.Relative));
brush.Stresh=Stretch.FIll;
MainRect.Fill=brush;</pre>
&nbsp;