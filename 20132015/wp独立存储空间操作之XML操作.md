title: wp 中独立存储空间操作之XML操作
categories:
  - WP8
date: 2013-08-11 13:21:04
tags:
  - WP8
---

一、window phone 利用StreamWriter写入文件问题
```
IsolatedStorageFile myIsolatedStorage = IsolatedStorageFile.GetUserStoreForApplication();
IsolatedStorageFileStream fileStream = myIsolatedStorage.OpenFile("myFile.txt", FileMode.Append, FileAccess.Write);
using (StreamWriter writer = new StreamWriter(fileStream))
{
writer.Write(input);
writer.Close();
}
```
二、创建文件夹
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
              {
               file.CreateDirectory(foldername);
            }
```
三、检查文件夹是否存在
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
              {
                  if (file.DirectoryExists(foldername))
                  {
                      MessageBox.Show("已存在");
                 }  
                  else
                 {
                     MessageBox.Show("不存在");
                  }
              }
```
四、删除目录
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
             {
                 file.DeleteDirectory(foldername);
             }
```
五、创建文件
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
            {         
                IsolatedStorageFileStream stream = file.CreateFile(filename);
                 stream.Close();
             }
```
六、检查文件是否存在
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
             {
                  if (file.FileExists(filename))
                   {
                     95MessageBox.Show("已存在" + filename);
                  }
                  else
                  {
                     MessageBox.Show("不存在");
                 }
             }```
七、删除文件
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
            {
                 file.DeleteFile(filename);
            }```
八、向文件里增加内容
```
 using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
  {
     using (IsolatedStorageFileStream stream = file.OpenFile(filename, FileMode.OpenOrCreate, FileAccess.ReadWrite))
      {
          StreamWriter writer = new StreamWriter(stream);
          writer.WriteLine(textBox1.Text);
          writer.Close();
          textBox1.Text = "";
       }          
 }
 ```
九、读取文件内容
```
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
            {
                using (IsolatedStorageFileStream stream = file.OpenFile(filename, FileMode.OpenOrCreate, FileAccess.ReadWrite))
               {
                 using (StreamReader  reader=new StreamReader (stream))
                   {
                      textBox1.Text = reader.ReadToEnd();
                  }
                }
            }
```
十、 程序配置信息保存
```
IsolatedStorageSettings.ApplicationSettings[settingname] = textBox2.Text;
             IsolatedStorageSettings.ApplicationSettings.Save();
             textBox2.Text = "";
```
十二、程序配置信息读取
``` 
if (IsolatedStorageSettings.ApplicationSettings.Contains(settingname))
           {
                textBox2.Text = IsolatedStorageSettings.ApplicationSettings[settingname].ToString();
            }
```

Demo一：

```
/// <summary>
/// 由xml字符串保存成xml文件
/// </summary>
/// <param name="xml"></param>
public void SaveXML(string xml)
{
try
{
string direction = "shared/transfers";
IsolatedStorageFile isoStore = IsolatedStorageFile.GetUserStoreForApplication();//获取本地应用程序存储对象
if (isoStore.DirectoryExists(direction)==false) //判断目录是否存在
{
isoStore.CreateDirectory(direction);
}
//清除之前保存的网页
if (isoStore.FileExists(confiPath) == true)//判断文件是否存在
{
isoStore.DeleteFile(confiPath);
}
//IsolatedStorageFileStream stream = isoStore.CreateFile(confiPath);
//stream.Close();
using(IsolatedStorageFileStream fileStream = new IsolatedStorageFileStream(confiPath, System.IO.FileMode.Create, isoStore))
{
//保存文件到本地存储
using (StreamWriter writer = new StreamWriter(fileStream))
{
writer.Write(xml);
writer.Close();

}
}
}
catch (Exception ex)
{

throw ex;
}
}
```

Demo二：
```
/// <summary>
/// 从独立存储空间读取xml文件到xml字符串
/// </summary>
/// <returns></returns>
public string ReadXML()
{
string xml;
using (IsolatedStorageFile file = IsolatedStorageFile.GetUserStoreForApplication())
{
using (IsolatedStorageFileStream stream = file.OpenFile(confiPath, FileMode.OpenOrCreate, FileAccess.ReadWrite))
{
using (StreamReader reader = new StreamReader(stream))
{
xml = reader.ReadToEnd();
}
}
}
return xml;
}
```

Demo三：
```
/// <summary>
/// 手动创建xml文件到独立存储空间
/// </summary>
/// <param name="value">标签的值</param>
public void WriteToFile(string value)
{
try
{
lock (_readLock)
{
string fileName = localVersionPath;
using (IsolatedStorageFile storage = IsolatedStorageFile.GetUserStoreForApplication())
{
if (storage.FileExists(fileName))
{
storage.DeleteFile(fileName);
}
XDocument _doc = new XDocument();
XElement root = new XElement("Root");//创建根节点
XElement _item = new XElement("Version");//创建一个XML元素
XAttribute version = new XAttribute("value", value);//创建一个XML属性

_item.Add(version);//将这个属性添加到 XML元素上
root.Add(_item);
//用_item 新建一个XML的Linq文档
_doc = new XDocument(new XDeclaration("1.0", "utf-8", "yes"), root);

// 创建独立存储文件流
IsolatedStorageFileStream location = new IsolatedStorageFileStream(fileName, System.IO.FileMode.Create, storage);
//将本地存储文件流转化为可写流
System.IO.StreamWriter file = new System.IO.StreamWriter(location);
//将XML文件 保存到流file上 即已经写入到手机本地存储文件上
_doc.Save(file);

file.Dispose();//关闭可写流
location.Dispose();//关闭手机本地存储流

}

}
}

catch (Exception)
{

}
}
```

Demo四：
```
/// <summary>
/// 解析XML文件
/// </summary>
public string ReadFromXml()
{
var xdata = "";
try
{

IsolatedStorageFile storage = IsolatedStorageFile.GetUserStoreForApplication();

if (!storage.FileExists(localVersionPath) || !storage.FileExists(confiPath))
{
// MessageBox.Show("文件不存在！");
return "";
}
using (IsolatedStorageFileStream fs = IsolatedStorageFile.GetUserStoreForApplication().OpenFile(localVersionPath, FileMode.Open, FileAccess.Read, FileShare.None))
{
XDocument doc = XDocument.Load(fs);
xdata = doc.Element("Root").Element("Version").Attribute("value").Value;
}
return xdata;

}
catch (Exception ex)
{
}
return xdata;
}
```

Demo 五：
```
/// <summary>
///解析XML字符串
/// </summary>
/// <param name="url">xml字符串</param>

public void ReaderXML(string url)
{

XElement xel;
//StreamResourceInfo xml = Application.GetResourceStream(new Uri(url, System.UriKind.Relative));
//XElement doc = XElement.Parse(content);
if (url.Trim() != "")
{
// xel = XElement.Load(xml.Stream);
xel = XElement.Parse(url);

foreach (XElement element in xel.Element("TopImage").Element("ImageList").Elements("Image"))
{
NewsInfo news = new NewsInfo();
news.NewsId = int.Parse(element.Attribute("newsId").Value);
news.ImageUrl = element.Value;
news.NewsTitle = element.Attribute("newsAbstract").Value;
news.NewsType = "新闻浏览";
imageList.Add(news);
}
}
}
```