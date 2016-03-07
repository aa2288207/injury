title: 'configure: error: OpenSSL was not found in any of '
tags:
  - bind
categories:
  - Linux
date: 2014-05-20 08:01:26
---

bind9.10安装error: <code>configure: error: OpenSSL was not found in any of </code>

原因：没有安装 openssl-devel

解决方法：

debin/ubuntu: <code>sudo apt-get install openssl</code>

<code>sudo apt-get install libssl-dev</code>

<code>redhat/centos: sudo yum install openssl-devel</code>

参考：[http://f.dataguru.cn/thread-139312-1-1.html](http://f.dataguru.cn/thread-139312-1-1.html)