title: windows phone 使用 Sqllite
categories:
  - WP8
date: 2013-09-04 09:25:36
tags:
  - WP8
---

大家知道，在移动端实现数据的离线采集，最重要的一点就是在移动设备上临时存储数据，那么需要移动设备上提供对数据库（不管是本地原生还是第三方）的支持。SQLite是一款轻型的数据库，目前已经在很多嵌入式产品中使用了它，iOS和Android等主流的移动平台也对它提供了支持，关于SQLite数据在此不再赘述，有需要的同学自己谷歌一下。本文主要研究了以下2点：

**1、在Windows Phone上使用SQLite数据库。**

其实SQLite的使用很简单，学过或了解SQL语句的同学都非常容易上手，在这部分我将详细讲述在WP上使用SQLite的详细步骤，包括安装配置和详细代码，供初学者参考。

**2、获取独立存储区中的数据库文件。**

独立存储（IsolatedStorage）是Silverlight一个特色，它是Silverlight的虚拟文件系统，关于虚拟文件系统的概念，大家也可以自己百度，Windows Phone 7是基于Silverlight，它的文件系统也是IsolatedStorage，使用SQLite在WP端存储离线数据时，数据库文件就存放在独立存储区，那么这给我们开发者带来的一个困扰是：我们似乎无法看到模拟器中的数据库文件，不知道每次操作时数据库中发生了怎么样的改变，不利于调试，因此，这部分给大家介绍两种工具，分别用来从真机/模拟器的独立存储中取出数据文件和可视化的操作数据文件。

先看第一部分。

&nbsp;

# <a name="t0"></a>1、在Windows Phone上使用SQLite数据库

## <a name="t1"></a>1）获取SQLite类库

