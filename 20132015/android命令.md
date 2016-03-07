title: Android  命令
categories:
  - Android
date: 2014-08-20 04:54:28
tags:
  - Android
---

一、命令查看端口

5037为adb默认端口 查看该端口情况如下：

netstat -aon|findstr "5037"

TCP 127.0.0.1:5037 0.0.0.0:0 LISTENING 6540

发现6540占用了 5037端口，继续查看6540的task，发现是wandoujia .如下所示

tasklist|findstr "6540"

wandoujia_daemon.exe 6540 Console 1 4,276 K

接下来问题就好解决了，在任务管理器kill掉wandoujia_daemon.exe ，运行android程序，ok .

&nbsp;

&nbsp;