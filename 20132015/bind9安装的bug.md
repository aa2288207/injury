title: bind9安装的bug
tags:
  - bind
categories:
  - bind
date: 2014-06-17 05:03:25
---

Centos5

执行命令

$ /xx/named/sbin/named -c /xx/named/etc/named.conf - u named

异常提示

named: -u with Linux threads not supported: no capabilities support or capabilities disabled at build time

&nbsp;

重新安装并启用 threads 支持即可。