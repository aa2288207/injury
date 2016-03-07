title: Debian下运行GUI程序出现”No protocol specified“错误
categories:
  - Linux
date: 2013-08-20 12:59:23
tags:
  - Debian
---

普通用户下正常，root下运行错误，发现是xserver对root的访问拒绝。
把/home/user/.Xauthority拷贝到/root下

cp   /home/duidui/.Xauthority    /root/

问题解决。

参考文章:[http://linux.chinaunix.net/techdoc/net/2009/06/09/1117575.shtml](http://linux.chinaunix.net/techdoc/net/2009/06/09/1117575.shtml)