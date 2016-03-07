```
Author: holdlg
Last updated: 2016-03-07 10:23:04
```

# 数据库命名规范

## [数据库规范]

 - 命名尽量简洁明义，能够一眼看出来这个数据库是用来做什么的;
 - 命名使用名词作为数据库名称，并且只用英文，不用中文拼音;
 - 命名使用英文字母，全部小写，控制在3-7个字母以内;
 - 命名如果有多个单词，使用下划线链接;
 - 使用<code>utf8</code>字符集，字符校验规则<code>utf8_general_ci</code>;
 ```
 CREATE DATABASE `elijah` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
 ```

## [表规范]

 - 命名统一前缀，相关功能的表使用相同前缀，<code>模块名_表名</code>，如:<code>manage_user</code>;
 - 命名使用英文小写单词，有多个单词用下划线链接;
 - 命名使用常见单词，避免使用长单词和生僻词;
 - 表引擎采用MyISAM;
 - 表必须有主键，均使用auto_increment的id作为主键(与业务无关),和业务相关的要做为唯一索引;
 - 使用<code>utf8</code>字符集，字符校验规则<code>utf8_general_ci</code>;
 - 表加备注，表明表中存放的数据内容;

## [字段规范]

 - 使用小写英文单词，尽量用单个单词表示，如果有多个单词使用下划线链接;
 - 使用简单单词，避免生僻词;
 - 字段应当有注释，描述该字段的用途及可能存储的内容;
 - 是别的表的外键均使用<code>表名_id</code>的方式来表明;
 - 表的主键一般都约定成为id，自增类型;
 - 时间字段，采用timestamp类型;
 - 使用<code>utf8</code>字符集，字符校验规则<code>utf8_general_ci</code>;

## [参考示例]
```
CREATE TABLE `right_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '自增id',
  `account` varchar(50) NOT NULL COMMENT '账号',
  `password` varchar(500) NOT NULL COMMENT '哈希密码',
  `photo` varchar(225) NOT NULL COMMENT '用户头像',
  `status` int NOT NULL COMMENT '用户状态 0.禁用 1.启用',
  `right_role_id` int NOT NULL COMMENT '用户角色关联角色表id',
  PRIMARY KEY (`id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 COMMENT '用户表';
```

# MyISAM与InnoDB的主要区别
[点击查看](http://www.ha97.com/4197.html)


# 数据库安装和常用管理命令

## 1.安装MySQL5.6
```
sudo apt-get install mysql-server-5.6
```

## 2.设置编码,sudo vim /etc/mysql/my.cnf
```
[client]
default-character-set=utf8

[mysqld]
character-set-server=utf8  
collation-server=utf8_general_ci
```

## 3.查看编码格式
```
SHOW VARIABLES LIKE 'character_set_%';
```

## 4.修改密码
```
update mysql.user set password=PASSWORD("") where user="root";
flush privileges;
```

## 5.启用远程链接
```
1、授权
    grant all privileges on *.*  to 'root'@'%' identified by 'root' with grant option;
    flush privileges;
2、修改/etc/mysql/my.conf
    找到bind-address = 127.0.0.1 这一行
    改为bind-address = 0.0.0.0   即可
3、重启
    sudo service mysql restart
```

## 6. windows mysql服务注册和卸载
```
mysqld --install MySQL5.6 --defaults-file="my.ini"
mysqld --remove MySQL5.6
```

## 7. windows pip install mysqldb
1. [下载](http://www.lfd.uci.edu/~gohlke/pythonlibs/#mysql-python)
2. 安装<code>pip install /path/MySQL_python-1.2.5-cp27-none-win_amd64.whl