title: flask 学习
categories:
  - Python
tags:
  - flask
date: 2016-01-21 14:36:47
---

# from flask import request
```
form
一个包含解析过的从 POST 或 PUT 请求发送的表单对象的 MultiDict 。
请注意上传的文件不会在这里，而是在 files 属性中。

args
一个包含解析过的查询字符串（ URL 中问号后的部分）内容的 MultiDict 。

values
一个包含 form 和 args 全部内容的 CombinedMultiDict 。

cookies
一个包含请求中传送的所有 cookie 内容的 dict 。

stream
如果表单提交的数据没有以已知的 mimetype 编码，
为性能考虑，数据会不经修改存储在这个流中。
大多数情况下，使用可以把数据提供为字符串的 data 是
更好的方法。流只返回一次数据。

headers
进入请求的标头存为一个类似字典的对象。

data
如果进入的请求数据是 Flask 不能
处理的 mimetype ，数据将作为字符串存于此。

files
一个包含 POST 和 PUT 请求中上传的文件的 MultiDict 。
每个文件存储为 FileStorage 对象。其基本的行为类似
你在 Python 中见到的标准文件对象，差异在于这个对象
有一个 save() 方法可以把文件存储到文件系统上。

environ
底层的 WSGI 环境。

method
当前请求的 HTTP 方法 (POST ， GET 等等)

get_json
获取json数据，注意json格式,windows下写法是:  "{\"Hello\":\"Karl\"}"

json
获取json数据，注意json格式,windows下写法是:  "{\"Hello\":\"Karl\"}"

path
url
url_root
base_url
script_root

------------
用法
request.args.get('name', 'default vlaue')
request.form.get('name', 'default vlaue')
request.json.get('name', 'default vlaue')
request.json['name']
```
