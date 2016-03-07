title: wp独立存储空间之——图片下载
categories:
  - WP8
date: 2013-08-20 11:05:55
tags:
  - WP8
---

WebClient - 将数据发送到指定的 URI，或者从指定的 URI 接收数据的类
DownloadStringAsync(Uri address, Object userToken) - 以字符串的形式下载指定的 URI 的资源
UploadStringAsync(Uri address, string data) - 以字符串的形式上传数据到指定的 URI。所使用的 HTTP 方法默认为 POST
OpenReadAsync(Uri address, Object userToken) - 以流的形式下载指定的 URI 的资源
OpenWriteAsync(Uri address, string method, Object userToken) - 打开流以使用指定的方法向指定的 URI 写入数据
<pre>/// &lt;summary&gt;
/// 使用webclient下载图片
/// &lt;/summary&gt;
/// &lt;param name="zimgName"&gt;图片名称&lt;/param&gt;
/// &lt;param name="zimgURL"&gt;图片地址&lt;/param&gt;
public void WriteZImg(string zimgName, string zimgURL)
{
try
{
//声明图片保存路径变量
string imageSavePath = string.Empty;
using (IsolatedStorageFile storageFile = IsolatedStorageFile.GetUserStoreForApplication())//获取从虚拟主机域调用的应用程序所使用的用户范围的独立存储
{
string dir = "Main";//保存图片的目录
if (!storageFile.DirectoryExists(dir))//判断目录是否存在
storageFile.CreateDirectory(dir);//创建目录
imageSavePath = dir + "\\" + zimgName;//拼接图片保存路径
//long maxSize = storageFile.Quota;//用来获取独立存储的最大可用空间量
//long availabelSize = storageFile.AvailableFreeSpace;//用来获取独立存储的可用空间量
}
WebClient wc = new WebClient();
wc.OpenReadCompleted += new OpenReadCompletedEventHandler(wc_OpenReadCompleted);
//注：由于异步下载并不会按照顺序下载，所以之前一直无法知道现在下载的到底是哪一张图片，经过网上查找资料，
//终于明白如何得知当前下载的是哪一张图片，因为
//WebClient.OpenReadAsync (Uri, Object)方法的第二个对象的含义是：一个用户定义对象，此对象将被传递给完成异步操作时所调用的方法。
//所以在下载完成的事件中可以通过OpenReadCompletedEventArgs的UserState属性来得知当前下载的是那张图片
wc.OpenReadAsync(new Uri(zimgURL, UriKind.RelativeOrAbsolute), imageSavePath); //打开流向指定资源的可读流。
}
catch (Exception e) { }
}
/// &lt;summary&gt;
/// 图片下载完成事件
/// &lt;/summary&gt;
/// &lt;param name="sender"&gt;&lt;/param&gt;
/// &lt;param name="e"&gt;&lt;/param&gt;
void wc_OpenReadCompleted(object sender, OpenReadCompletedEventArgs e)
{
if (e.Error == null &amp;&amp; !e.Cancelled)
{
try
{
using (IsolatedStorageFile storageFile = IsolatedStorageFile.GetUserStoreForApplication())
{
if (!storageFile.FileExists(e.UserState.ToString()))
{
using (Stream storageFileStream = storageFile.OpenFile(e.UserState.ToString(), FileMode.Create, FileAccess.Write))
{
#region 保存jpg格式的图片
//BitmapImage image = new BitmapImage();
//image.SetSource(e.Result);
//WriteableBitmap wb = new WriteableBitmap(image);
//Extensions.SaveJpeg(wb, storageFileStream, wb.PixelWidth, wb.PixelHeight, 0, 100);
////另一种保存图片的方法
////wb.SaveJpeg(storageFileStream, wb.PixelWidth, wb.PixelHeight, 0, 100);
////以下的方法是用来读取程应用程序包中的图片
////StreamResourceInfo resourceInfo = Application.GetResourceStream(new Uri(picPath));
////BitmapImage bitmap = new BitmapImage();
////bitmap.SetSource(resourceInfo.Stream);
#endregion
#region 保存png格式的图片
byte[] _imgBytes = new byte[e.Result.Length];
e.Result.Read(_imgBytes, 0, _imgBytes.Length);
storageFileStream.Write(_imgBytes, 0, _imgBytes.Length);
#endregion
}
}
}
}
catch (Exception ex)
{
/　　/Exception handle appropriately for your app
}
}
else
{
//Either cancelled or error handle appropriately for your app
}
}
/// &lt;summary&gt;
/// 从独立存储空间读取图片
/// &lt;/summary&gt;
/// &lt;param name="zimgName"&gt;图片名称&lt;/param&gt;
/// &lt;returns&gt;&lt;/returns&gt;
public BitmapImage ReadZImg(string zimgName)
{
try
{
using (IsolatedStorageFile storageFile = IsolatedStorageFile.GetUserStoreForApplication())
{
BitmapImage bi = new BitmapImage();
string fileDir = "Main";
string filePath = fileDir + "\\" + zimgName;
if (storageFile.FileExists(filePath))
{
using (IsolatedStorageFileStream fileStream = storageFile.OpenFile(filePath, FileMode.Open, FileAccess.Read))
{
bi.SetSource(fileStream);
return bi;
}
}
else
{
return null;
}
}
}
catch (Exception e) { return null; }

}</pre>