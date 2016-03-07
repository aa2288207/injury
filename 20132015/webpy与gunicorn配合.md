title: web.py serve static files in gunicorn
categories:
  - Python
tags:
  - webpy
  - Python
date: 2013-11-28 09:56:12
---

# web.py与gunicorn配合，静态文件解析。

## webpy的启动模式
```
app = web.application(urls, globals())
if __name__ == '__main__':
    app.run()
```

## gunicorn的默认启动模式是
```
app = web.application(urls, globals())
application = app.wsgifunc()
```

## gunicorn启用静态文件的启动模式是
```
app = web.application(urls, globals())

from web.httpserver import StaticMiddleware
application = app.wsgifunc(StaticMiddleware)
```

也就是说，必须要使用StaticMiddleware这个中间件，否则static文件会404

然后, <code>gunicorn -b ip:port appname:app</code> 就可以了。


膜拜文章：
[http://laiwei.net/2013/03/09/web-py-serve-static-files-in-gunicorn/](http://laiwei.net/2013/03/09/web-py-serve-static-files-in-gunicorn/)