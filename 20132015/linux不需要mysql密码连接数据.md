title: linux不需要mysql密码连接数据
categories:
  - MySQL
date: 2013-10-10 15:19:07
tags:
  - MySQL
---

redhat:

1. # service mysql stop

2. # service mysql start  --skip-grant-tables

3. # mysql -u root -p    (Enter 密码为空)

至此已连接上mysql. 推荐你修改密码重新登录，如下继续： (当然你可以创建新用户，具体请自行Google)

4. # update mysql.user set password = PASSWORD("你的密码") where user='root'

5. # exit

6. # service mysql restart

7. #  mysql -u root -p   (Enter 输入你的密码)