title: Android 之页面跳转
categories:
  - Android
date: 2013-09-24 14:35:02
tags:
  - Android
---

TextView    registerTv = (TextView) findViewById(R.id.registerTv);
<pre id="best-content-764768191">  tv.setOnClickListener(new OnClickListener(){
               public void onClick(View v){
                      Intent intent=new Intent(当前Activity名字.this,要跳转的Activity名字.class) ;
                       startActivity(intent) ;
}
});</pre>