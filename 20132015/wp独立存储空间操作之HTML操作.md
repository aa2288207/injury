title: wp 独立存储空间操作之HTML操作
categories:
  - WP8
date: 2013-08-11 13:27:37
tags:
  - WP8
---

一、保存HTML文件
<pre>
static string path = "/web.htm";
/// &lt;summary&gt;
/// 把保存HTML到独立存储空间
/// &lt;/summary&gt;
/// &lt;param name="strWebContent"&gt;&lt;/param&gt;
public static void SaveStringToIsoStore(string strWebContent)
{

IsolatedStorageFile isoStore = IsolatedStorageFile.GetUserStoreForApplication();//获取本地应用程序存储对象

//清除之前保存的网页
if (isoStore.FileExists(path) == true)
{
isoStore.DeleteFile(path);
}
StreamResourceInfo sr = new StreamResourceInfo(new MemoryStream(Encoding.UTF8.GetBytes(strWebContent)), "html/text");//转化为流
using (BinaryReader br = new BinaryReader(sr.Stream))
{
byte[] data = br.ReadBytes((int)sr.Stream.Length);
//保存文件到本地存储
using (BinaryWriter bw = new BinaryWriter(isoStore.CreateFile(path)))
{
bw.Write(data);
bw.Close();
}
}

}

二、修改HTML标签值
/// &lt;summary&gt;
/// 修改HTML
/// &lt;/summary&gt;
/// &lt;param name="html"&gt;&lt;/param&gt;
/// &lt;returns&gt;&lt;/returns&gt;
public static string UpdateHTM(string html)
{
// IsolatedStorageFile isoStore = IsolatedStorageFile.GetUserStoreForApplication();//获取本地应用程序存储对象

HtmlDocument doc = new HtmlDocument();
doc.LoadHtml(html);
var metaTags = doc.DocumentNode.Descendants("IMG").ToArray();
if (metaTags != null)
{
for (int i = 0; i &lt; metaTags.Length; i++)
{
var tag = metaTags[i];
if (tag.Attributes["src"] != null)
{
string value = tag.Attributes["src"].Value;
string name = tag.Attributes["src"].Name;
if (WebServiceCall.imgList.Count != 0 &amp;&amp; metaTags.Length == WebServiceCall.imgList.Count)
{
string imgPath = WebServiceCall.imgList[i];
html = html.Replace(value, imgPath);
// tag.Attributes["src"].Value=imgPath;
}
}
}

}
return html;

}

三、读取HTML文件到HTML字符串
/// &lt;summary&gt;
/// 从独立存储空间读取ＨＴＭＬ
/// &lt;/summary&gt;
/// &lt;returns&gt;&lt;/returns&gt;
public static string ReadHTML()
{
string strHtml = "";
IsolatedStorageFile isoStore = IsolatedStorageFile.GetUserStoreForApplication();//获取本地应用程序存储对象

//清除之前保存的网页
if (isoStore.FileExists(path) == true)
{
using (IsolatedStorageFileStream fs = isoStore.OpenFile(path, FileMode.Open, FileAccess.Read, FileShare.None))
{
StreamReader sr = new StreamReader(fs, Encoding.UTF8);
strHtml = sr.ReadToEnd();
}
}
return strHtml;
}

&nbsp;

&nbsp;

(*^__^*) 嘻嘻……这些只是用到的，后续应该还会更多，会继续更新的。。。。
</pre>