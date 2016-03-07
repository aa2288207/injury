title: 'Android 跳转（带数据 不带数据）/ 获取表单数据 显示表单数据 '
categories:
  - Android
date: 2013-09-12 15:05:48
tags:
  - Android
---

**1 简单跳转**
<div> <wbr />① setContentView 只需要一个activity</div>
<div>两个button分别监听触发事件</div>
<div>通过setContentView(R.layout.main)切换页面</div>
<div> <wbr />② 不同activity之间调用</div>
<div>intent.setClass( HelloWorld.this,MyNextActivity.class);</div>
<div>startActivity(intent);</div>
<div>MyNextActivity.this.finish();//关闭显示的Activit</div>
<div></div>
<div>
<div>**2 带数据跳转**
<div>发送 - Class <wbr />MainActivity：
<div>
<div>Intent intent=new Intent();//Intent可以在不同的应用程序的Activity发送数据</div>
<div>intent.setClass(MainActivity.this, OtherActivity.class);//从哪里跳到哪里</div>
<div>intent.putExtra("**<span style="color: #ff0000;">testIntent</span>**", "Robin");//传递数据</div>
<div>startActivity(intent);</div>
</div>
</div>
</div>
<div>接受 - Class OtherActivity：</div>
<div>
<div>Intent intent = this.getIntent();</div>
<div>String value = intent.getStringExtra("<span style="color: #ff0000;">**testIntent**</span>");</div>
</div>
<div></div>
<div>数据多时，使用Bundle对象</div>
<div>
<div>Intent intent = new Intent(A.this, B.class);</div>
<div>Bundle bundle = new Bundle();</div>
<div>bundle.putString("Name", "feng88724");</div>
<div>bundle.putBoolean("Ismale", true);</div>
<div>intent.putExtras(bundle);</div>
<div>startActivity(intent);</div>
<div></div>
<div>3传递对象</div>
<div>
<pre>Android中Intent中如何传递对象,有两种方法，一种是 Bundle.putSerializable(Key,Object);另一种是Bundle.putParcelable(Key, Object);当然这些Object是有一定的条件的，前者是实现了Serializable接口，而后者是实现了Parcelable接口。</pre>
<pre> ①对象类<span style="color: #ff0000;">**u**</span>要实现 implements Serializable</pre>
<pre>②传递              intent.setClass(MainActivity.this, OtherActivity.class);//从哪里跳到哪里</pre>
<pre>                Bundle bundle = new Bundle();
                 bundle.putSerializable(SER_KEY, <span style="color: #ff0000;">**u**</span>);
                 intent.putExtras(bundle);
                 startActivity(intent);</pre>
</div>
</div>
<div>③接受 User u = (User)getIntent().getSerializableExtra(MainActivity.SER_KEY);</div>
<div>**——————————————————————————————————————**</div>
<div>**获取表单数据**</div>
<div>private EditText displayContent;</div>
<div>displayContent = (EditText)findViewById(R.id.editText1);</div>
<div>Button监听</div>
<div>private Button myButton = null;</div>
<div>myButton = (Button)findViewById(R.id.button1);</div>
<div>myButton.setOnClickListener(new MyButtonListener());</div>
<div>
<div> <wbr />class MyButtonListener implements android.view.View.OnClickListener{</div>
<div> <wbr />  <wbr />  <wbr />  <wbr /> public void onClick(View v) {</div>
<div>//Intent 跳转</div>
<div> <wbr />  <wbr />  <wbr />  <wbr /> }</div>
<div>}</div>
</div>
<div>**接受页面显示数据**</div>
<div>value = 接收数据</div>
<div>
<div>myTextView = (TextView) findViewById(R.id.myTestView);</div>
<div>myTextView.setText(value);</div>
</div>
</div>
<div></div>
<div>-————————————————————————————————————————————</div>
<div>**配置**</div>
<div>每个页面的xml中 @id 自动与R匹配</div>
<div>每一个新的xml 页面 都要在String中注册</div>
<div>&lt;string name="other"&gt;info&lt;/string&gt;</div>
<div>其中的名字info是页面的台头名字</div>
<div></div>
<div>**注册**</div>
<div>每一个新的activity要在 manifest中注册</div>
<div> <wbr />&lt;activity android:name="com.example.login.OtherActivity" android:label="@string/other"/&gt;</div>
<div>label就是String中的名字</div>