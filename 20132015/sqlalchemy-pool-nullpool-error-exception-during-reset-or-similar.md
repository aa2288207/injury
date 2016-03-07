title: [sqlalchemy.pool.NullPool] ERROR: Exception during reset or similar
categories:
  - Python
tags:
  - Python
  - sqlalchemy
date: 2015-03-23 07:44:01
---

异常错误信息： ProgrammingError: SQLite objects created in a thread can only be used in that same thread.The object was created in thread id 139938739435328 and this is thread id 139938622985984

解决方法：**connect_args={'check_same_thread':False}**
原因：sqlite3线程锁 的问题
其他：sqlalchemy 0.7 升级至 0.9 造成的。

举例代码如下：
```
    from sqlalchemy.pool import StaticPool
    engine = create_engine('sqlite://',
                    connect_args={'check_same_thread':False},
                    poolclass=StaticPool)
```

参考：[http://docs.sqlalchemy.org/en/rel_0_7/dialects/sqlite.html](http://docs.sqlalchemy.org/en/rel_0_7/dialects/sqlite.html)