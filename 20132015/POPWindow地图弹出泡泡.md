title: POPWindow 使用如地图弹出泡泡
tags:
  - Android
categories:
  - Android
date: 2014-01-05 07:55:46
---

1 、overlay_popup.xml  直接把layout放出来

[xml]
```
<?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?>
<RelativeLayout xmlns:android=&quot;http://schemas.android.com/apk/res/android&quot;
android:id=&quot;@+id/popup_view&quot;
android:layout_width=&quot;wrap_content&quot;
android:layout_height=&quot;wrap_content&quot;
android:background=&quot;@drawable/street_view_pop&quot;
android:paddingLeft=&quot;5.0dip&quot;
android:paddingRight=&quot;5.0dip&quot; &amp;gt;</pre>
<TextView
android:id=&quot;@+id/name&quot;
android:layout_width=&quot;wrap_content&quot;
android:layout_height=&quot;wrap_content&quot;
android:layout_marginLeft=&quot;5dp&quot;
android:maxLength=&quot;15&quot;
android:singleLine=&quot;true&quot;
android:textColor=&quot;@color/white&quot;
android:textSize=&quot;14sp&quot; />

<ImageView
android:id=&quot;@+id/imgView&quot;
android:layout_width=&quot;wrap_content&quot;
android:layout_height=&quot;wrap_content&quot;
android:layout_marginLeft=&quot;5dp&quot;
android:layout_marginRight=&quot;5dp&quot;
android:layout_toRightOf=&quot;@+id/name&quot;
android:background=&quot;@drawable/camera_pop&quot; />

</RelativeLayout>

[/xml]
```

2、加载POPView

```java
private void initPopView(){
 if(null == popView){
 popView = getLayoutInflater().inflate(R.layout.overlay_popup, null);
 mapView.addView(popView, new MapView.LayoutParams(
 MapView.LayoutParams.WRAP_CONTENT,
 MapView.LayoutParams.WRAP_CONTENT, null,
 MapView.LayoutParams.BOTTOM_CENTER));
 popView.setVisibility(View.GONE);
 }

}
```

3:如何把这个View添加到MapView中.
通常是在mapView中点击某个位置,弹出popView
或者点击某个Overlay弹出popView,这里用点击Overlay来说明,

overlay有onTap()方法,你可以实现自己的overlay,overideonTap()方法,弹出popView,

也可以使用setOnFocusChangeListener(),在listener中实现弹出popView,.
<!--[endif]-->

```java
private final ItemizedOverlay.OnFocusChangeListener onFocusChangeListener = new ItemizedOverlay.OnFocusChangeListener() {
@Override
 public void onFocusChanged(ItemizedOverlay overlay, OverlayItem newFocus) {
 //创建气泡窗口</p>
if (popView != null) {
 popView.setVisibility(View.GONE);
 }
if (newFocus != null) {</p>
MapView.LayoutParams geoLP = (MapView.LayoutParams) popView.getLayoutParams();
 geoLP.point = newFocus.getPoint();//这行用于popView的定位
 TextView title = (TextView) popView.findViewById(R.id.map_bubbleTitle);
 title.setText(newFocus.getTitle());</p>
TextView desc = (TextView) popView.findViewById(R.id.map_bubbleText);
 if (newFocus.getSnippet() == null || newFocus.getSnippet().length() == 0) {
 desc.setVisibility(View.GONE);
 } else {
 desc.setVisibility(View.VISIBLE);
 desc.setText(newFocus.getSnippet());
 }
 mapView.updateViewLayout(popView, geoLP);
 popView.setVisibility(View.VISIBLE);
 }
 }
 }
```

**或者onTap的使用：**

```java
// 点击地图上的图层触发的
 @Override
 protected boolean onTap(int index) {
 // 在此处理item点击事件
 final OverlayItem item = getItem(index);
 TextView name = (TextView) popView.findViewById(R.id.name);

//这两句可设置X、Y的偏移
 layout_x = -drawable.getIntrinsicWidth()+ DisplayUtil.dip2px(Float.valueOf(&quot;10&quot;), mDensity);
 layout_y = -drawable.getIntrinsicHeight();
 String[] str = item.getTitle().split(&quot;,&quot;);
 final String sid = str[0];
 final String nameText = str[1];
 name.setText(nameText);
 if (popView != null) {
 popView.setVisibility(View.GONE);
 }
 MapActivity.mMapView.getController().animateTo(item.getPoint());
 MapView.LayoutParams geoLP = (com.baidu.mapapi.map.MapView.LayoutParams) popView
 .getLayoutParams();

geoLP.x = this.layout_x;// Y轴偏移
 geoLP.y = this.layout_y;// Y轴偏移
 geoLP.point = item.getPoint();// 这行用于popView的定位
 MapActivity.mMapView.updateViewLayout(popView, geoLP);
 popView.setVisibility(View.VISIBLE);

}

// 点击地图时触发，点击其他隐藏POPView
 @Override
 public boolean onTap(GeoPoint arg0, MapView arg1) {
 if (popView != null) {
 popView.setVisibility(View.GONE);
 }
 return false;
 }

```