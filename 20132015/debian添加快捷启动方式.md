title: debian添加快捷启动方式
categories:
  - Linux
tags:
  - Debian
date: 2013-08-22 22:56:06

---

**1、创建一个文件，将下面的代码拷贝进去**
这里我们只需要关注3个地方，分别为Exec=软件执行文件的路径，Icon=快捷方式图标（如果有的话），Name=快捷方式名称。根据自己软件按转的位置修改代码，保存之后关闭文件。 [

](http://www.jb51.net/os/Ubuntu/84222.html)
<div></div>
<div id="phpcode1">[Desktop Entry]
Categories=Development;
Comment[zh_CN]=
Comment=
Exec=/home/xukun/eclipse/eclipse
GenericName[zh_CN]=IDE
GenericName=IDE
Icon=/home/xukun/eclipse/icon.xpm
MimeType=
Name[zh_CN]=eclipse
Name=eclipse
Path=
StartupNotify=true
Terminal=false
Type=Application
X-DBUS-ServiceName=
X-DBUS-StartupType=
X-KDE-SubstituteUID=false
X-KDE-Username=xukun</div>
[
](http://www.jb51.net/os/Ubuntu/84222.html)**2、将文件名修改为eclipse.desktop

3、给文件添加可执行权限**
可以通过chmod +x desktop文件 或者 直接右键权限里面修改。

**4、将该文件复制到桌面**

&nbsp;

&nbsp;

参考文章:[http://www.cnblogs.com/quinnxu/archive/2013/05/30/3108847.html](http://www.cnblogs.com/quinnxu/archive/2013/05/30/3108847.html)