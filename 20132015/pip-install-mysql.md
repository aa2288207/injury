title: pip install MySQL-python 异常
tags:
  - MySQLdb
categories:
  - Linux
  - Python
date: 2014-09-19 08:38:01
---

当 pip install MySQL-python  显示如下bug

bug:

Command /usr/bin/python -c "import setuptools, tokenize;__file__='/tmp/pip_build_root/MySQL-python/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /tmp/pip-KumJOi-record/install-record.txt --single-version-externally-managed --compile failed with error code 1 in /tmp/pip_build_root/MySQL-python

&nbsp;

&nbsp;

UnicodeDecodeError: 'ascii' codec can't decode byte 0xe2 in position 65: ordinal not in range(128)

&nbsp;

你需要  yum install  mysql-devel  然后再安装就OK了。