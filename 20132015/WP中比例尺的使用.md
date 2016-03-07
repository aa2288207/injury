title: WP中比例尺的使用
categories:
  - WP8
date: 2013-06-04 14:27:59
tags:
  - WP8
---

**<span style="text-decoration: underline;">Setting the MapUnit Property:</span>**

For the ScaleLine to function correctly, it is possible to set the [MapUnit](http://help.arcgis.com/en/webapi/silverlight/apiref/ESRI.ArcGIS.Client.Toolkit~ESRI.ArcGIS.Client.Toolkit.ScaleLine~MapUnit.html) to whatever unit the Map's [SpatialReference](http://help.arcgis.com/en/webapi/silverlight/apiref/ESRI.ArcGIS.Client~ESRI.ArcGIS.Client.Geometry.SpatialReference.html) is using. For example: if the Map's SpatialReference is based on a Geographic coordinate system use DecimalDegrees (aka. Longitude/Latitude) units; if it is a UTM or WebMercator (SRID=102100) projection use Meters.

When the Map is using Geographic units (ie. DecimalDegrees) or WebMercator projection, the approximate scale will be calculated at the center of the map. If any other units are used, a direct conversion between MapUnit's and Metric/US units is used and scale distortion is not taken into account.

**<span style="text-decoration: underline;">Default MapUnit:</span>**

If the [MapUnit](http://help.arcgis.com/en/webapi/silverlight/apiref/ESRI.ArcGIS.Client.Toolkit~ESRI.ArcGIS.Client.Toolkit.ScaleLine~MapUnit.html) is not set manually, the scale line control will use a default map unit which is calculated from the spatial reference of the map or from the [ESRI.ArcGIS.Client.ArcGISTiledMapServiceLayer.Units](http://help.arcgis.com/en/webapi/silverlight/apiref/ESRI.ArcGIS.Client~ESRI.ArcGIS.Client.ArcGISTiledMapServiceLayer~Units.html) of the layers inside the map. If the spatial reference is Geographic WGS84 (SRID=4326) or WebMercator (SRID=102100), the default MapUnit will be DecimalDegrees and Meters respectively. For others spatial references, the scale line will look at the Units property of the layers having the same spatial reference than the map. If no layers are found, the default DecimalDegrees will be used.

**<span style="text-decoration: underline;">Controling the text on the ScaleLine:</span>**

It is not possibly to directly control the values of the text on the ScaleLine as a Property that can be set. The text as part of the ScaleLine that displays is automatically adjusted as the scale of the map changes when the ScaleLine is bound to a Map Control. This also means that it is not possible to control the scale (ie. zoom level) of the Map Control via a Property of the ScaleLine Control.

**<span style="text-decoration: underline;">ScaleBar style</span>**

The ScaleLine control replaces the ScaleBar control, which is deprecated. You can apply a template to the ScaleLine control to render with the same look and feel as the ScaleBar control. Below is a sample of a ScaleLine style allowing to get a scale bar with metric units.
XAML![](http://help.arcgis.com/en/webapi/silverlight/apiref/dotnetimages/copycode.gif)
<pre>&lt;esri:ScaleLine Name="ScaleLine1" Map="{Binding ElementName=Map1}"
     HorizontalAlignment="Left" VerticalAlignment="Top"  
     TargetWidth="400" 
     Foreground="Black" FontFamily="Courier New" FontSize="18" /&gt;</pre>
C#![](http://help.arcgis.com/en/webapi/silverlight/apiref/dotnetimages/copycode.gif)Copy Code
<pre>//Create a new ScaleLine Control and add it to the LayoutRoot (a Grid in the XAML)
ESRI.ArcGIS.Client.Toolkit.ScaleLine ScaleLine1 = new ESRI.ArcGIS.Client.Toolkit.ScaleLine();
LayoutRoot.Children.Add(ScaleLine1);

//Associate the ScaleLine with Map Control (analagous to a OneTime Binding). Most common coding pattern.
ScaleLine1.Map = Map1;

//Alternative Binding Method. Useful if the ScaleLine's Properties will dynamically impact other objects.
//System.Windows.Data.Binding myBinding = new System.Windows.Data.Binding();
//myBinding.ElementName = "Map1";
//ScaleLine1.SetBinding(ESRI.ArcGIS.Client.Toolkit.ScaleLine.MapProperty, myBinding);

//Set the alignment properties relative the hosting Grid Control
ScaleLine1.HorizontalAlignment = System.Windows.HorizontalAlignment.Left;
ScaleLine1.VerticalAlignment = System.Windows.VerticalAlignment.Top;

//Set the Map units for the ScaleLine
ScaleLine1.MapUnit = ESRI.ArcGIS.Client.Toolkit.ScaleLine.ScaleLineUnit.DecimalDegrees;

//Set the target width for the ScaleLine
ScaleLine1.TargetWidth = 400;

//Set ScaleLine color and related Font information
System.Windows.Media.Color myScaleLineColor = Color.FromArgb(255, 0, 0, 0);
ScaleLine1.Foreground = new System.Windows.Media.SolidColorBrush(myScaleLineColor);
ScaleLine1.FontFamily = new FontFamily("Courier New");
ScaleLine1.FontSize = 18;</pre>