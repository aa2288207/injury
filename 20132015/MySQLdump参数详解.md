title: MySQLdump参数详解
tags:
  - MySQL
categories:
  - MySQL
date: 2014-09-25 07:43:35
---

mysqldump备份还原和mysqldump导入导出语句大全详解

mysqldump备份：

mysqldump -u用户名 -p密码 -h主机 数据库 a -w “sql条件” –lock-all-tables &gt; 路径

mysqldump还原：

mysqldump -u用户名 -p密码 -h主机 数据库 路径

mysqldump -uusername -ppassword dbname a –where “tag=’tagname’” –no-create-info&gt; C:\dump.sql

mysqldump按条件导入：

mysqldump -u用户名 -p密码 -h主机 数据库 &lt; 路径

案例：

mysql -uusername -ppassword dbname db_name.sql
使用以下 SQL 来备份 Innodb 表：
/usr/local/mysql/bin/mysqldump -uyejr -pyejr ”
–default-character-set=utf8 –opt –extended-insert=false ”
–triggers -R –hex-blob –single-transaction db_name &gt; db_name.sql
另外，如果想要实现在线备份，还可以使用 –master-data 参数来实现，如下：
/usr/local/mysql/bin/mysqldump -uyejr -pyejr ”
–default-character-set=utf8 –opt –master-data=1 ”
–single-transaction –flush-logs db_name &gt; db_name.sql
它只是在一开始的瞬间请求锁表，然后就刷新binlog了，而后在导出的文件中加入CHANGE MASTER 语句来指定当前备份的binlog位置，如果要把这个文件恢复到slave里去，就可以采用这种方法来做。

1.2 还原
用 mysqldump 备份出来的文件是一个可以直接倒入的 SQL 脚本，有两种方法可以将数据导入。
直接用 mysql 客户端
例如：
/usr/local/mysql/bin/mysql -uyejr -pyejr db_name &lt; db_name.sql
用 SOURCE 语法 （实验不成功！！！）
其实这不是标准的 SQL 语法，而是 mysql 客户端提供的功能，例如：
SOURCE /tmp/db_name.sql;
这里需要指定文件的绝对路径，并且必须是 mysqld 运行用户(例如 nobody)有权限读取的文件。

&nbsp;

原文：http://www.kankanews.com/ICkengine/archives/469.shtml