title: Android  自定义GridView网格线
categories:
  - Android
date: 2014-08-29 07:34:02
tags:
  - Android
---

这个问题遗留了好长时间，一直无从下手，今天终于解决了

&nbsp;

&nbsp;
<div class="line number1 index0 alt2" style="color: #000000;">`public class LineGridView extends GridView{`</div>
<div class="line number2 index1 alt1" style="color: #000000;">`    ``public LineGridView(Context context) {`</div>
<div class="line number3 index2 alt2" style="color: #000000;">`        ``super``(context);`</div>
<div class="line number4 index3 alt1" style="color: #000000;">`        ``// TODO Auto-generated constructor stub`</div>
<div class="line number5 index4 alt2" style="color: #000000;">`    ``}`</div>
<div class="line number6 index5 alt1" style="color: #000000;">`    ``public LineGridView(Context context, AttributeSet attrs) {`</div>
<div class="line number7 index6 alt2" style="color: #000000;">`        ``super``(context, attrs);`</div>
<div class="line number8 index7 alt1" style="color: #000000;">`    ``}`</div>
<div class="line number9 index8 alt2" style="color: #000000;">`    ``public LineGridView(Context context, AttributeSet attrs, int defStyle) {`</div>
<div class="line number10 index9 alt1" style="color: #000000;">`        ``super``(context, attrs, defStyle);`</div>
<div class="line number11 index10 alt2" style="color: #000000;">`    ``}`</div>
<div class="line number12 index11 alt1" style="color: #000000;">`    ``@Override`</div>
<div class="line number13 index12 alt2" style="color: #000000;">`    ``protected void dispatchDraw(Canvas canvas){`</div>
<div class="line number14 index13 alt1" style="color: #000000;">`        ``super``.dispatchDraw(canvas);`</div>
<div class="line number15 index14 alt2" style="color: #000000;">`        ``View localView1 = getChildAt(0);`</div>
<div class="line number16 index15 alt1" style="color: #000000;">`        ``int column = getWidth() / localView1.getWidth();`</div>
<div class="line number17 index16 alt2" style="color: #000000;">`        ``int childCount = getChildCount();`</div>
<div class="line number18 index17 alt1" style="color: #000000;">`        ``Paint localPaint;`</div>
<div class="line number19 index18 alt2" style="color: #000000;">`        ``localPaint = ``new` `Paint();`</div>
<div class="line number20 index19 alt1" style="color: #000000;">`        ``localPaint.setStyle(Paint.Style.STROKE);`</div>
<div class="line number21 index20 alt2" style="color: #000000;">`        ``localPaint.setColor(getContext().getResources().getColor(R.color.grid_line));`</div>
<div class="line number22 index21 alt1" style="color: #000000;">`        ``for``(int i = 0;i &lt; childCount;i++){`</div>
<div class="line number23 index22 alt2" style="color: #000000;">`            ``View cellView = getChildAt(i);`</div>
<div class="line number24 index23 alt1" style="color: #000000;">`            ``if``((i + 1) % column == 0&amp;&amp;i&lt;column){         // 第一列画头顶线显示底部线`</div>
<div class="line number25 index24 alt2" style="color: #000000;">`                ``canvas.drawLine(cellView.getLeft(), cellView.getBottom(), cellView.getRight(), cellView.getBottom(), localPaint);`</div>
<div class="line number26 index25 alt1" style="color: #000000;">`            ``}``else` `if``((i + 1) &gt; (childCount - (childCount % column))){       // 边界处理（最后一行）画右边垂直隔离线`</div>
<div class="line number27 index26 alt2" style="color: #000000;">`                ``canvas.drawLine(cellView.getRight(), cellView.getTop(), cellView.getRight(), cellView.getBottom(), localPaint);`</div>
<div class="line number28 index27 alt1" style="color: #000000;">`            ``}``else``{`</div>
<div class="line number28 index27 alt1" style="color: #000000;">                                 if（i&lt;column）  // 其他列，画右边隔离线，与底线</div>
<div class="line number28 index27 alt1" style="color: #000000;">                                  {</div>
<div class="line number28 index27 alt1" style="color: #000000;"></div>
<div class="line number29 index28 alt2" style="color: #000000;">`                ``canvas.drawLine(cellView.getRight(), cellView.getTop(), cellView.getRight(), cellView.getBottom(), localPaint);`</div>
<div class="line number30 index29 alt1" style="color: #000000;">`                ``canvas.drawLine(cellView.getLeft(), cellView.getBottom(), cellView.getRight(), cellView.getBottom(), localPaint);`</div>
<div class="line number30 index29 alt1" style="color: #000000;">`              }`</div>
<div class="line number30 index29 alt1" style="color: #000000;">                         else//如果gridview分页，第一页有底线，这样可以去掉底线， // 其他列，画右边隔离线</div>
<div class="line number30 index29 alt1" style="color: #000000;">                               {</div>
<div class="line number30 index29 alt1" style="color: #000000;">`                  ``canvas.drawLine(cellView.getRight(), cellView.getTop(), cellView.getRight(), cellView.getBottom(), localPaint);`</div>
<div class="line number30 index29 alt1" style="color: #000000;">                                 }</div>
<div class="line number31 index30 alt2" style="color: #000000;">`            ``}`</div>
<div class="line number32 index31 alt1" style="color: #000000;">`        ``}`</div>
<div class="line number32 index31 alt1" style="color: #000000;">               // 确保最后一行，没有填满的单元格右侧也好垂直隔离线（注意与上面代码 else if 的关系）</div>
<div class="line number33 index32 alt2" style="color: #000000;">`        ``if``(childCount % column != 0){`</div>
<div class="line number34 index33 alt1" style="color: #000000;">`            ``for``(int j = 0 ;j &lt; (column-childCount % column) ; j++){`</div>
<div class="line number35 index34 alt2" style="color: #000000;">`                ``View lastView = getChildAt(childCount - 1);`</div>
<div class="line number36 index35 alt1" style="color: #000000;">`                ``canvas.drawLine(lastView.getRight() + lastView.getWidth() * j, lastView.getTop(), lastView.getRight() + lastView.getWidth()* j, lastView.getBottom(), localPaint);`</div>
<div class="line number37 index36 alt2" style="color: #000000;">`            ``}`</div>
<div class="line number38 index37 alt1" style="color: #000000;">`        ``}`</div>
<div class="line number39 index38 alt2" style="color: #000000;">`    ``}`</div>
<div class="line number40 index39 alt1" style="color: #000000;">`}`</div>
<div class="line number40 index39 alt1" style="color: #000000;"></div>
<div class="line number40 index39 alt1" style="color: #000000;">

在`dispatchDraw`方法中，我们对每一个子view的边界按照一定的方式绘上了边框，一般一个格子只需绘制其中两条边，需要注意的是最边上的格子需要特殊处理。`super``.dispatchDraw(canvas);`一定要调用，不然格子中的内容（子view）就得不到绘制的机会，结果就如下面这样：

![](http://www.jcodecraeer.com/uploads/20131227/13881504312676.png "device-2013-12-27-211055.png")

</div>