title: 'libc6 : Depends: libc-bin (= 2.15-0ubuntu10.4) but 2.15-0ubuntu10.7 is to be installed'
tags:
  - ubuntu
categories:
  - Linux
date: 2014-09-30 07:27:01
---

<table>
<tbody>
<tr>
<td class="votecell">
<div class="vote">正解：</div></td>
<td class="answercell">
<div class="post-text">

运行 :

    sudo dpkg -r libc6

    sudo rm /var/cache/apt/archives/libc6_2.15-0ubuntu10.5_i386.deb
    `</pre>
    上面的命令正常，打开下面文件 :
    <pre>`gksudo gedit /var/lib/dpkg/status

删除libc6相关的整个节点内容：

`Package : libc6`

运行

sudo apt-get -f install

</div></td>
</tr>
</tbody>
</table>
&nbsp;

参考：http://askubuntu.com/questions/488671/libc6-depends-libc-bin-2-15-0ubuntu10-but-2-15-0ubuntu10-5-is-installed