```
Author: holdlg
Last updated: 2016-03-15 10:23:04
```

# jinja2 2.7 自定义过滤器
## 定义过滤器
```
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

# jinja2 自定义过滤器 注册方式
def show_binary(value):
    """ value值解码失败，返回Binary，避免页面异常"""
    try:
        return value.decode('utf-8')
    except:
        return 'Binary'
# 此处filters可自定义名称
app.jinja_env.filters['show_binary'] = show_binary


# jinja2 自定义过滤器 装饰器方式
@app.template_filter('show_binary')
def show_binary(value):
    """ value值解码失败，返回Binary，避免页面异常"""
    try:
        return value.decode('utf-8')
    except:
        return 'Binary'

if __name__ == "__main__":
    app.run()
```

## 使用过滤器,在模板html中
```
{{value|show_binary}}
```