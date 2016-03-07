title: windows store开发与Wp8开发不同之处1
categories:
  - WP8
date: 2013-05-23 18:18:59
tags:
  - WP8
---

首先Wp向win8的迁移（各种流之间 的转换）：
<div>

保存图片到本地
<div id="cnblogs_code_open_aad7898e-6baf-451f-b46b-28ad9f5b6943">
<pre>private async Task SaveImageFromUrl(string uri, string filename)
        {

            var rass = RandomAccessStreamReference.CreateFromUri(new Uri(uri));
            IRandomAccessStream inputStream = await rass.OpenReadAsync();
            Stream input = WindowsRuntimeStreamExtensions.AsStreamForRead(inputStream.GetInputStreamAt(0));
            try
            {
                //获取图片扩展名的Guid
                StorageFolder folder = KnownFolders.PicturesLibrary;
                StorageFile outputFile = await folder.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
                using (IRandomAccessStream outputStream = await outputFile.OpenAsync(FileAccessMode.ReadWrite))
                {
                    Stream output = WindowsRuntimeStreamExtensions.AsStreamForWrite(outputStream.GetOutputStreamAt(0));
                    await input.CopyToAsync(output);
                    output.Dispose();
                    input.Dispose();
                }
            }
            catch (Exception)
            {
            }
        }</pre>
</div>
</div>
根据图片uri保存到本地的函数，即以上为图片uri和图片名称的转换，另以下三种转换：

1、FileName转换为Stream，图片可为本地图片，也可为应用程序中图片
<div>

图片转换为流
<div id="cnblogs_code_open_4762fed1-99a1-455b-95be-f974294189a6">
<pre>private async Task&lt;Stream&gt; ImageNameToStream(string filename)
        {
            try
            {
                ////本地图片库
                //StorageFolder folder = KnownFolders.PicturesLibrary;//本地图片库
                //StorageFile storagefile = await folder.GetFileAsync(filename);

                //应用程序Images文件夹图片
                Uri _baseUri = new Uri("ms-appx:///");
                Uri uri = new Uri(_baseUri, "../Images/" + filename);
                StorageFile storagefile = await StorageFile.GetFileFromApplicationUriAsync(uri);

                IRandomAccessStream irandom = await storagefile.OpenAsync(FileAccessMode.Read);
                Stream outPutstream = irandom.GetInputStreamAt(0).AsStreamForRead();
                return outPutstream;
            }
            catch (Exception ex)
            {
                return null;
            }
        }</pre>
<div>2、Stream转换成文件，图片保存到本地流转换成本地图片</div>
</div>
</div>
<div>
<div id="cnblogs_code_open_97cafaf2-6d76-49dd-a505-a7160b157674">
<pre>private async Task StreamToFileName(Stream inputstream, string filename)
        {
            try
            {
                StorageFolder folder = KnownFolders.PicturesLibrary;
                StorageFile outputFile = await folder.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
                using (IRandomAccessStream output = await outputFile.OpenAsync(FileAccessMode.ReadWrite))
                {
                    Stream outputstream = WindowsRuntimeStreamExtensions.AsStreamForWrite(output.GetOutputStreamAt(0));
                    await inputstream.CopyToAsync(outputstream);
                    outputstream.Dispose();
                    inputstream.Dispose();
                }
            }
            catch (Exception ex)
            {
            }
        }</pre>
</div>
</div>
3、图片Uri转换成流网络图片Uri转换成流
<div>
<div id="cnblogs_code_open_fd849e9e-a8ee-4020-aebd-1fd3ca2257fe">
<pre>private async Task&lt;Stream&gt; UriToStream(string uri)
        {
            var rass = RandomAccessStreamReference.CreateFromUri(new Uri(uri));
            IRandomAccessStream inputStream = await rass.OpenReadAsync();
            Stream input = WindowsRuntimeStreamExtensions.AsStreamForRead(inputStream.GetInputStreamAt(0));
            return input;
        }</pre>
