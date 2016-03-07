title: 'could not listen on UDP socket: permission denied'
tags:
  - bind
categories:
  - Linux
date: 2014-10-16 05:31:19
---

安装bind9提示 could not listen on UDP socket: permission denied

也提示：couldn't add command channel 127.0.0.1#953: permission denied

我用的是 非root用户，非root 用户不能使用 1024一下 端口。修改使用端口均大于1024即可。

如：

启动项：/home/ops/bind/named/sbin/named -gc /home/ops/bind/named/etc/named.conf 

./etc/named.conf 文件的

```
controls {
    inet 127.0.0.1 port 9953
    allow { 127.0.0.1; } keys { "rndc-key"; };
};
```