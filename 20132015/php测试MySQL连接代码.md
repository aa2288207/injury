title: php测试MySQL连接代码
tags:
  - php
categories:
  - MySQL
date: 2013-11-10 05:44:06
---

测试代码如下:
```
<?php
     $link=mysql_connect('localhost','root','root');
     if(!$link) echo "ok!";
        else echo "error!";
     mysql_close();
?>
```