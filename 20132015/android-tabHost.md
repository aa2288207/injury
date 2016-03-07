title: Android 中tabHost详解
categories:
  - Android
date: 2014-03-23 10:35:38
tags:
  - Android
---

# 一. TabHost介绍：

TabHost组件可以在界面中存放多个选项卡, 很多软件都使用了改组件进行设计;

## 1\. TabHost常用组件

**TabWidget** : 该组件就是TabHost标签页中上部 或者 下部的按钮, 可以点击按钮切换选项卡;

**TabSpec** : 代表了选项卡界面, 添加一个TabSpec即可添加到TabHost中;

-- **创建选项卡** : newTabSpec(String tag), 创建一个选项卡;

-- **添加选项卡** : addTab(tabSpec);

&nbsp;

## 2\. TabHost使用步骤

a. **定义布局** : 在XML文件中**使用TabHost组件**, 并在其中**定义一个FrameLayout选项卡**内容;

b. **继承TabActivity** : 显示选项卡组件的Activity**继承TabActivity**;

c.** 获取组件** : 通过调用**getTabHost()方法**, 获取TabHost对象;

d. **创建添加选项卡** : 通过TabHost创建添加选项卡;

&nbsp;

## 3\. 将按钮放到下面

布局文件中TabWidget代表的就是选项卡按钮, Fragement组件代表内容;

**设置失败情况** : 如果Fragement组件没有设置 android:layout_weight属性, 那么将TabWidget放到下面, 可能不会显示按钮;

**设置权重** : 设置了Fragment组件的权重之后, 就可以成功显示该选项卡按钮;

&nbsp;

# 二. TabHost布局文件

## 1\. 根标签及id

**设置Android自带id** : XML布局文件中, 可以使用&lt;TabHost&gt; 标签设置, 其中的id 需要引用 android的自带id : android:id="@android:id/tabhost" ;

**getHost()获取前提** : 设置了该id之后, 在Activity界面可以使用 getHost(), 获取这个TabHost 视图对象;

示例 :

&lt;TabHost      android:id="@android:id/tabhost"      android:layout_width="match_parent"      android:layout_height="match_parent" &gt;

## 2\. TabWidget组件

**选项卡切换** : 该组件是选项卡切换按钮, 通过点击该组件可以切换选项卡;

**设置android自带id** : 这个组件的id要设置成android的自带id : android:id="@android:id/tabs" ;

**TabHost必备组件** : 该组件与FrameLayout组件是TabHost组件中必备的两个组件;

**切换按钮下方显示** : 如果想要将按钮放到下面, 可以将该组件定义在下面, 但是注意,**FrameLayout要设置android:layout_widget = "1"**;

**设置TabWidget大小** : 如果想要设置该按钮组件的大小, 可以设置该组件与FrameLayout组件的权重;

示例 :

&lt;TabWidget      android:id="@android:id/tabs"      android:layout_width="fill_parent"      android:layout_height="wrap_content"   android:orientation="horizontal"/&gt;

## 3\. FrameLayout组件

**组件作用** : 该组件中定义的子组件是TabHost中每个页面显示的选项卡, 可以将TabHost选项卡显示的视图定义在其中;

**设置android自带id** : 这个组件的id要设置成android的自带的id : android:id="@android:id/tabcontent" ;

示例 :

&lt;FrameLayout    android:id="@android:id/tabcontent"     android:layout_width="fill_parent"     android:layout_height="fill_parent"     android:layout_weight="1"&gt;

&nbsp;

# 二. Activity方法

&nbsp;

## 1\. 获取TabHost

**获取方法** : getHost();

**前提** : 调用getHost()方法获取TabHost组件的方法的前提是在布局文件中, 设置了android自带的id android:id="@android:id/tabhost" 才可以;

## 2\. 创建选项卡

**创建选项卡** : 调用TabHost组件的newTabHost(tag), 其中的tag是字符串, 即在**选项卡的唯一标识**;

**设置选项卡** :

-- **设置按钮名称** : setIndicator("叫兽");

-- **设置选项卡内容** : setContent(), 可以设置视图组件, 可以设置Activity, 也可以设置Fragement;

**添加选项卡** : tabHost.add(spec), 传入的参数是创建选项卡的TabSpec对象;

&nbsp;

&nbsp;

&nbsp;
<pre>**总结 - 实现Tab功能的几种方式**：
**        1.（废弃）继承自TabActivity + TabHost 布局 + Activity 内容**
                1.1：TabActivity为ActivityGroup[在版本13里被放弃]子类
                1.2：使用getTabHost() 获得TabHost 对象
                1.3：使用 newTabSpec(...).setContent(Intent) 添加Tab标签与内容

**        2.（废弃）继承自ActivityGroup + TabHost布局 + Activity 内容**
                2.1：ActivityGroup在版本13里被放弃
                2.2：使用findViewById 获得TabHost 对象
                2.3：使用setup(new LocalActivityManager(this, true))初始化
                2.4：使用 newTabSpec(...).setContent(Intent) 添加Tab标签与内容

**        3.（简单）继承自FragmentActivity + FragmentTabHost 布局 + Fragment 内容**
                3.1：使用findViewById 获得FragmentTabHost 对象
                3.2：使用setup(this, getSupportFragmentManager(), R.id.realtabcontent)初始化
                3.3：使用addTab(newTabSpec().setIndicator(),Fragment.class, null) 添加Tab标签与内容

**        4.（复杂）继承自FragmentActivity + TabHost 布局 + ViewPager布局 + Fragment 内容**
                4.1：使用findViewById 获得TabHost 对象
                4.2：使用setup()初始化
                4.3：使用TabHost.addTab(tabSpec.setContent(DummyTabFactory));添加Tab标签与**空内容**
                4.4：在TabHost.onTabChanged中控制ViewPager的实际显示
                4.5：滑动时在ViewPager.onPageSelected 中控制Tab标签的选择。
                **PS：当Tab标签数量固定且不追求和系统保持一致的标签效果，的情况下这里的TabHost布局有些多余。
                如 ：特有应用需要的Tab标签固定，且有自己的一套显示效果，那么这里完全无需TabHost布局。**

**        5.（DIY）继承自FragmentActivity + 自定义布局 + ViewPager布局 + Fragment 内容**
                5.1：自定义布局中嵌入固定Tab标签元素
                5.2：在标签元素点击事件中控制ViewPager的实际显示
                5.3：滑动时在ViewPager.onPageSelected 中控制标签元素的选择。</pre>