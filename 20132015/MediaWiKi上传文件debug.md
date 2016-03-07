title: MediaWiKi 上传文件debug
categories:
  - MediaWiKi
date: 2013-12-06 07:34:39
tags:
  - MediaWiKi
---

debug 内容如下：

1. file extension ".zip" does not match the detected MIME type of the file (application/x-rar)
2. A file identical to this file (File:Wiki upload test.zip) has previously been deleted. You should check that file's deletion history before proceeding to re-upload it.
3. The file is a ZIP file that contains a Java .class file. Uploading Java files is not allowed because they can cause security restrictions to be bypassed.

&nbsp;

摘录：

默认情况下是无法上传office相关文件,系统会报两种错误:

该文件是已损坏或以其它方式无法读取的 ZIP 文件。 不能正确检查安全。

The file is a corrupt or otherwise unreadable ZIP file. It cannot be properly checked for security.

文件扩展名“.ppt”与检测到的文件MIME类型（application/zip）不匹配。

File extension ".ppt" does not match the detected MIME type of the file (application/zip)

对于前一个错误,需增加$wgAllowJavaUploads变量并设置为true

对于后一个错误,需打开includes/mime.types文件,找到application/zip行并在后面加上doc docx xls xlsx ppt pptx

&nbsp;

更多参考：[http://www.cnblogs.com/ljzforever/archive/2013/04/27/3047956.html](http://www.cnblogs.com/ljzforever/archive/2013/04/27/3047956.html)

&nbsp;