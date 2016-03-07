title: "Can't start server : Bind on unix socket: Permission denied  "
categories:
  - MySQL
date: 2014-10-08 07:31:12
tags:
  - MySQL
---

这个bug也提示：* The server quit without updating PID file

解决方法(看红色字体)：

[mysqld]
datadir=/usr/local/mysql/data
<span style="color: #ff0000;">socket=/tmp/mysql.sock</span>

[mysql]
<span style="color: #ff0000;">socket=/tmp/mysql.sock</span>
[mysql.server]
user=mysql
basedir=/usr/local/mysql

[safe_mysqld]
err-log=/usr/local/mysql/mysqld.log
pid-file=/usr/local/mysql/mysqld.pid

&nbsp;

参考：http://rickie622.blog.163.com/blog/static/21238811201112885256860/