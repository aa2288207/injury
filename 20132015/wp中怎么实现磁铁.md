title: wp中怎么实现磁铁
categories:
  - WP8
date: 2013-07-16 17:10:20
tags:
  - WP8
---

网上有很多方法实现磁铁的方式，最多的也就是
[http://www.cnblogs.com/wpdev/archive/2011/10/17/windows-phone-hubtile.html](http://www.cnblogs.com/wpdev/archive/2011/10/17/windows-phone-hubtile.html)
但是这个HubTile不好使，动态还行，但是字体颠倒，静态更没法用
最终经过千辛万苦终于从朋友得知了一个第三方控件


添加引用：
```
xmlns:c4f="clr-namespace:Coding4Fun.Toolkit.Controls;assembly=Coding4Fun.Toolkit.Controls"

<c4f:Tile Margin="0, 12, 12, 0" Width="120" Height="120" >
<Border>
<Grid>
<Image Source="" Stretch="Fill" />
<TextBlock Text="" Foreground="White" FontSize="20" Margin="0,90,0,0" TextAlignment="Center" />
</Grid>
</Border>
</c4f:Tile>
```
需要的亲们可以去哪儿下载: [Demo下载](http://pan.baidu.com/share/link?shareid=574172447&amp;uk=957296843)

上面的这个是写死的,如果想改成动态的而且listbox可以水平排列则
```
<listbox>
<Listbox.ItemsPanel>

<ItemsPanelTemplate>
<StackPanel Orientation="Horizontal" />
</ItemsPanelTemplate>
</Listbox.ItemsPanel>
<Listbox.ItemTemplate>
<DataTemplate>
<StackPanel Orientation="Horizontal">
<RadioButton GroupName="eyeGroup" Content="{Binding Title}" IsChecked="{Binding IsSelected, Mode=TwoWay}"></RadioButton>
</StackPanel>
</DataTemplate>
</Listbox.ItemTemplate>
</ItemsControl>

</Listbox.ItemsPanel>
</listbox>
```