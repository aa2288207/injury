title: BoundMetaData is not defined error in SQLAlchemy
tags:
  - sqlalchemy
categories:
  - Python
date: 2014-07-02 05:41:18
---

```
from sqlalchemy import *

db = create_engine('sqlite:///test.db')
metadata = MetaData(db)

参考地址：http://www.mohdshakir.net/2007/12/13/boundmetadata-is-not-defined
```