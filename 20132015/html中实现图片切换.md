title: html中实现图片切换
categories:
  - Android
date: 2013-09-02 11:19:30
tags:
  - Android
---

一、用JS实现：
```
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<title>无标题文档</title>
</head>
<script language="javascript" type="text/javascript">
function cursor(str){
var id = document.getElementById(str);
id.style.visibility = "visible";
}
function hidecursor(str){
var id = document.getElementById(str);
id.style.visibility = "hidden";
}
</script>
<body>
<div style=" background-image:url(http://img04.taobaocdn.com/imgextra/i4/641929016/T2.8OjXdXdXXXXXXXX_!!641929016.jpg); width:950px; height:120px;">
<div style="position:relative;z-index:2; width:25px; height:10px;margin:auto; margin-right:438px;" align="right"><a href="http://holdxl.taobao.com/category-777995204.htm?spm=a1z10.3.0.0.CZfeDt&amp;amp;search=y&amp;amp;catName=电信充值" onMouseMove="hidecursor('img1')" onMouseOut="cursor('img1')"><img id="img1" src="http://img03.taobaocdn.com/imgextra/i3/641929016/T2lpM6Xo8XXXXXXXXX_!!641929016.png_100x100.jpg" style=" position:relative;margin-top:21px;border:none; " /></a></div>
</div>
</body>
</html>
```

二、DIV+CSS实现：
```
<html>
<title></title>
<head></head>
<body>
<style type="text/css">
#a1{position:relative; border:none; width:54px; height:53px; display:block;}
#a1:hover{background-image:url(http://img03.taobaocdn.com/imgextra/i3/641929016/T2TsGUXfdbXXXXXXXX_!!641929016.png_100x100.jpg)}
</style>
<div style="position:relative;z-index:2; width:25px; height:10px; margin:auto; margin-right:325px; margin-top:-5px;" ><a href="http://holdxl.taobao.com/category-777995210.htm?spm=a1z10.3.0.0.QpOsuZ&amp;search=y&amp;catName=%D2%C6%B6%AF%B3%E4%D6%B5" id="a1"></a></div>

</div>
</body>
</html>
```