title: Android之XML操作
categories:
  - Android
date: 2013-11-19 03:05:13
tags:
  - Android
---

一、解析XML：
```
/*
* 解析XML
*/
private void readerFertilizerXML() {
try {
// 获取事件源
SAXParserFactory factory = SAXParserFactory.newInstance();
XMLReader xmlReader = factory.newSAXParser().getXMLReader();
// 等同于这句，为XMLReader设置内容处理器
xmlReader.setContentHandler(xmlHandler);
// 解析XML文档（Assets目录下的XML文件）
xmlReader.parse(new InputSource(this.getResources().getAssets()
.open("Fertilizer.xml")));

} catch (SAXException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (ParserConfigurationException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (IOException e) {
// TODO Auto-generated catch block
e.printStackTrace();
}
}
```