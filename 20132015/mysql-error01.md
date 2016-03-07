title: '创建索引失败 1452 - Cannot add or update a child row: a foreign key constraint fails'
tags:
  - MySQL
categories:
  - MySQL
date: 2014-02-28 06:38:10
---

外键的创建条件：
1.两个表必须是 InnoDB表，MyISAM表暂时不支持外键（据说以后的版本有可能支持，但至少目前不支持）；
2.外键列必须建立了索引，MySQL 4.1.2以后的版本在建立外键时会自动创建索引，但如果在较早的版本则需要显示建立；
3.外键关系的两个表的列必须是数据类型相似，也就是可 以相互转换类型的列，比如int和tinyint可以，而int和char则不可以；

4.表里面字段已经有数据了，不能存在外键引用了但被引用的值不存在.

&nbsp;

&nbsp;