title: Paas云空间 appfog 查看php空间的MySQL配置信息
categories:
  - PaaS
date: 2013-11-15 10:16:44
tags:
  - appfog
---

如下代码，保存为 *.php 文件上传至空间，访问*.php也没即可看到。
```
<html>  
 <head>  
     <title>获得数据库信息</title>  
 </head>  
 <body>  
 <?php  
      $services_json = json_decode(getenv("VCAP_SERVICES"),true);   //进行获得数据库信息的json文件解析  
      $mysql_config = $services_json["mysql-5.1"][0]["credentials"];  
      $name = $mysql_config["name"];  
      $hostname = $mysql_config["hostname"];  
	  $host = $mysql_config["host"];  
	  $port = $mysql_config["port"];  
	  $user = $mysql_config["user"]; 
	  $username = $mysql_config["username"]; 
	  $password = $mysql_config["password"];
 ?>  
       <div  align ="center">  

<label>数据库名称：</label><?php echo $name;?>

<label>数据库主机名称：</label><?php echo $hostname;?>

<label>数据库主机IP：</label><?php echo $host;?>

<label>端口号：</label><?php echo $port;?>

<label>用户名：</label><?php echo $user;?>

<label>数据库用户名：</label><?php echo $username;?>

<label>数据库密码：</label><?php echo $password;?>

       </div>  

 </body>  
</html> 
```

appfog官方文档：https://docs.appfog.com/services/mysql

大多Paas空间都是用 全局变量，获取信息。如上可参考