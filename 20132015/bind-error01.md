title: 'configure: error: no acceptable C compiler found in $PATH '
tags:
  - bind
categories:
  - Linux
date: 2014-05-20 07:57:58
---

bind9.10安装error: configure: error: no acceptable C compiler found in $PATH

原因：没有安装gcc

解决方法：

debian/ubuntu：<code>sudo apt-get install gcc</code>

redhat/centos: <code>sudo yum install gcc</code>