1、从网站下载Sqlite Clientfor Windows Phone 7，截止目前，最新版本为0.6.1，下载地址：[http://sqlitewindowsphone.codeplex.com/](http://sqlitewindowsphone.codeplex.com/)；

2、下载后解压文件夹内容如下：

&nbsp;
> ![](http://my.csdn.net/uploads/201205/24/1337828223_6076.png)
&nbsp;

&nbsp;

3、编译Community.CsharpSqlite.WP程序，获取Community.CsharpSqlite.WP.dll类库文件。

&nbsp;

## <a name="t2"></a>2）在Windows Phone上使用SQLite

&nbsp;

1、新建windows Phone应用程序，目标平台选择wpos 7.1；

2、添加对1）中生成的Community.CsharpSqlite.WP.dll文件的引用；

3、在新建的程序主页面中设计4个按钮，分别用来创建、填充、清除和关闭数据库，如下：
> &nbsp;
> 
> 
> ![](http://my.csdn.net/uploads/201205/24/1337839297_1221.png)
&nbsp;

4、在后台代码中添加SQLite类库的引用：
> <table border="1" cellspacing="0" cellpadding="0">
> 
> <tbody>
> 
> <tr>
> 
> <td valign="top">using System;
> 
> 
> using System.Collections.Generic;
> 
> 
> using System.Linq;
> 
> 
> using System.Net;
> 
> 
> using System.Windows;
> 
> 
> using System.Windows.Controls;
> 
> 
> using System.Windows.Documents;
> 
> 
> using System.Windows.Input;
> 
> 
> using System.Windows.Media;
> 
> 
> using System.Windows.Media.Animation;
> 
> 
> using System.Windows.Shapes;
> 
> 
> using Microsoft.Phone.Controls;
> 
> 
> using SQLiteClient;</td>
> 
> </tr>
> 
> </tbody>
> 
> </table>
&nbsp;

5、添加SQLite数据库连接变量：
> <table border="1" cellspacing="0" cellpadding="0">
> 
> <tbody>
> 
> <tr>
> 
> <td valign="top">namespace SQLiteTest
> 
> 
> {
> 
> 
> public partial class MainPage : PhoneApplicationPage
> 
> 
> {
> 
> 
> SQLiteConnection mySQLiteDB = null;
> 
> 
> &nbsp;
> 
> 
> // 构造函数
> 
> 
> public MainPage()
> 
> 
> {
> 
> 
> InitializeComponent();
> 
> 
> }
> 
> 
> }
> 
> 
> }</td>
> 
> </tr>
> 
> </tbody>
> 
> </table>
> 
> &nbsp;
6、给“Open”按钮添加事件，创建并打开数据库：
> <table border="1" cellspacing="0" cellpadding="0">
> 
> <tbody>
> 
> <tr>
> 
> <td valign="top">
> 
> 
> private void btnOpen_Click(object sender, RoutedEventArgs e)
> 
>         {
> 
>             if (mySQLiteDB == null)
> 
>             {
> 
>                 mySQLiteDB = new SQLiteConnection("TestSQLiteDB");
> 
>                 mySQLiteDB.Open();
> 
>                 btnOpen.IsEnabled = false;
> 
>                 btnClose.IsEnabled = true;
> 
>                 btnClear.IsEnabled = false;
> 
>                 btnPopulate.IsEnabled = true;
> 
>             }
> 
>         }
> 
> </td>
> 
> </tr>
> 
> </tbody>
> 
> </table>
&nbsp;

7、接下来，需要创建表，并往表中填充数据，使用SQLiteCommand对象实现：
> <table border="1" cellspacing="0" cellpadding="0">
> 
> <tbody>
> 
> <tr>
> 
> <td valign="top">
> 
> 
> private void btnPopulate_Click(object sender, RoutedEventArgs e)
> 
>         {
> 
>             //创建表RegisteredStudents，有3个属性：id、姓名、学号
> 
>             SQLiteCommand cmd = mySQLiteDB.CreateCommand("Create table RegisteredStudents (id int primary key,name text,zipcode numeric(7))");
> 
>             int i = cmd.ExecuteNonQuery();
> 
>             int id = 0;
> 
>             string name = "Name" + id;
> 
>             int zipcode = 98000;
> 
>             for (int j = 0; j &lt; 10; j++)
> 
>             {
> 
>                 id++;
> 
>                 name = "Name" + id;
> 
>                 zipcode = 98000 + id;
> 
>                 cmd.CommandText = " Insert into RegisteredStudents (id, name, zipcode) values (" + id +",\"" + name +"\"," + zipcode +")";
> 
>                 i = cmd.ExecuteNonQuery();
> 
>             }
> 
>             btnPopulate.IsEnabled = false;
> 
>             btnClear.IsEnabled = true;
> 
>         }
> 
> </td>
> 
> </tr>
> 
> </tbody>
> 
> </table>
&nbsp;

8、清空表中的数据，同样使用SQLiteCommand对象，代码如下：
> <table border="1" cellspacing="0" cellpadding="0">
> 
> <tbody>
> 
> <tr>
> 
> <td valign="top">
> 
> > private void btnClear_Click(object sender, RoutedEventArgs e)
> > 
> >         {
> > 
> >             SQLiteCommand cmd = mySQLiteDB.CreateCommand("drop table RegisteredStudents");
> > 
> >             int i = cmd.ExecuteNonQuery();
> > 
> >             btnPopulate.IsEnabled = true;
> > 
> >             btnClear.IsEnabled = false;
> > 
> >         }
> > 
> > &nbsp;
> 
> </td>
> 
> </tr>
> 
> </tbody>
> 
> </table>
> 
> &nbsp;
9、断开数据库连接，关闭数据库，如下:
> <table border="1" cellspacing="0" cellpadding="0">
> 
> <tbody>
> 
> <tr>
> 
> <td valign="top">
> 
> 
> private void btnClose_Click(object sender, RoutedEventArgs e)
> 
>         {
> 
>             if (mySQLiteDB != null)
> 
>             {
> 
>                 mySQLiteDB.Dispose();
> 
>                 mySQLiteDB = null;
> 
>                 btnOpen.IsEnabled = true;
> 
>                 btnPopulate.IsEnabled = false;
> 
>                 btnClear.IsEnabled = false;
> 
>                 btnClose.IsEnabled = false;
> 
>             }
> 
>         }
> 
> </td>
> 
> </tr>
> 
> </tbody>
> 
> </table>
&nbsp;

运行程序，点击open可以在WP的模拟器的独立存储空间中创建名为“TestSQLiteDB”数据库，点击populate按钮可以为其填充数据，点击clear可以清空数据库中的数据，close关闭数据库连接。但是所有这些执行成功的操作在数据库中引起了怎样的变化，我们不得而知，所以接下来我们进入到第二步，如何取到模拟器中的数据库文件。

&nbsp;

# <a name="t3"></a>2、获取和操作独立存储区中的数据库文件

## <a name="t4"></a>1）获取数据库文件

&nbsp;

Windows Phone Power Tools工具可以直接连接模拟器/真机，读取独立存储空间中的数据（[参考文章](http://www.cnblogs.com/vistach/archive/2012/02/23/Windows_Phone_WP7_LINQ_Database_DB_View_SQL_Server_CompactPowerTools_IsolatedStorage.html)）。[下载](http://wptools.codeplex.com/)该工具，具体使用方法很简单，如下图：
> ![](http://my.csdn.net/uploads/201205/24/1337838788_6959.png)
&nbsp;

选择真机或模拟器连接
> ![](http://my.csdn.net/uploads/201205/24/1337838844_1855.png)
&nbsp;

连接成功后，在File Browser中可以看到，已经取到了该应用程序的独立存储区以及其中的数据库文件，点击“get”，将该数据文件存储到本地：
> ![](http://my.csdn.net/uploads/201205/24/1337838912_3152.png)
&nbsp;

## <a name="t5"></a>2）可视化操作数据库文件

&nbsp;

通过Windows Phone PowerTools将数据库文件导出到电脑中，这个时候我们可以依靠另一种非常好用的可视化工具“SQLite-Manager”来操作和管理数据库文件了。SQLite-Manager帮助我们管理和创建与数据库相关的东西，如database、tables、views等，SQLite-Manager是一个插件，可以在火狐浏览器中安装：
> ![](http://my.csdn.net/uploads/201205/24/1337838966_9320.png)
&nbsp;

安装好后，在火狐的浏览器菜单中启动SQLite Manager：
> ![](http://my.csdn.net/uploads/201205/24/1337839004_5250.png)
&nbsp;

接下来，我们就可以非常方便的可视化的操作数据库了：
> ![](http://my.csdn.net/uploads/201205/24/1337839080_9239.png)
&nbsp;
> ![](http://my.csdn.net/uploads/201205/24/1337839089_7877.png)