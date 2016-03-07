title: wp入门开发
categories:
  - WP8
date: 2013-06-04 17:04:08
tags:
  - WP8
---

**一、设置地图初始化视野**
<pre>
注:如果利用XAML设置视野会给ExtentChanged事件造成死循环，建议后台设置
 <!--Extent标签用来初始地图的范围，通过设置4格数值指定min x,min y,max x,max y相当于于BingMap for Silverlight中的2个Location点Location(60,60) 和另一点Location(13,140)来初始化地图为中国地图
<esri:Map.Extent>
<esriGeometry:Envelope XMin="661140" YMin="-1420246" XMax="3015668" YMax="1594451" >
<esriGeometry:Envelope.SpatialReference>
<esriGeometry:SpatialReference WKID="26777"/>
</esriGeometry:Envelope.SpatialReference>
</esriGeometry:Envelope>
</esri:Map.Extent></pre>
**二、模拟定位，以及视野以当前位置画圆**
<pre>MapPoint mapPoint=new MapPoint(116.3880556,39.907325)北京天安门坐标
private void MyMap_ExtentChange(object sender,ExtentEventArcgs e)
{
this.MyMap.Panto(mapPoint)
}</pre>
使用GraphicsLayer从后台中获得当前的位置，然后构造一个Point类型的Graphic 并设置点的符号， 添加到GraphicsLayer中，这里需要事先定义GeoCoordinateWatcher，并注册位置变化事件。在位置变化事件里不断的获得位置
GeoCoordinateWatcher只能获得WGS 84坐标系下的经纬度，我们可以根据底图的参考系来进行转换，如果底图本来就是WGS84坐标系的话，就不需要转换了，如果是webmercator空间坐标系的话，可以使用WebMercator来完成地理坐标与空间坐标的转换，如果是其他的坐标系的话，应当使用几何服务。
<pre>void watcher_PositionChanged(object sender, GeoPositionChangedEventArgs e)
{
ESRI.ArcGIS.Client.Projection.WebMercator mercator = new ESRI.ArcGIS.Client.Projection.WebMercator();
_graphicLocation.Geometry = mercator.FromGeographic(new MapPoint(e.Position.Location.Longitude, e.Position.Location.Latitude));
}</pre>
**三、使用StackPanel中动态添加控件**
由于StackPanel添加控件挤一块不美观，所以可采用Margin调整距离
提供对象的边距值。 默认值是所有属性（维度）都等于 0 的默认 Thickness。
XAML 值
<pre><frameworkElement Margin="uniform"/>
- or -
<frameworkElement Margin="left+right,top+bottom"/>
- or -
<frameworkElement Margin="left,top,right,bottom"/>
uniform
一个以像素为单位度量的值，用于指定统一的 Thickness。 uniform 值应用于全部四个 Thickness 属性（Left、Top、Right、Bottom）。
left+right
一个以像素为单位度量的值，用于指定对称 Thickness 的 Left 和 Right。
top+bottom
一个以像素为单位度量的值，用于指定对称 Thickness 的 Top 和 Bottom。
left top right bottom
以像素为单位度量的值，用于指定 Thickness 结构的四个可能的维度属性（Left、Top、Right、Bottom）。</pre>
**四、控件Button按钮如果变成圆角**
<pre>1、利用Blend进行设计
2、选中按钮，右键编辑模板——新建空模板——选中Grid——右键更改模板样式——选中border——如果需要显示按钮上面的文字，则里面需要放一个leabel控件，如果设置图片直接背景设置——更改CornerRadius（设置值：15）可以设置成圆角，选中状态——pressed（点击时）向右下角偏移——设置Projection中的x（5），y（5）然后即可。</pre>
**五、ArcGIS API for Silverlight 地图加载进度条类之MapProgressBar**
<pre>注意调整BorderBrush、Background、BorderThickness、TextBrush属性，即可美化一下进度条，如果需要做的更好，需要熟练使用Blend的美工进行调整。</pre>
**六、使屏幕上的元素不占位又不可见**
<pre>属性Opacity用于控制对应控件的透明程度。当设置为1时，控件可见度最好；当设置为0时，控件完全不可见。
如果你想要隐藏某个元素，但你还是希望它有一个非零的版面大小，那么请不要使用Visibility属性，而应用使用类似于下面的操作。
属性Visibility有两个取值，一个是Visible，另一个是Collapsed。而相比之下，取值Collapsed的结果是导致元素的大小为零，从而使之不再占用屏幕布局
但是，上面的代码在Windows Phone 7 Silverlight应用程序中导致的结果是，控件TextBlock仍然会占用触摸输入。因此，如果你既不想使之占用屏幕空间，也不想使之占用触摸输入，那么你可以使用如下的代码方案：
最后值得注意的是，属性Opacity和Visibility对于子控件也有影响。例如，你设置一个Panel控件的上述两个属性，那么其内部包含的子控件也都受到同样的影响。
Visibility的使用
控件.Visibility=Visibility.visible或者控件.Visibility=Visibility.Collapsed</pre>
**七、地图加载的进度条**
<pre>利用了Map控件内置的一个Progress事件。
<!--progressbar 放在LayoutRoot中-->
<Grid HorizontalAlignment="Center" x:Name="progressGrid" VerticalAlignment="Center" Width="200" Height="20" Margin="5,5,5,5">
<ProgressBar x:Name="MyProgressBar" Minimum="0" Maximum="100" />
<TextBlock x:Name="ProgressValueTextBlock" Text="100%" HorizontalAlignment="Center" VerticalAlignment="Center" />
</Grid></pre>
在esri:Map标签中加入一个事件：Progress="Map1_Progress"
<pre>private void Map1_Progress(object sender, ESRI.ArcGIS.ProgressEventArgs e)
{
if (e.Progress < 100)
{
progressGrid.Visibility = Visibility.Visible;
MyProgressBar.Value = e.Progress;
ProgressValueTextBlock.Text = String.Format("正在处理 {0}%", e.Progress);
}
 else 
{
 progressGrid.Visibility = Visibility.Collapsed; 
} 
}</pre>
**八、后台代码中创建和使用ImageBtesh**
<pre>ImageBrush brush=new ImageBrush（）；
brush.ImageSource=new BitmapImage(new Uri("wrox.png",UriKind.Relative));
brush.Stresh=Stretch.FIll;
MainRect.Fill=brush;</pre>
**九、地图初始化视野**
<pre>如果想获得地图的默认的初始范围，我们应该在它第一次加载的时候来获取，在地图的范围变化，我们可以在ExtentChanging 和 ExtentChanged 两个事件里来获取地图地图变化前后的范围值。在地图移动或者缩放的时候会触发这两个事件，获取初始范围的代码如下
void MyMap_ExtentChanged(object sender, ExtentEventArgs e)
{ 
if (e.OldExtent == null)
ESRI.ArcGIS.Client.Geometry.Envelope initialExtent = e.NewExtent;
}
我们在平移或者缩放过程中，地图会有一个过渡动画，我们可以控制动画的时间，默认的情况下缩放的持续时间是1.5秒，平移动画的持续时间是0.75秒，通过设置Map 的PanDuration以及ZoomDuration可以设置，以下是取消动画的操作</pre>
**十、textblock.TextWrapping 属性**
<pre>   TextBlock默认是不自动换行的，如果想TextBlock换行，可以设定属性TextWrapping="Wrap"。
   TextBox 固定了长度 肯定字符串过长 就无法全部显示出来</pre>
