title: python 一句话输出26个英文字母
categories:
  - Python
date: 2013-08-28 10:43:26
tags:
  - Python
---

原文：[http://blog.sina.com.cn/s/blog_494e28800100jvlb.html](http://blog.sina.com.cn/s/blog_494e28800100jvlb.html)


chr(i) # return i character
ord(c) # return integer
cmp(x,y) # 比较x,y大小,  <wbr />小于-1 等于0 大小1

>>> chr(97)
'a'
>>> ord('a')
97
>>> cmp(5,6)
-1
>>> cmp(6,5)
1
>>> cmp(6,6)
0

>>> [chr(i) for i in range(97,123)]
['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']

>>>