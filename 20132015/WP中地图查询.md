title: WP中地图查询
categories:
  - WP8
date: 2013-08-11 15:45:22
tags:
  - WP8
---

一、IdentifyTask：单个服务的使用（本人感觉适合查询底图），带条件查询，是对一个地图服务多个图层（全部，或者指定几个ID索引）做空间识别查询
<pre>       private void IdentityQuery(MapPoint point)
        {
            try
            {
                if (point != null)
                {
                    IdentifyParameters identifyParameters = new IdentifyParameters()
                    {
                        Geometry = point,
                        MapExtent = MyMap.Extent,
                        Tolerance = 10,
                        ReturnGeometry = true,
                        //Width = (int)MyMap.ActualWidth,
                        //Height = (int)MyMap.ActualHeight,
                        LayerOption = LayerOption.visible,
                        //  SpatialReference = MyMap.SpatialReference
                    };
                    string url = url = App.Current.Resources[mapLayerMgr.BussineLayer] as string;
                    IdentifyTask identifyTask = new IdentifyTask(url);
                    identifyTask.ExecuteCompleted += identifyTask_ExecuteCompleted;
                    identifyTask.Failed += IdentifyTask_Failed;
                    identifyTask.ExecuteAsync(identifyParameters);
                    GraphicsLayer businessGraphicsLayer = MyMap.Layers["businessGraphicsLayer"] as GraphicsLayer;
                    businessGraphicsLayer.ClearGraphics();
                    this.MyMap.SnapToLevels = true;
                     point.SpatialReference = MyMap.SpatialReference;
                    Graphic graphic = new Graphic()
                    {
                        Geometry = point,
                        Symbol = LayoutRoot.Resources["DefaultPictureSymbol"] as Symbol
                    };
                    businessGraphicsLayer.Graphics.Add(graphic);
                }

            }
            catch (Exception ex)
            {

            }
        }
 private void identifyTask_ExecuteCompleted(object sender, IdentifyEventArgs e)
        {
            if (e.IdentifyResults != null &amp;&amp; e.IdentifyResults.Count &gt; 0)
            {
                              ShowFeatures(e.IdentifyResults);//处理查询结果
            }
       }</pre>
二、FindTask 对一个地图服务多个图层（全部，或者指定几个ID索引）做属性查询，一般作为业务图层使用
<pre>public void QueryAttribute(string strText)
        {
     FindTask findTask = new FindTask("http://gis.huiyang.gov.cn:8399/arcgis/rest/services/行政办公政务底图/惠阳公共管理版电子地图GDBM/MapServer");
            findTask.ExecuteCompleted += FindTask_ExecuteCompleted;
            findTask.Failed += FindTask_Failed;

            FindParameters findParameters = new FindParameters();
            for (int i = 0; i &lt; urlList.Count; i++)
            {
                findParameters.LayerIds.Add(urlList[i]);
            }
            findParameters.SpatialReference = _map.SpatialReference;
            findParameters.Contains = true;//默认模糊查询

            findParameters.SearchText = strText;

            findTask.ExecuteAsync(findParameters);
            _map.Cursor = Cursors.Wait;
}
  private void FindTask_ExecuteCompleted(object sender, FindEventArgs e)
 {
     //处理查询结果
 }</pre>
三、QueryTask 只能针对一个图层进行空间或属性查询
<pre> 
    //string url = urlStr+"/"+urlList[i];
                        //QueryTask queryTask = new QueryTask(url);
                        //queryTask.Failed += QueryTask_Failed;
                        //queryTask.ExecuteCompleted += QueryTask_ExecuteCompleted;
                        //Query query = new Query();
                        //query.OutSpatialReference = _map.SpatialReference;
                        //query.OutFields.AddRange(new string[] { "*" });// Specify fields to return from initial query
                        //// This query will just populate the drop-down, so no need to return geometry
                        //query.ReturnGeometry = false;
                        //// Return all features
                        //query.Where = "1=1";  //这个条件必须写，意思是条件为真
                        ////query.Text = txtSearch.Text.Trim();</pre>