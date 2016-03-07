title: python md5
tags:
  - md5
  - Python
categories:
  - Python
date: 2014-05-23 06:00:48
---

Python2.5以后版本，推荐使用的方法：

import   hashlib

my_md5 = hashlib.md5()

my_md5 = update(password)

result = my_md5.hexdigest()

&nbsp;

更多参考：http://www.qttc.net/201304314.html

http://www.cnblogs.com/the4king/archive/2012/02/06/2340660.html

http://outofmemory.cn/code-snippet/939/python-liangzhong-produce-md5-method