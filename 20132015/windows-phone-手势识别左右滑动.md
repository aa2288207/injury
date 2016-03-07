title: windows phone 手势识别左右滑动
categories:
  - WP8
date: 2013-07-22 13:17:34
tags:
  - WP8
---

1\. 引入dll （silverlight for wndows phone toolkit）

2.引入命名空间
<div>01.xmlns:toolkit="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone.Controls.Toolkit"</div>
<div>

3.手势是依附控控件而存活的，在某个控件内部添加(这里是coverflow第三方控件,),添加了 Flick事件
<div>&lt;local:CollectionFlow x:Name="ImageList" ItemTemplate="{StaticResource DataTemplate1}" ItemsPanel="{StaticResource ItemsPanelTemplate1}"&gt;
&lt;toolkit:GestureService.GestureListener&gt;
&lt;toolkit:GestureListener   Flick="GestureListener_Flick" /&gt;
&lt;/toolkit:GestureService.GestureListener&gt;
&lt;/local:CollectionFlow&gt;</div>
4.
<div> private void GestureListener_Flick(object sender, FlickGestureEventArgs e)
{
//监听器里面写相关处理代码， 通过角度判断左右滑动.
if (e.Angle &gt; 135 &amp;&amp; e.Angle &lt; 225)  //向左增加图片
{

}
else if (e.Angle &gt; 315 || e.Angle &lt; 45)//向右增加图片
{

}</div>
<div>// 这里的e.Angle是滑动的角度，和几何里的象限一摸一样 使用起来很简单</div>
<div>}</div>
</div>