title: debian openjdk
tags:
  - Debian
  - jdk
  - openjdk
categories:
  - Java
  - Linux
date: 2014-01-03 03:14:28
---

先说一下jdk和jre吧

jre 是java运行环境，比如说我用eclipse是做python开发的，我只安装jre就可以了，保证eclipse可以跑起来。

jdk是java开发环境，jdk包含jar 如果安装jdk可以不用载安装jre了，一般安装sun jdk 7 都会选2次路径，第二次选的是jre的路径，可以不安装的。(我没测试过)

&nbsp;

再说一下sun jdk 和 openjdk吧,推荐用sun jdk 吧，目前是这样的，openjdk貌似不是那么完善，但是群众们说未来openjdk 才是王道。如果你想折腾的话搞搞 openjdk.

&nbsp;

debian 7.3 默认的 openjdk-6-jre   和 openjdk-6-jdk

卸载：apt-get autoremove --purge openjdk-6-*

ps：卸载 openjdk-6 貌似会给安装 openjdk-7吧，感觉是这样的卸载是控制台输出的内容。偶也是瞎折腾。

&nbsp;

debian 安装 openjdk-7

jdk:  apt-get install openjdk-7-jdk

jre:   apt-get install openjdk-7-jre

卸载：apt-get autoremove --purge openjdk-7-*

ps:  --purge  是清除配置或缓存文件的。

&nbsp;

debian 安装 sun jdk7 参考：[http://holdlg.coding.io/?p=587](http://holdlg.coding.io/?p=587)