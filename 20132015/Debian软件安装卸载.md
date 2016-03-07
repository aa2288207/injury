title: Debian 软件安装卸载
categories:
  - Linux
date: 2013-08-21 11:37:02
tags:
  - apt-get
---

方法一：可以用终端安装或卸载软件。

方法二：

用系统自带的“新立得软件包管理器” 在终端里安装软件 apt-get install softname1 softname2 softname3……

卸载软件 apt-get remove softname1 softname2 softname3……

卸载并清除配置 apt-get remove --purge softname1

更新软件信息数据库 apt-get update

进行系统升级 apt-get upgrade

搜索软件包 apt-cache search softname1 softname2 softname3……

安装deb软件包 dpkg -i xxx.deb

删除软件包 dpkg -r xxx.deb

连同配置文件一起删除 dpkg -r --purge xxx.deb

查看软件包信息 dpkg -info xxx.deb

查看文件拷贝详情 dpkg -L xxx.deb

查看系统中已安装软件包信息 dpkg -l

重新配置软件包 dpkg-reconfigure xxx

在“新立得”里 点搜索，输入软件名在需要安装或卸载的软件上右击－点标记－最后点应用

&nbsp;

参考文章：[http://hi.baidu.com/arm_dsp/item/2f97ff5a251685a8acc857be](http://hi.baidu.com/arm_dsp/item/2f97ff5a251685a8acc857be)