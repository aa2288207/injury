title: linux mysql的启动问题 ERROR! The server quit without updating PID file
categories:
  - Linux
date: 2013-10-10 14:51:53
tags:
  - Linux
---

<pre>控制台：</pre>
<pre id="answer-content-185797375">ERROR! The server quit without updating PID file</pre>
<pre id="answer-content-185797375">
错误日志：
080523 7:53:28 [ERROR] Can't start server : Bind on unix socket: Permission denied

080523 7:53:28 [ERROR] Do you already have another mysqld server running on socket: /tmp/mysql.sock ? 

排查为 mysql.sock 文件找不到的问题。

参考文章:[http://blog.csdn.net/faye0412/article/details/7038290

](http://blog.csdn.net/faye0412/article/details/7038290)**我的解决方法**： 重新复制一下 <span style="color: #0000ff;">**/usr/share/mysql/my-large.cnf**</span> 为 **<span style="color: #0000ff;">/etc/my.cnf</span>**  即ok

参考文章：[http://blog.csdn.net/zengmuansha/article/details/9081281](http://blog.csdn.net/zengmuansha/article/details/9081281)</pre>