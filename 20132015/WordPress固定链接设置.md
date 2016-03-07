title: WordPress固定链接设置
categories:
  - wordpress
date: 2013-06-28 14:54:53
tags:
  - wordpress
---

# WordPress固定链接设置

## 不要让日期出现在固定链接里面

这基于两个方面的考虑。一是如果数字出现在固定链接里面，等于提醒搜索引擎，这是很旧的内容了，没必要再爬一遍了。另外一个原因是，假如你要修改文章的日期重新发布的话，链接地址就变了，也就是意味着你的反向链接，PR 等等都没有了。

## 不要让分类的链接出现在固定链接里面

这一点是很多人都会忽略的地方。让分类出现在固定链接里面有两个缺陷：一是一篇文章如果选择了多个分类的话，则会出现多个链接地址，这很容易造成因为重复内容而被搜索引擎惩罚；二是有可能会造成关键词堆砌而被搜索引擎惩罚。

## 链接不要过深

这一点经常看到。很多wordpress 用户的固定链接是年/月/日/分类名/文章名。这种过于深的固定链接对搜索引擎是非常不友好的。

## 不要让中文字符出现在固定链接里面

虽然现在的搜索引擎已经能识别URL地址里面的中文字符，但无论是从美观上，还是从wordpress 优化的角度来看，都是非常差的。

# wordpress固定链接设置的一些参数：
## wordpress时间形式
```
1.%year% 基于文章发布的年份，比如2010；
2.%monthnum% 基于文章发布的月份，比如01；
3.%day% 基于文章发布当日，比如06；
4.%hour% 基于文章发布小时数，比如23；
5.%minute% 基于文章发布分钟数，比如43；
6.%second% 基于文章发布秒数，比如33；
7.%postname% 基于文章的postname，其值为撰写时指定的缩略名，不指定缩略名时是文章标题；
8.%post_id% 基于文章post_id，比如48；
9.%category% 基于文章分类，子分类会处理成“分类/子分类”这种形式；
10.%author% 基于文章作者名。
```

## 网上常见的几种设置方法：
```
/%year%/%monthnum%/%day%/%postname%/
/%year%/%monthnum%/%postname%/
/%year%/%monthnum%/%day%/%postname%.html
/%year%/%monthnum%/%postname%.html
/%category%/%postname%.html
/%post_id%.html
```

总结：LosesToy认为，最好的 wordpress固定链接形式是：域名/文章 名（参数为/%postname%.html）。

PS：原文作者已经说明最好参数，可本人觉得用/%post_id%.html 最简洁了。(纯属个人观点，本人菜鸟，如有什么不对的地方，还忘指正)

2013年4月17日更新：

可以使用[WordPress插件Custom Permalinks](http://wubangtu.com/custom-permalinks.html "推荐一款WordPress插件Custom Permalinks")自定义每篇文章的固定链接形式。


原文来自：http://wubangtu.com/53

参考文章：http://www.23kaiyuan.com/257.html

堆堆观点：以上是广大网友分享内容。 介于SEO的问题堆堆在用的自定义链接写法是：

<span style="color: #ff0000;">[ http://wp.duiduibox.com/]( http://wp.duiduibox.com)?p=%post_id%</span><span style="color: #0000ff;">&amp;name=%postname%&amp;category=%category%</span>

红色部分是为了站点正常访问，蓝色部分是我自己加的让链接地址显示文章名字和分类。至于有没有SEO效果.百度是这么说滴。
