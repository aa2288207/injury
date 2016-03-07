title: bind-dlz MySQL支持 naptr 记录
tags:
  - bind
categories:
  - Linux
date: 2014-10-16 08:39:02
---

bind-dlz 的官网文档没有说明 naptr记录的解析实现，查询和研究了一下，实现配置如下。

./etc/named.conf 配置

dlz "Mysql zone" {
database "mysql
{host=127.0.0.1 dbname=dns ssl=false port=3306 user=root}
{select zone from dns_records where zone = '%zone%' limit 1}
{select ttl, type, mx_priority,
case
when lower(type) = 'txt' then concat('\"', data, '\"')
when lower(type) = 'soa' then concat_ws(' ', data, resp_person, serial, refresh, retry, expire, minimum)
when lower(type) = 'naptr' then <span style="color: #ff0000;">concat(' ', naptr_order, ' ', naptr_preference, ' \"', naptr_flags, '\"', ' \"', naptr_service, '\"', ' \"', naptr_regexp,'\" ', data, '.')</span>
else data
end
from dns_records where zone = '%zone%' and host = '%record%'}";
};

<span style="color: #008000;">(注：'%zone%' 是bind9.6的写法。   '$zone$'是bind9.10的写法。自行斟酌 )</span>

&nbsp;

建dns库和dns_records 表：

CREATE DATABASE `dns` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

create table dns_records (
`id` int(10) unsigned NOT NULL AUTO_INCREMENT,
zone varchar (255),
host varchar (255),
type varchar (255),
data varchar (255),
ttl int(11),
mx_priority varchar (255),
refresh int(11),
retry int(11),
expire int(11),
minimum int(11),
serial bigint(20),
resp_person varchar (255),
primary_ns varchar (255),
<span style="color: #ff0000;">naptr_order int(11),</span>
<span style="color: #ff0000;"> naptr_preference int(11),</span>
<span style="color: #ff0000;"> naptr_flags varchar (255),</span>
<span style="color: #ff0000;"> naptr_service varchar (255),</span>
<span style="color: #ff0000;"> naptr_regexp varchar (255),</span>
PRIMARY KEY (`id`)
);

测试sql：

insert INTO dns_records (zone,host,type,data,ttl,retry,naptr_order,naptr_preference,naptr_flags,naptr_service,naptr_regexp)
values ('test.cn','69101','NAPTR','www.qq4.com',15,20,0,0,'u','RNS','');

&nbsp;

测试命令和结果：

[ops@Echo named]$ dig @localhost -p 19953 69101.test.cn naptr

; &lt;&lt;&gt;&gt; DiG 9.6-ESV-R5 &lt;&lt;&gt;&gt; @localhost -p 19953 69101.test.cn naptr
; (1 server found)
;; global options: +cmd
;; Got answer:
;; -&gt;&gt;HEADER&lt;&lt;- opcode: QUERY, status: NOERROR, id: 14559
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;69101.test.cn. IN NAPTR

;; ANSWER SECTION:
69101.test.cn. 15 IN NAPTR 0 0 "u" "RNS" "" www.qq4.com.

;; Query time: 1 msec
;; SERVER: 127.0.0.1#19953(127.0.0.1)
;; WHEN: Thu Oct 16 16:12:59 2014
;; MSG SIZE rcvd: 67

&nbsp;

参考文章：

[http://permalink.gmane.org/gmane.network.dns.bind9.dlz/1361](http://permalink.gmane.org/gmane.network.dns.bind9.dlz/1361)

[http://tools.ietf.org/html/rfc2915](http://tools.ietf.org/html/rfc2915)

[http://bind-dlz.sourceforge.net/mysql_driver.html](http://bind-dlz.sourceforge.net/mysql_driver.html)