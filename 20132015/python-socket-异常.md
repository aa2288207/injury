title: python socket 异常
tags:
  - socket
categories:
  - Python
date: 2014-07-10 07:24:05
---

try:
print 'receive from %r' % str(self.client_address) # data source
data_xml = self.request.recv(config.get_BUF_SIZE()) # receive
xml += data_xml
except socket.error, e:
err = e.args[0]
print errno.EWOULDBLOCK
print e
print err
print socket.errno
print socket.error
break
except:
print 'XTXT=='*23
traceback.print_exc()
break

&nbsp;

有关 socket.recv() 函数字节的error 10035 问题：

参考：http://stackoverflow.com/questions/16745409/what-does-pythons-socket-recv-return-for-non-blocking-sockets-if-no-data-is-r

https://docs.python.org/2/library/socket.html

https://docs.python.org/2/library/errno.html#module-errno