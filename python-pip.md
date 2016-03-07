title: windwos pip-cache-error
categories:
  - Python
  - pip
tags:
  - pip
date: 2015-12-26 20:35:39
---

# error信息：
```
  Hash of the package https://pypi.python.org/packages/source/p/pdfminer/pdfminer-20140328.tar.gz#md5=dfe3eb1b7b7017ab514aad6751a7c2ea (from https://pypi.python.org/simple/pdfminer/) (94e0d5d7dd467fb44467c76be9c977c4) doesn't match the expected hash dfe3eb1b7b7017ab514aad6751a7c2ea!
Bad md5 hash for package https://pypi.python.org/packages/source/p/pdfminer/pdfminer-20140328.tar.gz#md5=dfe3eb1b7b7017ab514aad6751a7c2ea (from https://pypi.python.org/simple/pdfminer/)
```

# windows 解法
删除<code>C:\Users\yourname\AppData\Local\pip\cache\http\</code>下相应的安装文件

# linux 解法
删除<code>sudo rm -rf /root/.pip/cache</code>下相应的安装文件
