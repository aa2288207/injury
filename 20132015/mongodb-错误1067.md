title: mongodb启动服务时候报错。错误1067，进程意外终止。
tags:
  - MongoDB
categories:
  - MongoDB
date: 2013-12-13 01:54:35
---

![1067](http://pic2.filec2c.com/doimg/holdlg/aeb534c9/)
&nbsp;

偶mongodb  版本：2.4.8 滴

类似还有：错误1053

解决方法：

1.  网友们分享：是删掉mongod.lock这个文件，然后重新启动。mongod.lock这个文件在你的数据库文件夹里面。
2.  偶的方法是：修改配置文件，mongo.cfg  添加dbpath 值，如图：
[mongo.cfg](http://pic3.filec2c.com/doimg/holdlg/302d0e55/)

参考文章：[http://www.cnblogs.com/lipan/archive/2011/03/08/1966463.html](http://www.cnblogs.com/lipan/archive/2011/03/08/1966463.html "mongodb")
官方文档：[http://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/ "mongodb document")     记得选版本哦。