title: Linux top命令操作指令
categories:
  - Linux
date: 2013-12-10 03:04:38
tags:
  - Linux
---

有关top命令前四行内容定义解析，请参照：[http://os.51cto.com/art/201108/285581.htm](http://os.51cto.com/art/201108/285581.htm)

&nbsp;

下面我列出一些常用的linux top命令操作指令：

q：退出top命令

<Space>：立即刷新

s：设置刷新时间间隔

c：显示命令完全模式

t:：显示或隐藏进程和CPU状态信息

m：显示或隐藏内存状态信息

l：显示或隐藏uptime信息

f：增加或减少进程显示标志

S：累计模式，会把已完成或退出的子进程占用的CPU时间累计到父进程的MITE+

P：按%CPU使用率排行

T：按MITE+排行

M：按%MEM排行

u：指定显示用户进程

r：修改进程renice值

kkill：进程

i：只显示正在运行的进程

W：保存对top的设置到文件~/.toprc，下次启动将自动调用toprc文件的设置。

h：帮助命令。