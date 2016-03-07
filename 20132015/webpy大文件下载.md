title: web.py大文件下载
categories:
  - Python
tags:
  - Python
  - webpy
date: 2013-11-11 02:57:43
---

需要下载大文件的时候，如果先将文件直接读入内容再返回，那肯定就很浪费内存，甚至会崩溃。

所以我们需要读一些内容然后直接flush给客户端，但是web.py的文档里面却没有找到flush的方法。

不过在web.py的cookbook中的How to Stream Large Files中看到可以直接yield返回内容。所以，我们可以使用yield来做flush做的事情。

```
BUF_SIZE = 2048000
class upCenterBigDownload(object):
    def GET(self):
        file_name = 'file_name'
        file_path = os.path.join('file_path', file_name)
        f = None
        try:
            f = open(file_path, "rb")
            web.header('Content-Type','application/octet-stream')
            web.header('Content-disposition', 'attachment; filename=%s.dat' % file_name)
            while True:
                c = f.read(BUF_SIZE)
                if c:
                    yield c
                else:
                    break
        except Exception, e:
            print e
            yield 'Error'
        finally:
            if f:
                f.close()
```
来源：http://www.cnblogs.com/QLeelulu/archive/2011/08/05/2128577.html