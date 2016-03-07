title: Android webview 调用JS 打成apk后不能调用
categories:
  - Android
date: 2015-02-02 03:42:09
tags:
  - Android
---

今天有一个bug，就是webview跟js交互的方法怎么也调不起来，debug包没问题，release包就出错，想想是打包时混淆的问题，打了一个不混淆的包，果不其然，就是混淆的问题。

然后就找解决方案，在proguard-project文件中有这么一句

-keepclassmembers   class org.hdt.info.util.JavaScriptInterfaceClass{*;}

把-keepclassmembers   class org.hdt.info.util.JavaScriptInterfaceClass{*;}换成你自己定义的那个类名（包名也必须有，如果定义的是内部类，则是cn.wj.ui.WebViewActivity$myInterface），在4.1的系统上是没有问题了，但4.2的机子上还是不行，再找找，哦，原来是4.2以上版本调用js接口需要在方法使用声明@JavascriptInterface,然后混淆时可能会弄丢该声明导致，程序无法调用js，需要继续再配置文件中添加条件，

-keepattributes *Annotation*
-keepattributes *JavascriptInterface*

&nbsp;

引用 文章：http://blog.csdn.net/minenamewj/article/details/40112335