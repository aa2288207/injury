title: 如何快速设置debian源
categories:
  - Linux
date: 2013-06-23 22:02:07
tags:
  - Linux
---

如何快速设置debian源

使用apt-spy,可以自动测试到哪个源的下载速度最快，并自动将最快的源写入配置文件

由于刚装好系统是没有apt-spy,所以先找个源先安装apt-spy

&nbsp;

1)设置临时源
vi /etc/apt/sources.list
#添加以下一行到文件最后
deb http://http.us.debian.org/debian stable main

&nbsp;

2)更新软件包列表并安装apt-spy
apt-get update
apt-get install apt-spy

&nbsp;

3)自动下载列表并使用apt-spy测试最快的源
apt-spy update
apt-spy -d stable -a asia -t 3

&nbsp;

4)查看生成的配置文件，里面是最快的源
cat /etc/apt/sources.list.d/apt-spy.list

&nbsp;

5)删除临时源
vi /etc/apt/sources.list
#删除以下一行
deb http://http.us.debian.org/debian stable main

&nbsp;

6）更新软件包列表
apt-get update

完成！

&nbsp;

-------

source:高进波Linux博客

filepath:http://www.gaojinbo.com/%E5%A6%82%E4%BD%95%E8%AE%BE%E7%BD%AE%E5%BF%AB%E9%80%9F%E7%9A%84debian%E6%BA%90.html