```
Author: holdlg
Last updated: 2016-03-23 15:23:04
```

# ubuntu14 gulp bug
- 异常：Error: watch xxxxx/xxxx ENOSPC
- 解决方法执行
```
echo fs.inotify.max_user_watches=582222 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```