**十一、地图单位计算**
<pre>在不同的坐标系之间，不同单位之间，转换地图单位      
 /// 
/// 长度(米)转换经纬度差
///
 public static double convertedBufferDistanceToJWD(double bufferDistance)
 { 
  IUnitConverter unitConverter = new UnitConverterClass(); 
  double convertedBufferDistance = unitConverter.ConvertUnits(buff  erDistance, 
  esriUnits.esriMeters, esriUnits.esriDecimalDegrees); 
  return convertedBufferDistance; 
}
   ///
  ///经纬度差转换长度(米) 
  ///
 public static double convertedBufferDistanceToMeter(double bufferDistance) 
{ 
IUnitConverter unitConverter = new UnitConverterClass(); 
double convertedBufferDistance = unitConverter.ConvertUnits(bufferDistance,
 esriUnits.esriDecimalDegrees, esriUnits.esriMeters); return convertedBufferDistance; 
}
 以上以单位米和经纬度作为对比</pre>
**十二、Application Bar（菜单系统）**
<pre>创建新项目，下面有注释，把注释去掉都可以显示了
可以采用系统提供的图标，路径为：c:\Program Files\Microsoft SDKs\Windows Phone\V7.0\Icons
App Bar：图片规格是48×48像素，背景透明，Bar里面的图标控制在26×26像素，格式是png格式，如果大于的
话则超出Bar的区域，图片属性设置为content
![Application <wbr>Bar（菜单系统）](http://s15.sinaimg.cn/middle/69089285gcb9d8882fcee&amp;690)
下面三个五角星和记事本标志的是Application Bar也就是菜单系统，包含：定义带图标按钮（ApplicationBarIconButton）
和展开菜单项的显示(不带图标，MenuItem)，建议不要出现返回按钮，最重要最常用的功能放到ApplicationBarIconButton中
一、ApplicationBarIconButton（菜单系统按钮）
1、最多放4个按钮，再多会有异常（ApplicationBarIconButton）
2、属性Opacity（透明度），默认为1（完全不透明），透明是0，半透明是0.5，微软建议三个值（1、0.5、0）
二、右边小小白点，点击小白点下面有详情显示，下面的详情内容不带图片（MenuItem）
1、MenuItem最多不超过5个，如果超过5个会有滚动条，对客户不友好
2、MenuItems的内容长度不要超过屏幕宽度，超过会被屏幕截断
前台代码：
<phone:PhoneApplicationPage.ApplicationBar>
<<wbr /> <wbr /> <wbr /> <wbr /> !--带图标按钮-->
<wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBar IsVisible="True" IsMenuEnabled="True">
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBarIconButton<wbr /> IconUri="/Image/appbar.minus.rest.png" Text="缩小"></shell:ApplicationBarIconButton<wbr />>
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBarIconButton<wbr /> IconUri="/Image/appbar.new.rest.png" Text="放大"></shell:ApplicationBarIconButton<wbr />>
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBarIconButton<wbr /> IconUri="/Images/appbar.save.rest.png" Text="平移"></shell:ApplicationBarIconButton<wbr />>
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <!--展开菜单项下面的显示，不带图标的显示-->
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBar.MenuItems>
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBarMenuItem  <wbr />Text="保存"></shell:ApplicationBarMenuItem>
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> <shell:ApplicationBarMenuItem Text="保存"></shell:ApplicationBarMenuItem>
<wbr />  <wbr />  <wbr />  <wbr />  <wbr />  <wbr /> </shell:ApplicationBar.MenuItems>
<wbr />  <wbr />  <wbr />  <wbr /> </shell:ApplicationBar>
<wbr />  <wbr /> </phone:PhoneApplicationPage.ApplicationBar>
后台代码：
动态加入ApplicationBarIconButton： ApplicationBarIconButton iconButton=new ApplicationBarIconButton（）； iconButton.IconUri=new Uri("/Images/appbar.save.rest.png",UriKind.Relative); iconButton.Text=""; this.AplicationBar.Buttons.Add(iconButton); iconButton.Click+=new EventElandr(iconButton_click); void iconButton_Click(object sender,EnentArgs e) { } 隐藏按钮：(this.ApplicationBar.Buttons[隐藏的索引] as ApplicationBarIconButton).IsEnabled=false,显示为true</pre>
**十二、以下是取消地图动画的操作**
我们在平移或者缩放过程中，地图会有一个过渡动画，我们可以控制动画的时间，默认的情况下缩放的持续时间是1.5秒，平移动画的持续时间是0.75秒，通过设置Map 的PanDuration以及ZoomDuration可以设置，以下是取消动画的操作

<esri:Map x:Name="MyMap" ZoomDuration="00:00:00" PanDuration ="00:00:00">

</esri:Map>

&nbsp;

&nbsp;