title: flask-sqlalchemy  关联关系说明
tags:
  - flask
  - flask-sqlalchemy
categories:
  - Python
date: 2014-09-04 03:49:15
---

sqlalchemy.exc.AmbiguousForeignKeysError:
Could not determine join condition between parent/child tables on relationship UserInfo.role - there are multiple foreign key paths linking the tables.
Specify the 'foreign_keys' argument, providing a list of those columns which should be counted as containing a foreign key reference to the parent table.

异常说的是。UserInfo.role 引用关系不明确写法：**<span style="color: #008000;"> role = db.relationship('RoleInfo')  </span>**

正确写法如下举例：

class UserInfo(db.Model):
------- id = db.Column(db.Integer, primary_key=True)
------- role_id = db.Column(db.Integer, db.ForeignKey('role_info.id'))
-------**<span style="color: #008000;"> role = db.relationship('RoleInfo', foreign_keys=[role_id])</span>**
------- creator = db.Column(db.Integer, db.ForeignKey('user_info.id'))
------- creator_obj = db.relationship('UserInfo', **<span style="color: #800000;">remote_side=id</span>**)

class RoleInfo(db.Model):
------id = db.Column(db.Integer, primary_key=True)
------creator = db.Column(db.Integer, db.ForeignKey('user_info.id'))
------creator_obj = db.relationship('UserInfo',**<span style="color: #800000;"> primaryjoin='RoleInfo.creator==UserInfo.id'</span>**)

&nbsp;

关联自己需要用到 **<span style="color: #800000;">remote_side</span>** 属性。

&nbsp;