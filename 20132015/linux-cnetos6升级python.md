title: linux cnetos6.5 升级 python2.7.8
tags:
  - pip
  - Python
categories:
  - Python
date: 2014-09-19 08:00:44
---

各种坑。  python.tar.xz 编译安装正常。安装 pip 缺少 zlib 相关包，缺少openssl openssl-devel 包  每次更新包，需要重新编译 python。 好坑。装之前 参考:[ http://www.cnblogs.com/balaamwe/p/3480430.html](http://www.cnblogs.com/balaamwe/p/3480430.html)