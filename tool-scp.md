```
Author: holdlg
Last updated: 2016-03-07 10:23:04
```

# scp 命令
scp linux 传输文件

## 本地上传到远程服务器
上传文件 <code>scp /localdir/file user@host:/remotedir/ </code>
上传目录 <code>scp -r /localdir user@host:/remotedir/ </code>

## 从远程服务器下载
下载文件 <code>scp user@host:/remotedir/file /localdir/</code>
下载目录 <code>scp -r user@host:/remotedir /localdir/</code>
