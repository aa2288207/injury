title: 'dpkg 被中断,您必须手工运行 sudo dpkg --configure -a解决此问'
categories:
  - Linux
tags:
  - Debian
date: 2013-08-19 10:58:10

---

debian代码:

su rm /var/lib/dpkg/updates/*

su apt-get update

su apt-get upgrade

&nbsp;

以此执行如上代码。