title: Android 调用系统发送彩信
categories:
  - Android
date: 2014-05-14 02:47:41
tags:
  - Android
---

彩信知识点：

# 1.Intent界面跳转：
```
Intent.ACTION_SENDTO  无附件的发送
Intent.ACTION_SEND  带附件的发送
Intent.ACTION_SEND_MULTIPLE  带有多附件的发送
```

# 2.群发功能：
```
String address="100861111;100861111111"; 联系人用“；”隔开
```

# 3.多附件，支持幻灯片形式发送：
```
//多附件操作方法

String picUrl="file:///sdcard/aa.jpg";
String url2="file:///sdcard/bb.jpg";
Uri uri1=Uri.parse(picUrl);
Uri uri2=Uri.parse(url2);
ArrayList&lt;Uri&gt; uris=new ArrayList&lt;Uri&gt;();
uris.add(uri1);
uris.add(uri2);

Intent intent = new Intent(Intent.ACTION_SEND_MULTIPLE);

intent.putExtra(Intent.EXTRA_STREAM, uris);// uri为你的附件的uri
```

# 4. 彩信中的格式必须是这样的：

```
String picUrl="file:///sdcard/aa.jpg"; 否则报发送彩信无法将图片添加到信息

单附件群发Demo：

//发送彩信的图片路径
String picUrl=Environment.getExternalStorageDirectory().getAbsolutePath()+"/aa.jpg";

File file = new File(picUrl);
Uri uri1=Uri.fromFile(file);

Intent intent = new Intent(Intent.ACTION_SEND);
String address="100861111;100861111111";
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
intent.putExtra(Intent.EXTRA_STREAM, uri1);// uri为你的附件的uri

intent.putExtra("subject", "it's subject"); //彩信的主题
intent.putExtra("address", address); //彩信发送目的号码
intent.putExtra("sms_body", "it's content"); //彩信中文字内容
intent.setType("image/*");// 彩信附件类型
intent.setPackage("com.android.mms");
startActivity(intent);
```