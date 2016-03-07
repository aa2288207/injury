title: ArcGIS10.1地图发布
categories:
  - ArcGIS
date: 2013-09-04 10:15:47
tags:
  - ArcGIS
---

<wbr />打开ArcMap，在ArcCatalog中连接ArcGIS Server站点（登录ArcGIS Manager时创建），双击Add ArcGIS Server，弹出Add ArcGIS Server向导：

![](http://pic002.cnblogs.com/images/2012/432820/2012102911283544.png "ArcGIS10.1地图发布")

这里有三种连接方式：

<wbr />  <wbr />  <wbr />　　1\. Use GIS services: 用户身份连接

<wbr />  <wbr />　　 使用此种连接，可以浏览、使用站点内发布的所有服务。但是，不能编辑服务器属性、发布服务、编辑服务属性或者添加、删除、启动、停止或暂停服务。

<wbr />  <wbr />　　 2\. Pulish GIS services: 发布身份连接

<wbr />  <wbr />　　 使用此种连接，可以发布GIS服务,也可以配置和发布草案服务，但是不能编辑站点的任何属性。

<wbr />  <wbr />　　 3\. Administrator GIS services: 管理者身份连接

<wbr />  <wbr />　　使用管理身份连接，可以编辑服务器属性，如configuration store位置、集群配置以及站点中的所有参与机器列表。也可以发布、添加、删除、启动或停止服务。

<wbr />  <wbr />这里我们使用管理者身份连接，选择Administrator GIS services，点击下一步，进入常规向导，在Server URL后面输入[http://localhost:6080/arcgis](http://localhost:6080/arcgis),其中arcgis为安装时的默认实例名。用户名和密码是安装时自己设定的。

<wbr />  <wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911305273.png "ArcGIS10.1地图发布")

在ArcCatalog中定位到地图文档所在的位置，选中之前保存的无标题mxd文档，右键Share As Service…

![](http://pic002.cnblogs.com/images/2012/432820/2012102911314758.png "ArcGIS10.1地图发布")

在弹出的窗口中选择Publish a service:

<wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911324845.png "ArcGIS10.1地图发布")

下一步：在Choose a connection中选择server连接，在Service name中输入服务名:

![](http://pic002.cnblogs.com/images/2012/432820/2012102911334353.png "ArcGIS10.1地图发布")

下一步：默认

<wbr />  <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911343038.png "ArcGIS10.1地图发布")

Continue，弹出服务编辑器，在Capabilities中，设置地图服务功能
<wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911352055.png "ArcGIS10.1地图发布")

分析服务，服务发布之前必须分析。点击Analyse按钮:

![](http://pic002.cnblogs.com/images/2012/432820/2012102911360265.png "ArcGIS10.1地图发布")

发布地图服务，点击Publish,向服务器拷贝数据，然后发布:

![](http://pic002.cnblogs.com/images/2012/432820/2012102911364437.png "ArcGIS10.1地图发布")

点击ok，在ArcCatalog中多了一个MyMapServer服务:

<wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911373282.png "ArcGIS10.1地图发布")

**二、创建缓存**

** <wbr />  <wbr />  <wbr />**在ArcCatalog中，右键单击要创建缓存的地图服务，如下图所示，点击“Service Properties…”：

<wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911392377.png "ArcGIS10.1地图发布")

　　进入地图服务属性页面：选择“Using tiles from a cache”选项卡：

 <wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911403091.png "ArcGIS10.1地图发布")

 <wbr />  <wbr />  <wbr />“Choose the minimum and maximum scales for this tiled map/image service.All levels between the minimum and maximum scale levels will be cached.”的意思是：你可以设置别人访问的最大最小缓存比例尺，最小比例尺：比如你的缓存方案中设置的最小比例尺是1:2000000,但是你想要其他人使用缓存切片的最小比例尺是1：5000000，你就可以在”Levels of Detail”中设置你的最小比例尺缓存为1:5000000。最大比例尺也是类似的道理。<span style="color: #ff0000;">如果使用地图的坐标系则在切片方案中选择建议或地图服务，否则默认的是WGS84</span>

 <wbr />  <wbr />  <wbr />点击Suggest,在”Scale Levels”中输入比例尺个数，点击OK <wbr />

 <wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911412144.png "ArcGIS10.1地图发布")

　　也可以点击”Advanced Settings”，在右边的页面中的文本中输入比例尺，点击“Add”：

 <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911420348.png "ArcGIS10.1地图发布")

　　设置好所有参数后，点击OK：切图过程可以通过右键“View Cache Status”查看：

![](http://pic002.cnblogs.com/images/2012/432820/2012102911431057.png "ArcGIS10.1地图发布")

![](http://pic002.cnblogs.com/images/2012/432820/2012102911434530.png "ArcGIS10.1地图发布")

在Rest目录查看：

<wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911442714.png "ArcGIS10.1地图发布")

**三、删除缓存**

** <wbr />  <wbr />  <wbr /> <wbr />**右键选择要删除缓存的地图服务，如下图所示：

<wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911453110.png "ArcGIS10.1地图发布")

<wbr />

<wbr />  <wbr />  <wbr />  <wbr />选择Delete Cache，删除缓存窗体中会默认输入这个地图服务路径，及切图时的实例数：

![](http://pic002.cnblogs.com/images/2012/432820/2012102911460632.png "ArcGIS10.1地图发布")

<wbr />  <wbr /> <wbr />

点击OK，执行删除。

**四、更新缓存**

<wbr />  <wbr />  <wbr />如下图，给mxd增加一个河流图层，保存

<wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911474666.png "ArcGIS10.1地图发布")

定位到MyMapServer，右键Manage Cache/ManageTiles…

<wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911482370.png "ArcGIS10.1地图发布")

打开“Manage Map Server Cache Tiles”对话框：

<wbr />  <wbr /> <wbr />

![](http://pic002.cnblogs.com/images/2012/432820/2012102911492094.png "ArcGIS10.1地图发布")

<wbr /> <wbr />

点击OK ，在Rest目录中浏览如下：

![](http://pic002.cnblogs.com/images/2012/432820/2012102911531994.png "ArcGIS10.1地图发布")