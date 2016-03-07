title: Buildout 和 Virtualenv
tags:
  - Buildout
  - Virtualenv
categories:
  - Python
date: 2014-06-13 10:22:51
---

buildout 和 virtualenv   个人推荐buildout  一个顶2个。不过vitualenv + pip 貌似比较普及。

&nbsp;

安装pip:

下载： [https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py "pip")

python  get-pip

&nbsp;

安装Buildout：

pip install zc.buildout

<span style="color: #444444;">buildout  init</span>

配置 <span style="color: #444444;">buildout.cfg  参见：[http://holdlg.coding.io/?p=1253](http://holdlg.coding.io/?p=1253)</span>

&nbsp;

&nbsp;

安装 virtualenv

pip install virtualenv

virtualenv  dome-env          创建虚拟环境

激活：

linux 用 source  demo-env/bin/activate

win用 demo-env\Script\activate.bat

配置<span style="color: #000000;">requirement.txt  可以通过  pip  freeze  查看，然后保存结果即为当前的配置。</span>

其他地方使用<span style="color: #000000;">requirement.txt    pip install -r requirement.txt</span>

&nbsp;

本文仅供参考。

&nbsp;