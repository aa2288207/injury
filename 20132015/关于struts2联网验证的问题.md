title: 关于struts2联网验证的问题
tags:
  - java
categories:
  - Java
date: 2014-02-13 09:00:24
---

error:  http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd - [unknown location]

解决方法：把xxxAction-validator.xml 验证的文件的头信息修改一下，如：

原xml

[xml]

&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE validators PUBLIC "-//OpenSymphony Group//XWork Validator 1.0.2//EN" "http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd"&gt;

[/xml]

修改后的xml

[xml]

&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE validators PUBLIC  "-//Apache Struts//XWork Validator 1.0.2//EN"  "http://struts.apache.org/dtds/xwork-validator-1.0.2.dtd"&gt;

[/xml]

&nbsp;

参考文章：http://blog.csdn.net/zhoulianglg/article/details/9364411