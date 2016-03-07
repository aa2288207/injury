title: Android之下拉框使用
categories:
  - Android
date: 2013-10-28 17:26:07
tags:
  - Android
---

Spinner在android中是用来显示下拉框的组件，对其进行设置主要有两种方式：
<div>方式一：直接在xml文件中设置其要现实的内容：</div>
<div> <wbr />  <wbr />  <wbr />  <wbr />在对应的布局文件中例如main.xml</div>
<div>[![[转载]android中下拉框spinner的两种用法](http://s11.sinaimg.cn/middle/877c72acga9bc222ef4ea&amp;690 "[转载]android中下拉框spinner的两种用法")](http://photo.blog.sina.com.cn/showpic.html#blogid=690892850101qpgs&amp;url=http://s11.sinaimg.cn/orignal/877c72acga9bc222ef4ea)</div>
要显示的内容在String.xml文件中设置如下：
<div>[![[转载]android中下拉框spinner的两种用法](http://s13.sinaimg.cn/middle/877c72acga9bc2a5c41ac&amp;690 "[转载]android中下拉框spinner的两种用法")](http://photo.blog.sina.com.cn/showpic.html#blogid=690892850101qpgs&amp;url=http://s13.sinaimg.cn/orignal/877c72acga9bc2a5c41ac) 设置完成后，下拉框就可以显示内容了。</div>
<div>如果调用下拉框的值用spinner.getSelectedItem().toString()</div>
<div></div>
<div>方式二：在coll_vehi.xml中写入</div>
<div> <wbr />  <wbr /> &lt;Spinner</div>
<div> <wbr />  <wbr />  <wbr />android:id="@+id/vehicle_type"</div>
<div> <wbr />  <wbr />  <wbr />android:layout_height="wrap_content"</div>
<div> <wbr />  <wbr />  <wbr />android:layout_width="wrap_content"</div>
<div> <wbr />  <wbr />  <wbr />/&gt;</div>
<div>在activity主程序中写：</div>
<div></div>
<div>![](http://s6.sinaimg.cn/large/877c72acga9bc5958ad45&amp;690)</div>
<div>
<div>//通过createFromResource方法创建一个ArrayAdapter对象</div>
<div>//第一个参数值上下文对象</div>
<div>//第二个参数引用在strings.xml文件当中定义的string数组</div>
<div>//第三个参数是用来指定spinner的样式，是一个布局文件的ID，该布局文件由Android系统所提供，也可替换为自己定义的布局文件</div>
</div>
<div>ArrayAdapter&lt;CharSequence&gt; adpater=ArrayAdapter.createFromResource(this,R.array.plants_array,android.layout.simple_spinner_item);</div>
<div>//设置Spinner当中每个条目的样式，同样是引用一个Android系统提供的布局文件</div>
<div>apapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdovn_item);</div>
<div>spinner.setAdapter(adapter);</div>
<div>spinner.setPrompt("测试")；//标题的设置</div>
<div>spinner.setOnItemSelectedListener(new SpinnerOnSelectedListener());</div>
<div></div>
<div></div>
<div>如果调用下拉框的值用spinner.getSelectedItem().toString()</div>
<div></div>