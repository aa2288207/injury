title: python xml解析之xml.etree.ElementTree
categories:
  - Python2
tags:
  - xml
date: 2013-08-14 16:58:19
---

实例xml如下

```
<?xml version="1.0" encoding="UTF-8"?>

<Root>

<NewsView>
<Column Id="10"  Name="头条"  />
<Column Id="15"  Name="中央要闻"  />
<Column Id="18"  Name="地方组织要闻"  />
<Column Id="19"  Name="社会活动新闻"  />
<Column Id="18"  Name="会员动态"  />
<Column Id="17"  Name="一周简报"/>
</NewsView>

<NewsView>
<Column Id="140"  Name="头条"  />
<Column Id="105"  Name="中央要闻"  />
<Column Id="138"  Name="地方组织要闻"  />
<Column Id="109"  Name="社会活动新闻"  />
<Column Id="198"  Name="会员动态"  />
<Column Id="197"  Name="一周简报"/>
</NewsView>

</Root>
```

python 代码
```
# -*- coding: utf-8 -*-
'''
Created on 2013年8月14日

@author: dui
'''

import os
from xml.etree import ElementTree  # xml解析类库

def getxml(xmlpath):
try:
widgets = ElementTree.parse(xmlpath)    # 读取xml文件
# print widgets
newsViews = widgets.getiterator('NewsView')  # 查找 NewsView 节点
for newsView in newsViews:                      # 循环NewsView节点
print '%s:%s' % (newsView.tag,newsView.text)   # 输出节点和节点文本
#result.append(Column.attrib)
for child in newsView.getchildren():         # 查找NewsView 子节点  Column.xml
print 'Id:%s' % (child.get('Id'))        # 获取节点Id 并输出
print 'Name:%s' % (child.get('Name'))    # 获取节点Name 并输出
except Exception, e:
print e
return 'ok'

if __name__ == "__main__":
xmlpath = '%s\SubColumn.xml' % os.getcwd()   # xml文件位置
print xmlpath
getxml(xmlpath)
```

执行结果:

E:\work\workspace_python\Test\src\Test\SubColumn.xml
NewsView:

Id:10
Name:头条
Id:15
Name:中央要闻
Id:18
Name:地方组织要闻
Id:19
Name:社会活动新闻
Id:18
Name:会员动态
Id:17
Name:一周简报
NewsView:

Id:140
Name:头条
Id:105
Name:中央要闻
Id:138
Name:地方组织要闻
Id:109
Name:社会活动新闻
Id:198
Name:会员动态
Id:197
Name:一周简报
完毕.