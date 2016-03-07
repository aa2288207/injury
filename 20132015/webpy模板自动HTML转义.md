title: webpy模板自动HTML转义
categories:
  - Python
tags:
  - Python
date: 2013-11-11 06:10:31

---

要注意 web.py 将会转义任何任何用到的变量，所以当你将 name 的值设为是一段 HTML 时，它会被转义显示成纯文本。

如果要关闭该选项，可以写成 $:name 来代替 $name。 

如果我们想部分转移，怎么办？ webpy显然提供了转移函数，我们在应用层直接调用就可以了。 

from  web.net  import  htmlquote

htmlquote(raw_text)

参考来源:http://www.itdiffer.com/index.php?doc-view-595.html