title: debian sun jdk7 安装配置
categories:
  - Linux
tags:
  - Debian
date: 2013-08-20 11:46:47
---

1.下载 jdk-7u25-linux-x64.tar.gz

wget  http://download.oracle.com/otn-pub/java/jdk/7u25-b15/jdk-7u25-linux-x64.tar.gz?AuthParam=1376970087_4606229645e5d0ce14103a52be54c49d

2.解压jdk-7u25-linux-x64.tar.gz

tar  xzvf  jdk-7u25-linux-x64.tar.gz  -C  /usr/local/

3.环境变量

vim  /etc/profile

文件内容最后追加

# sun jdk1.7.0_25
export JAVA_HOME=/usr/local/jdk1.7.0_25
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH
export CLASSPATH=.$JAVA_HOME/lib:$JAVA_HOME/jre/lib:$CLASSPATH

保存退出

4.刷新生效

source   /etc/profile