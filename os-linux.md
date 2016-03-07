```
Author: holdlg
Last updated: 2016-03-07 10:23:04
```

# 安装
  中文字体 <code>sudo apt-get install ttf-wqy-*</code>
  安装ibus-googlepinyin <code>sudo apt-get install ibus-googlepinyin</code>
  安装vim <code>sudo apt-get install vim</code>
  安装svn <code>sudo apt-get install subversion</code>
  安装ssh <code>sudo apt-get install ssh</code>
  安装git <code>sudo apt-get install git</code>
  安装MySQL5.6 <code>sudo apt-get install mysql-server-5.6</code>

# ubuntu启用root登录

1.设置密码<code>sudo passwd root</code>
2.配置root登录
  创建并编辑<code>vim /etc/lightdm/lightdm.conf</code>文件。
  写入以下内容。
  ```
      [SeatDefaults]
      # 启动后以root身份自动登录
      autologin-user=root
      greeter-session=unity-greeter
      user-session=ubuntu

      # 手工输入登陆系统的用户名和密码
      greeter-show-manual-login=true

      # 禁用guest用户
      allow-guest=false
  ```
3.保存退出，注销,以root用户登录。


# ubuntu长期支持
1. ubuntu多版本长期支持网站：

   [http://old-releases.ubuntu.com/ubuntu/](http://old-releases.ubuntu.com/ubuntu/)

2. 更多ubuntu版本的源可以在网易镜像源下载：

   [http://mirrors.163.com/.help/ubuntu.html](http://mirrors.163.com/.help/ubuntu.html)

3. 使用old-releases.ubuntu.com替换掉mirrors.163.com即可。


# Linux RWX权限说明
```
r(Read,读取)：对文件，具有读取文件内容的权限；
              对目录，具有浏览目录的权限。
w(Write,写入)：对文件，具有新增,修改,删除文件内容的权限；
               对目录，具有新建，删除，修改，移动目录内文件的权限。
x(Execute,执行)：对文件，具有执行文件的权限；
                 对目录，该用户具有进入目录的权限。
```