title: jar不是内部或外部命令 解法
categories:
  - java
date: 2013-12-09 01:26:57
tags:
  - java
---

1.看你的jdk版本的bin里面是否有javac.exe  和 jar.exe

2. 检查环境变量。

JAVA_HOME =D:\jdk\JDK1.6

PATH =%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

CLASSPATH = .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar

3. 修改path相关java的值，用绝对地址，不用JAVA_HOME，  PATH =D:\jdk\JDK1.6 \bin;D:\jdk\JDK1.6 \jre\bin;