```
Author: holdlg
Last updated: 2016-02-19 13:06:25
```

# 限制上传文件大小
 - nginx默认上传限制1m
 - 打开配置文件：<code>sudo vim /etc/nginx/conf.d/nginx.conf</code>
 - 修改<code>server</code>段，添加<code>client_max_body_size 20m;</code>,上传限制在20M以内，配置如下：
 
```
server {
listen 80;
server_name 192.168.10.131;
access_log  /var/log/nginx/localhost-flask.log;

location / {
    proxy_pass http://127.0.0.1:8000;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    client_max_body_size 20m;
    error_page 404 /static/errors/404.html;
    error_page 500 502 503 504 /static/errors/50x.html;
}

location /static/ {
    root /home/venus/storage/;
    index index.html;
}
}
```


# 使用外链显示错误页面
```
server
{
    listen  80;
    server_name     www.aa.com;

    location / {
        #直接跳转的www.xx.com的503错误页面（此页面要真实存在）。
        error_page  502 503 504      http://www.xx.com/50x.html;   

        proxy_pass        http://172.17.4.11:6666;
        proxy_redirect off;
        proxy_set_header   Host             $host;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
    }
}
```

# 使用本地文件显示错误页面
```
server
{
    listen  80;
    server_name     www.aa.com;

    location / {
        #直接跳转的www.xx.com的50x错误页面（此页面要真实存在）。
        error_page  502 503 504      /errors/50x.html;   

        proxy_pass        http://172.17.4.11:6666;
        proxy_redirect off;
        proxy_set_header   Host             $host;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
    }

    location /errors/ {
        #/home/www/html/errors/50x.html 需可访问
        root /home/www/html/;
        index.html
    }
}
```

# 404情况
编辑error_page为<code>error_page 404 /errors/404.html;</code> 修改对应位置即可。

# Windows 启动停止脚本
## cmd启动脚本，php有窗口停留
```
@echo off
echo Starting Nginx 1.8.1 for Windows
D:
cd D:\php-5.6.18-Win32-VC11-x64\ && start php-cgi.exe -b 127.0.0.1:9000 -c php.ini
echo php-cgi.exe started.
cd D:\nginx-1.8.1\ && start nginx.exe
echo nginx.exe started.
exit
```

## vbs启动，无窗口停留
```
Set ws = CreateObject("Wscript.Shell") 
ws.run "cmd /c D: && cd D:\php-5.6.18-Win32-VC11-x64\ && php-cgi.exe -b 127.0.0.1:9000 -c php.ini",vbhide 
ws.run "cmd /c D: && cd D:\nginx-1.8.1\ && nginx.exe",vbhide 
ws.run "cmd /c echo php-cgi and nginx started && pause"
```

## cmd停止脚本
```
@echo off
echo Stopping nginx...
taskkill /F /IM nginx.exe > nul
echo Stopping PHP FastCGI...
taskkill /F /IM php-cgi.exe > nul
exit
```