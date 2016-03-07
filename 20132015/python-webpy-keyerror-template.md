title: "python webpy KeyError: '__template__'"
categories:
  - Python
date: 2013-11-27 08:43:15
tags:
  - Python
---

异常信息，如下：
<pre lang="python">
Traceback (most recent call last):
  File "d:\cnnic\python27\lib\site-packages\web\application.py", line 239, in process
    return self.handle()
  File "d:\cnnic\python27\lib\site-packages\web\application.py", line 230, in handle
    return self._delegate(fn, self.fvars, args)
  File "d:\cnnic\python27\lib\site-packages\web\application.py", line 420, in _delegate
    return handle_class(cls)
  File "d:\cnnic\python27\lib\site-packages\web\application.py", line 396, in handle_class
    return tocall(*args)
  File "D:\works\Komodo\SyServer\sy\goods\goods.py", line 41, in GET
    return render.goodsProduceProcessInfo(self.getGoodsProduceProcessInfo(goods_code))
  File "d:\cnnic\python27\lib\site-packages\web\template.py", line 1017, in __getattr__
    t = self._template(name)
  File "d:\cnnic\python27\lib\site-packages\web\template.py", line 1014, in _template
    return self._load_template(name)
  File "d:\cnnic\python27\lib\site-packages\web\template.py", line 999, in _load_template
    return Template(open(path).read(), filename=path, **self._keywords)
  File "d:\cnnic\python27\lib\site-packages\web\template.py", line 857, in __init__
    BaseTemplate.__init__(self, code=code, filename=filename, filter=filter, globals=globals, builtins=builtins)
  File "d:\cnnic\python27\lib\site-packages\web\template.py", line 797, in __init__
    self.t = self._compile(code)
  File "d:\cnnic\python27\lib\site-packages\web\template.py", line 804, in _compile
    return env['__template__']
KeyError: '__template__'
</pre>

解决方法：
html 模板页面
$def with(param)   记住啊是 with, 是 with