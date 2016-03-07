title: InfoWindow 控件实现通过指定点显示相应信息
categories:
  - WP8
date: 2013-05-29 11:28:39
tags:
  - WP8
---

# 前台UI：
```
<!--LayoutRoot 是包含所有页面内容的根网格-->
<Grid x:Name="LayoutRoot" Background="Transparent">
<Grid.Resources>
<esri:SimpleRenderer x:Key="MySimpleRenderer">
<esri:SimpleRenderer.Symbol>
<esriSymbols:SimpleFillSymbol Fill="#01FFFFFF" BorderBrush="#88000000" BorderThickness="2"></esriSymbols:SimpleFillSymbol>
</esri:SimpleRenderer.Symbol>
</esri:SimpleRenderer>
<DataTemplate x:Key="LocationInfoWindowTemplate">
<StackPanel >
<!-- <TextBlock Text="Location:" Foreground="Black" />-->
<TextBlock Text="{Binding X, StringFormat=X\=\{0:0.000\}}" Foreground="Black" />
<TextBlock Text="{Binding Y, StringFormat=Y\=\{0:0.000\}}" Foreground="Black"/>
</StackPanel>
</DataTemplate>

<DataTemplate x:Key="MyFeatureLayerInfoWindowTemplate">
<TextBlock Text="{Binding [shape_area]}" Foreground="Black" FontSize="14" />
</DataTemplate>
</Grid.Resources>
<esri:Map x:Name="map1" WrapAround="True" IsLogoVisible="False" MapGesture="map1_MapGesture" >
<esri:GraphicsLayer ID="graphicesLayer" Renderer="{StaticResource MySimpleRenderer}"/>
</esri:Map>
<esriToolkit:ScaleLine HorizontalAlignment="Left" VerticalAlignment="Bottom"/>
<esriToolkit:InfoWindow x:Name="MyInfoWindow"
Padding="2"
CornerRadius="20"
Background="LightSalmon"
Map="{Binding ElementName=map1}"
ContentTemplate="{StaticResource MyFeatureLayerInfoWindowTemplate}"
/>
<esriToolkit:InfoWindow x:Name="InfoWindow"
CornerRadius="15"
Background="White"
BorderBrush="Gray"
BorderThickness="1"
Map="{Binding ElementName=map1}"
ContentTemplate="{StaticResource LocationInfoWindowTemplate}"
/>
</Grid>
</phone:PhoneApplicationPage>
```

# 后台
```
//点击触屏点
private void map1_MapGesture(object sender, Map.MapGestureEventArgs e)
{
if (e.Gesture == GestureType.Tap)
{
List<Graphic> list = new List<Graphic>(e.DirectlyOver(1));
if(list.Count>0)
{
foreach (Graphic g in list)
{
MyInfoWindow.Anchor = e.MapPoint;
MyInfoWindow.IsOpen = true;
//Since a ContentTemplate is defined, Content will define the DataContext for the ContentTemplate
MyInfoWindow.Content = g.Attributes;
// return;
}
}
else
{
InfoWindow.Anchor = e.MapPoint;
InfoWindow.IsOpen = true;
InfoWindow.Content = e.MapPoint;
};
}
}
private void PhoneApplicationPage_ManipulationCompleted(object sender, System.Windows.Input.ManipulationCompletedEventArgs e)
{
MyInfoWindow.IsOpen = false;
this.InfoWindow.IsOpen = false;
}
如果是mouseClick事件的话：
GraphicsLayer featureLayer = MyMap.Layers["graphicesLayer"] as GraphicsLayer;
System.Windows.Point screenPnt = MyMap.MapToScreen(e.MapPoint);
// Account for difference between Map and application origin
GeneralTransform generalTransform = MyMap.TransformToVisual(Application.Current.RootVisual);
System.Windows.Point transformScreenPnt = generalTransform.Transform(screenPnt);
IEnumerable<Graphic> selected =
featureLayer.FindGraphicsInHostCoordinates(transformScreenPnt);
foreach (Graphic g in selected)
{
MyInfoWindow.Anchor = e.MapPoint;
MyInfoWindow.IsOpen = true;
//Since a ContentTemplate is defined, Content will define the DataContext for the ContentTemplate
MyInfoWindow.Content = g.Attributes;
return;
}
//如果前台声明过InfoWindow的话，后台不需要声明了，直接赋值，
下面这种是后台写法
InfoWindow window = new InfoWindow()
{
Anchor = e.MapPoint,
Map = MyMap,
IsOpen = true,
ContentTemplate = LayoutRoot.Resources["LocationInfoWindowTemplate"]
 as System.Windows.DataTemplate,
//Since a ContentTemplate is defined, Content will define the 
DataContext for the ContentTemplate
Content = e.MapPoint
};
LayoutRoot.Children.Add(window);</pre>
实现的效果：![](http://images.cnblogs.com/cnblogs_com/dubaokun/201212/201212162156109541.png)

&nbsp;

后台手动给InfoWindow 的Content赋值
```

# 前台
```
<Grid.Resources>

<DataTemplate x:Key="LocationInfoWindowTemplate">
<StackPanel >
<!-- <TextBlock Text="Location:" Foreground="Black" />
<TextBlock Text="{Binding X, StringFormat=X\=\{0:0.000\}}" Foreground="Black" />
-->
<TextBlock Text="{Binding ElementName=responseTextBlock,Path=Text}" Foreground="Black"/>
</StackPanel>
</DataTemplate>
</Grid.Resources>
<TextBlock Text="" Visibility="Collapsed" Name="responseTextBlock" Height="50" TextAlignment="Center" Foreground="Blue" />
<esriToolkit:InfoWindow x:Name="MyInfo" Content="InfoWindow" HorizontalAlignment="Left" CornerRadius="15" Background="White" BorderBrush="Gray" BorderThickness="1" >
</esriToolkit:InfoWindow>
```

#后台：
```
responseTextBlock.Text="aaaaaaaaaaaaaaaaaa";//Text可以随意的赋值
MyInfo.Anchor = point;
MyInfo.Map = MyMap;
MyInfo.IsOpen = true;
MyInfo.ContentTemplate = LayoutRoot.Resources["LocationInfoWindowTemplate"] as System.Windows.DataTemplate;
//Since a ContentTemplate is defined, Content will define the DataContext for the ContentTemplate
MyInfo.Content = responseTextBlock.Text;
```