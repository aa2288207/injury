title: python全局变量global
categories:
  - Python
date: 2013-11-12 09:09:53
tags:
  - Python
---

python 的全局变量global 声明好纠结，在class上方声明或在__init__ 中声明，在def 中可以直接用，但不可以修改。在def中修改，需要在def重新声明一次。
```
global a
class A():
    a = 1
    def ta():
        print a

    def tb():
        global a
        a += 1
        print a

    def tc():
        a += 1
        print a
```
以上：
ta() 结果是： 1
tb() 结果是： 2
tc() 结果是： 异常error