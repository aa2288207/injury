title: Android 调用百度地图
categories:
  - Android
date: 2013-12-13 15:54:14
tags:
  - Android
---

# 一.环境要求

配置KEY：eclipse——>windows-——>perference——>SHA1 获得数字签证

数字签证+";"+项目包名

需要的Jar包：SDKJar包，libBaiduMapSDK_v2_3_1.so（动态类）

# 二.配置文件中必须加的权限
```
<!-- 使用网络权限 -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
<!--  获取设置信息和详情页直接拨打电话需要以下权限  -->
<uses-permission android:name="android.permission.CALL_PHONE"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
<!-- SDK离线地图和cache功能需要读写外部存储 -->
<uses-permission android:name="android.permission.WRITE_SETTINGS"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

# 三.Activity 里面需要注意
```
//注意：请在试用setContentView前初始化BMapManager对象，否则会报错
BMapManager   mBMapMan=new BMapManager(getApplication());  mBMapMan.init("我的Key", null);
```

# 四. 网络判断
```
// 常用事件监听，用来处理通常的网络错误，授权验证错误等
class MyListener implements MKGeneralListener {

@Override
// 判断网络错误
public void onGetNetworkState(int arg0) {
if (arg0 == MKEvent.ERROR_NETWORK_CONNECT) {
Toast.makeText(MapActivity.this, "您的网络出错啦！", Toast.LENGTH_LONG)
.show();
} else if (arg0 == MKEvent.ERROR_NETWORK_DATA) {
Toast.makeText(MapActivity.this, "输入正确的检索条件！",
Toast.LENGTH_LONG).show();
}
// ...

}

@Override
// 判断KEY 授权认证
public void onGetPermissionState(int arg0) {
// 非零值表示key验证未通过
if (arg0 != 0) {
// 授权Key错误：
Toast.makeText(MapActivity.this,
"请输入正确的授权Key,并检查您的网络连接是否正常！error: " + arg0,
Toast.LENGTH_LONG).show();
} else {
Toast.makeText(MapActivity.this, "key认证成功", Toast.LENGTH_SHORT)
.show();
}

}

}
```