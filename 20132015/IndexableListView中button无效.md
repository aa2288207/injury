title: IndexableListView 中button无效
categories:
  - Android
date: 2014-07-25 07:31:54
tags:
  - Android
---

<div>这是一个网上的开源项目，用来设置索引，用来实现向微信通讯录的那种列表，用了之后发现listView中的button点击无效，原来是下面几行代码再做鬼</div>
<div>注释掉</div>
<div>// @Override</div>
<div>// public boolean onInterceptTouchEvent(MotionEvent ev) {</div>
<div>// return true;</div>
<div>// }</div>