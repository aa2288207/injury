title: debian wheezy 7.3 apt-get简单php5 apache2配置
tags:
  - Debian
categories:
  - Linux
date: 2014-01-14 10:04:42
---

人比较懒用的apt-get 安装.   说明 debian apt-get apache2 和 apache-httpd2.x 配置是不一样的。 比如：apt-get install apache2 是木有 httpd.conf 的。

1\. 安装

mysql： apt-get install mysql-server      顺便说一下，可以不安装.

php5:  apt-get install php5      配置文件：/etc/php5/apache2/php.ini

apache2: apt-get install apache2     目录：/etc/apache2/

2\. 配置

修改 apache2.conf 里面的

# Include module configuration:
Include mods-enabled/*.load
Include mods-enabled/*.conf

为

# Include module configuration:
Include /etc/apache2/mods-enabled/*.load
Include /etc/apache2/mods-enabled/*.conf

修改最大连接数为1000

MaxKeepAliveRequests 1000

在最后加入

AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps

保存apache2.conf

3\. 测试

在 /var/www/ 新建  index.php 键入：&lt;?php phpinfo(); ?&gt;

ok, 重启一下apache 2:  servcie apache2 restart

访问一下： http://localhost/index.php.

&nbsp;

4\. /etc/apache2/sites-enabled/000-default  可以修改 DocumentRoot  即php工程目录

更多详细参考：[http://blog.csdn.net/rainysia/article/details/7056231](http://blog.csdn.net/rainysia/article/details/7056231 "debian")