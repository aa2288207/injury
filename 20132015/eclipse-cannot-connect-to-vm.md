title: eclipse Cannot connect to VM
categories:
  - Java
date: 2013-12-09 07:45:20
tags:
---

eclipse 调试模式，出现 Cannot connect to VM。

原因：是windows  socket通信模块异常了。

解决方法：重置winsock

1、需要管理员的权限 打开 cmd 命令窗口
2、在命令提示字符键入netsh winsock reset    ，执行完浏览器可能无法正常访问网络。

3、重启电脑。

4、还不行，最后是我杀毒软件的问题，avast！8 网络安全版，果断卸载就可以了。