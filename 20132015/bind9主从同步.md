title: bind9 主从同步 serial
tags:
  - bind
categories:
  - Linux
date: 2014-06-05 08:49:04
---

现象：slave zone 文件的日期一直更新， 但是zone文件里面的内容不变（还是乱码，据说是加密的文件）

分析：zone文件里面 SOA配置里有 serial 这个选项， master-slave更新，slave  zone文件的 serial 必须小于 master  zone文件的 serial  值。    master的zone文件在变更时会通知slave更新，slave会检查 serial  值。

解决方法：O(∩_∩)O，自己写脚本。貌似结合mysql同步可以实现，呵呵。总之不会像数据库的自增一样勾选就会了。