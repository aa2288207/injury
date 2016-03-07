title: jdk 8 安装
categories:
  - Java
tags:
  - Java
date: 2015-12-28 10:43:04
---

# jdk 8 安装

#### 1. 下载
 - url <code>http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-x64.tar.gz</code>
#### 2. 解压
 - 执行<code>tar zxvf ~/download/jdk-8u60-linux-x64.tar.gz -C /opt/java/</code>
#### 3. 配置环境变量
 - 打开文件 <code>vi /etc/profile</code>
 - 最下方添加如下内容：
    ```bash
    export JAVA_HOME=/opt/java/jdk1.8.0_60  
    export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib:$CLASSPATH  
    export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH
    ```
 - 生效<code>source /etc/profile</code>
#### 4. 查看安装结果
 - 执行 <code>java --version</code>
