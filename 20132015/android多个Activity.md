title: Android 多个Activity采用onActivityResult
categories:
  - Android
date: 2015-02-05 09:13:03
tags:
  - Android
---

假如有三个页面：Activity1，Activity2，Activity3

1、Activity1———————&gt;Activiity2:

1)  Activity1.startActivityForResult(intent, 3);

@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
if (resultCode==1&amp;&amp;requestCode == 3) {
处理3页面返回的值
}
}

2).Activity2.startActivityForResult(intent, 3);

@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
if (resultCode==1&amp;&amp;requestCode == 3) {
Activity2.setResult(1, data);
Activity2.finish();
}
}

3).Activity3. setResult(1, intent);
Activity3\. finish();

&nbsp;