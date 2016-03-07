title: ViewFlipper 和 listview 滑动冲突
categories:
  - Android
date: 2014-08-25 02:31:25
tags:
  - Android
---

当 ViewFlipper <wbr /> 左右滑动和listview的上下滑动冲突时，哈哈以下解决办法：

 <wbr />

@Override
<wbr />public boolean onTouch(View arg0, MotionEvent arg1) {
<wbr /> <wbr />System.out.println("Touch::::::::::::::::::::");
<wbr /> <wbr />super.onTouchEvent(arg1);
<wbr /> <wbr />return gd.onTouchEvent(arg1);
<wbr />}

 <wbr />

 <wbr />

<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">@Override</span>
<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">public boolean dispatchTouchEvent(MotionEvent ev) {</span>
<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">// 先执行滑屏事件</span>
<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">gd.onTouchEvent(ev);</span>
<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">super.dispatchTouchEvent(ev);</span>
<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">return true;</span>
<span style="color: #464646;"> </span><wbr style="color: #464646;" /><span style="color: #464646;">}</span>