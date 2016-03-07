title: Android  调用系统组件
categories:
  - Android
date: 2014-03-14 10:26:47
tags:
  - Android
---

一、点击通知栏中通知直接跳转短信内容页面：
     Intent intent=new Intent();
     intent.setAction(Intent.ACTION_VIEW);
     intent.setType("vnd.android-dir/mms-sms");
     intent.putExtra("address",  values.get("address").toString());
     intent.putExtra("body", values.getAsString("body"));

二、点击通知栏中通知直接跳转短信编辑页面：
     Intent intent=new Intent();
     intent.setAction(Intent.ACTION_VIEW);
     intent.setType("vnd.android-dir/mms-sms");
    // intent.setData(Uri.parse("content://mms-sms/conversations/"));//此为号码  

   指定发送短信人
      uri = Uri.parse("smsto:"+要发送短信的对方的number);    

      intent = new Intent(Intent.ACTION_SENDTO,uri);  

三、点击通知栏中通知跳转拨号：
      Intent intent=new Intent();
      intent.setAction(Intent.ACTION_CALL);
      intent.setData(Uri.parse("te:"+电话号码));

四、启动联系人界面：
    Intent intent=new Intent();
    intent.setAction(Intent.ACTION_PICK);
    intent.setData(Uri.parse(Contacks.People.CONTENT_URL));

五、浏览网页某一具体网址：
   Intent intent   = new Intent(Intent.ACTION_VIEW,uri);
   Uri uri = Uri.parse("http://xxxxxxxxxxxxxxxxxxxxxxxx");   
   //加下面这句话就是启动系统自带的浏览器打开上面的网址，  不加下面一句话，  如果你有多个浏览器，就会弹出让你选择某一浏览器，     然后改浏览器就会打开该网址...............
   intent.setClassName("com.android.browser", "com.android.browser.BrowserActivity");  
    startActivity(intent);

六、发送邮件：
    Uri uri = Uri.parse("mailto:xxx@abc.com");   
    Intent it = new Intent(Intent.ACTION_SENDTO, uri);   
    startActivity(it);   

后续....