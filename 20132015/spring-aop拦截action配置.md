title: spring aop拦截action配置
tags:
  - java
  - spring aop
  - struts2
categories:
  - Java
date: 2014-05-13 07:29:25
---

struts.xml:

//让struts2始终先考虑spring的自动装箱,Struts2的action由Spring来负责进行实例化

&lt;constant name="struts.objectFactory.spring.autoWire.alwaysRespect" value="true" /&gt;

applicationContext.xml:

//<span style="color: #454545;">表示使用CGLib动态代理技术织入增强</span>

&lt;aop:aspectj-autoproxy proxy-target-class="true"/&gt;

否则可能出现：<span style="color: #323232;">**NoSuchMethodException**</span>

解疑：为什么需要启用 cglib 动态代理？

spring的动态代理如果不指定，他会根据类的信息来进行代理，

如果类有接口的会使用JDK的动态代理，

如果类没有接口的就会使用cglib，

因为struts2的ActionSupport是有实现接口的，所以他用了JDK的动态代理，那样你类中自己的属性自然就没有了。

而你指定了使用cglib，那他就会动态生成一个继承你这个Action的子类，自然你Action类中可供子类访问的属性都有了。

参考：http://bbs.csdn.net/topics/390630278

参考2：http://blog.csdn.net/unei66/article/details/9422339