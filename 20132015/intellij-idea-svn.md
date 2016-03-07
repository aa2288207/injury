title: intelliJ IDEA svn 插件
tags:
  - IntelliJ
categories:
  - Java
date: 2015-03-24 04:43:00
---

*   intelliJ IDEA 提示：Can’t use Subversion command line client:svn
*   原因： 没有svn的可执行命令。
*   解决办法：

        1.  如果没有安装 svn 可执行命令，可以在[http://subversion.apache.org/packages.html#windows](http://subversion.apache.org/packages.html#windows)下载，推荐 SlikSVN 只有核心部分,典型（typical）安装即可。
    2.  在intellij IDEA界面，file->settings->version control -> subversion -> use command line client 填写路径 X:/yourpath/slivsvn/bin/svn.exe
    3.  如果安装过了相关的svn可执行文件，重复2操作。