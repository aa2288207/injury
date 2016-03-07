title: debian 目录
categories:
  - Linux
tags:
  - Debian
date: 2013-08-20 11:01:16
---

```
debian的目录结构，所谓linux一切都基于文件的，有必要先了解下目录结构：

/boot           放置linux核心与开机相关文件的地方
                    这个目录下的vmlinuz-xxx就是linux的kernel喽，grub就是从这里加载kernel的

/bin             放置:ls,mv,rm,mkdir,rmdir,gzip,tar,telnet,等等命令的地方

/dev              放置设备有关的文件。linux系统均把设备当成文件来看待
                    例如/dev/sda1代表硬盘；/dev/cdrom代表光盘；

/etc             系统在开机过程中需要读取的档案均在这个目录中
                    例如:用户配置文件：/etc/passwd；网络配置文件：/etc/network/interface等

/home         系统预设的使用者的家目录；（在/etc/passwd里配置）

/lib              在linux执行或者编译一些程序的时候，均会使用到一些函数库(library)；

/proc          系统核心和执行程序的一些信息
                    这个目录在系统启动时自动挂在上，里边的数据都是来自内存，不会占用磁盘空间

/sbin          放置一些系统管理常用的程序；如：fdisk,mke2fs,mount等；

/usr            里边放置程序和指令；例示windows的programfiles 目录。

/usr/bin     放置可执行程序；

/usr/sbin   放置管理之使用的程序；和/sbin例示

/var            存放所有服务的登录文件和错误信息文件（log file)都在/var/log里。
```