title: Linux(Debian/ubuntu)下Python MySQL支持
categories:
  - python
date: 2013-09-04 18:10:42
tags:
  - MySQLdb
---

>>> import MySQLdb

ImportError: No module named MySQLdb

看到以上信息表示MySQL支持无效。


解决方法

ubuntu /debian系统

直接

sudo apt-get install python-mysqldb

即可。

如果编译

需要 sudo apt-get install libmysqlclient-dev