</div>
</div>
若有其他流与Metro流之间的转换,参考[http://www.cnblogs.com/jing870812/archive/2012/04/12/2444870.html](http://www.cnblogs.com/jing870812/archive/2012/04/12/2444870.html)

今天在Stream与IrandomAccessStream之间转换时，感觉很纠结，所以干脆先把想到的一些场景都罗列了一下，希望下次再用的时候就不用这么毛手毛脚的了。。。

**Stream 转IRandomAccessStream**
<div>
<div id="highlighter_554296">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>
<div>`方法一：`</div>
<div>`byte``[] bytes = StreamToBytes(stream);`</div>
<div>`InMemoryRandomAccessStream memoryStream = ``new` `InMemoryRandomAccessStream();`</div>
<div>`DataWriter datawriter = ``new` `DataWriter(memoryStream.GetOutputStreamAt(0));`</div>
<div>`datawriter.WriteBytes(bytes);`</div>
<div>`await datawriter.StoreAsync();`</div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
<div>
<div>`方法二：`</div>
<div>`var randomAccessStream = ``new` `InMemoryRandomAccessStream();`</div>
<div>`var outputStream = randomAccessStream.GetOutputStreamAt(0);`</div>
<div>`await RandomAccessStream.CopyAsync(stream.AsInputStream(), outputStream);`</div>
<div></div>
<div>**IRandomAccessStream 转 Stream**</div>
<div>
<div>`Stream stream=WindowsRuntimeStreamExtensions.AsStreamForRead(randomStream.GetInputStreamAt(0));`</div>
<div>**Ibuffer转Stream**</div>
<div>
<div>`Stream stream = WindowsRuntimeBufferExtensions.AsStream(buffer);`</div>
<div>

**Stream转Ibuffer**
<div>
<div>
<div id="highlighter_328703">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>` <code>MemoryStream memoryStream = ``new` `MemoryStream(); `</code></div>
<div>`if` `(stream != ``null``)`</div>
<div>` ``{`</div>
<div>`      ``byte``[] bytes = ReadFully(stream);`</div>
<div>`      ``if` `(bytes != ``null``)`</div>
<div>`      ``{`</div>
<div>`           ``var binaryWriter = ``new` `BinaryWriter(memoryStream);`</div>
<div>`           ``binaryWriter.Write(bytes);`</div>
<div>`       ``}`</div>
<div>`  ``}`</div>
<div>` ``IBuffer buffer=WindowsRuntimeBufferExtensions.GetWindowsRuntimeBuffer(memoryStream,0,(``int``)memoryStream.Length);`</div></td>
</tr>
</tbody>
</table>
</div>
</div>
**Ibuffer转byte[]**
<div>
<div>`byte``[] bytes=WindowsRuntimeBufferExtensions.ToArray(buffer,0,(``int``)buffer.Length);`</div>
<div></div>
<div>**Byte[]转Ibuffer**</div>
<div>`WindowsRuntimeBufferExtensions.AsBuffer(bytes,0,bytes.Length);`</div>
<div></div>
<div>**Ibuffer转IrandomAccessStream**</div>
<div>
<div>
<div id="highlighter_509672">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>
<div>`InMemoryRandomAccessStream inStream = ``new` `InMemoryRandomAccessStream();`</div>
<div>`DataWriter datawriter = ``new` `DataWriter(inStream.GetOutputStreamAt(0));`</div>
<div>`datawriter.WriteBuffer(buffer,0,buffer.Length);`</div>
<div>`await datawriter.StoreAsync();`</div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
_**IrandomAccessStream转Ibuffer**_
<div>
<div>`FileInputStream inputStream=randomStream.GetInputStreamAt(0) ``as` `FileInputStream;`</div>
<div>

**IRandomAccessStream转FileOutputStream**
<div>
<div>`FileOutputStream outStream= randomStream.GetOutputStreamAt(0) ``as` `FileOutputStream;`</div>
<div></div>
<div>**Stream转byte[]**</div>
<div>

public static byte[] ConvertStreamTobyte(Stream input)
{
byte[] buffer = new byte[16 * 1024];
using (MemoryStream ms = new MemoryStream())
{
int read;
while ((read = input.Read(buffer, 0, buffer.Length)) &gt; 0)
{
ms.Write(buffer, 0, read);
}
return ms.ToArray();
}
}
**Byte转Stream**
<div>`public` `Stream BytesToStream(``byte``[] bytes)`</div>
<div>`        ``{`</div>
<div>`            ``Stream stream = ``new` `MemoryStream(bytes);`</div>
<div>`            ``return` `stream;`</div>
<div>`        ``}`</div>
<div>**Stream转MemoryStream**</div>
<div>
<div>`public` `static` `MemoryStream ConvertStreamToMemoryStream(Stream stream)`</div>
<div>`        ``{`</div>
<div>`            ``MemoryStream memoryStream = ``new` `MemoryStream();`</div>
<div>`            ``if` `(stream != ``null``)`</div>
<div>`            ``{`</div>
<div>`                ``byte``[] buffer = ReadFully(stream);`</div>
<div>`                ``if` `(buffer != ``null``)`</div>
<div>`                ``{`</div>
<div>`                    ``var binaryWriter = ``new` `BinaryWriter(memoryStream);`</div>
<div>`                    ``binaryWriter.Write(buffer);`</div>
<div>`                ``}`</div>
<div>`            ``}`</div>
<div>`            ``return` `memoryStream;`</div>
<div>`        ``}`</div>
</div>
</div>
</div>
<div></div>
<div></div>
</div>
</div>
&nbsp;

</div>
</div>
</div>
<div></div>
&nbsp;

</div>
</div>
</div>
</div>