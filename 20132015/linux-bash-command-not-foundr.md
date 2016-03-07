title: 'Linux:-bash: ***: command not foundr'
tags:
  - Linux
categories:
  - Linux
date: 2014-01-17 03:00:42
---

确保安装正确，没有遇到异常错误。

解决方法 (推荐1)

1. 软连接   ln -s  /usr/local/projectname /bin/project_exec_file

路径按照自己的目录，软连到/usr/bin 一般这个目录是 linux 默认的可执行文件路径。

2.修改Path,   vim /etc/profile   添加  export PATH=$PATH:/usr/local/projectname/bin/project_exec_file

还有其他修改方法。自行google哈。