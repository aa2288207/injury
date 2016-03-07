title: python 时间加减运算
tags:
  - Python
categories:
  - Python
date: 2014-08-08 03:07:45
---

>>>import datetime
>>> d1 = datetime.datetime.now()
>>> d1.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-02 17:11:07'
>>> d2 = d1 + datetime.timedelta(seconds=10)#增加10秒
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-02 17:11:17'
>>> d2 = d1 + datetime.timedelta(minutes=10)#增加10分钟
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-02 17:21:07'
>>> d2 = d1 + datetime.timedelta(hours=10)#增加10小时
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-03 03:11:07'
>>> d2 = d1 + datetime.timedelta(days=10)#增加10天
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-12 17:11:07'
>>> d2 = d1 - datetime.timedelta(seconds=10)#减去10秒
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-02 17:11:57'
>>> d2 = d1 - datetime.timedelta(minutes=10)#增加10分钟
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-02 17:01:07'
>>> d2 = d1 - datetime.timedelta(hours=10)#减去10小时
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-09-02 07:11:07'
>>> d2 = d1 - datetime.timedelta(days=10)#减去10天
>>> d2.strftime("%Y-%m-%d %H:%M:%S")
'2013-08-23 17:11:07'