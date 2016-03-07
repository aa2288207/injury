title: tar.xz压缩和解压
categories:
  - tar
tags:
  - tar
date: 2014-09-19 06:14:28
---

# 解压 xz 格式文件

## 方法一：
需要用到两步命令，首先利用 xz-utils 的 xz 命令将 linux-3.12.tar.xz 解压为 linux-3.12.tar，其次用 tar 命令将 linux-3.12.tar 完全解压。
```
xz -d linux-3.12.tar.xz
tar -xf linux-3.12.tar
```

## 方法二（推荐）
```
tar -Jxf linux-3.12.tar.xz
```

# 创建 xz 格式文件

## 方法一：
也是用到两步命令，首先利用 tar 命令将 linux-3.12 文件夹打包成 linux-3.12.tar，其次用 xz-utils 的 xz 命令将 linux-3.12.tar 压缩成 linux-3.12.tar.xz。
```
tar -cf linux-3.12.tar linux-3.12
xz -z linux-3.12.tar
```

## 方法二（推荐）
```
tar -Jcf linux-3.12.tar.xz linux-3.12
```

认识tar.xz格式文件是在Linux内核的[官方网站](https://www.kernel.org/)上，比如最新的[Linux内核3.12](https://www.kernel.org/pub/linux/kernel/v3.x/linux-3.12.tar.xz)，就是.xz后缀的文件。
根据维基百科的[解释](http://zh.wikipedia.org/wiki/Xz)， xz 是一个使用 LZMA压缩算法的无损数据压缩文件格式。和gzip与bzip2一样，同样支持多文件压缩，但是约定不能将多于一个的目标文件压缩进同一个档案文件。相反，xz通常作为一种归档文件自身的压缩格式，例如使用tar或cpioUnix程序创建的归档。xz 在GNU coreutils（版本 7.1 或更新）中被使用。xz 作为压缩软件包被收录在 Fedora (自Fedora 12起), Arch Linux, FreeBSD、 Slackware Linux、CRUX 和 Funtoo中。

由于 xz 文件格式的压缩率更高，已在 Linux 各发行版中广泛使用。最典型的就是Linux内核，3.12版本的xz压缩包仅72.85MB，解压后能达到518.77MB。

# 参考链接：
XZ Utils的官方网站为：[http://tukaani.org/xz/](http://tukaani.org/xz/)
wiki: [http://zh.wikipedia.org/wiki/Xz](http://zh.wikipedia.org/wiki/Xz)