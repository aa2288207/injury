title: Android控件之RelativeLayout控件属性
categories:
  - Android
date: 2013-09-12 13:02:59
tags:
  - Android
---

layout_alignParentBottom=ture/false    当前控件低端与父控件的低端对齐(重合）

layout_alignParentLeft=true/false        当前控件左端与父控件的左端对齐(重合）

layout_alignParentRight=ture/false      当前控件右端与父控件的右端对齐(重合）

layout_alignParentTop=true/false        当前控件上端与父控件的上端对齐(重合）

layout_centerHorizontal  =true/false    当前控件位于父控件的横向中间位置（水平方向上的中间）  //针对RelativeLayout里面的子控件

android:gravity="center_horizontal"    针对RelativeLayout控件位置

layout_centerInParent=true/false        当前控件位于父控件的纵横向中间位置（垂直方向上的中间）

layout_above             使当前控件位于给出id控件的上方

layout_below             使当前控件位于给出id控件的下方

layout_toLeftOf          使当前控件位于给出id控件的左侧

layout_toRightOf        使当前控件位于给出id控件的右侧

layout_alignBottom     使当前控件与给出id控件的底部部重合**(注意可用和给出id控件来对齐）**

layout_alignLeft          使当前控件与给出id控件的左边重合

layout_alignRight        使当前控件与给出id控件的右边重合

layout_alignTop          使当前控件与给出id控件的顶部重合

layout_alignBaseline    使当前控件的BaseLine与给出id控件t的BaseLine重合，这个主要用于Label或者其他包含文本的widgets。