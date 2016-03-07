title: pyqt4 查看源代码
categories:
  - Python
date: 2013-12-10 06:12:42
tags:
  - pyqt4
---

用pyqt4 窗口--&gt;查看源代码, 一般会弹窗口，  不能启动 C:/Python27/Lib/site-packages/PyQt4\uic。

网上的解决方法是：
pyqt4：pyuic4 -o codeFile.py -x yourUIfile.ui
pyqt5：pyuic5 -o codeFile.py -x yourUIfile.ui

偶也没找到其他好的方法，用了一下批处理命令，做了个 bat脚本。如下

```
pyuic4 -o untitled.py -x untitled.ui
```

保存到 *.bat 文件，每次双击即可。