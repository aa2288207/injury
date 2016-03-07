title: 安装失败，无法启动google chrome 安装程序
tags:
  - chrome
categories:
  - chrome
date: 2014-01-26 02:17:56
---

xx.. 不知道肿么， chrome 的主页被修改成了， hao123.com  好坑。 各种设置无效。

于是直接删了， C:\Program Files\Google  这个文件夹。 然后重装就报了这个错误:   安装失败，无法启动google chrome 安装程序.

google了一下，说删 HKEY_CURRENT_USER 下面的 ..\Google\Update\clinet* 开头的。 但是不行。

&nbsp;

我删了  HKEY_LOCAL_MACHINE\SOFTWARE\Google\Update\Clinet*  开始的。 然后就ok了。

&nbsp;

这个主页是 GoogleUpdate.exe 的问题。 注册表搜索一下del ，就ok了。