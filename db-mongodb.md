title: mongodb 安装
categories:
  - MongoDB
tags:
  - MongoDB
date: 2015-12-28 10:41:04
---

# mongodb 远程访问
 - 修改<code>/etc/mongodb.conf</code> 文件
 - 将<code>bind_ip = 127.0.0.1</code>修改为<code>bind_ip = 0.0.0.0</code>

# mongodb 安装

## 1.添加许可
```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```

## 2.写入安装列表
```bash
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
```

## 3.更新源
```bash
sudo apt-get update
```

## 4.在线安装
```bash
sudo apt-get install -y mongodb-org
```

## 5.启动，停止，重启
```bash
sudo service mongod start
sudo service mongod stop
sudo service mongod restart
```

## 6.卸载mongodb，删除目录
```bash
sudo apt-get purge mongodb-org*
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```
