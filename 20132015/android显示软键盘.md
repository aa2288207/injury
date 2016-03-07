title: android中隐藏以及显示软键盘代码
categories:
  - Android
date: 2014-07-03 06:26:51
tags:
  - Android
---

代码控制软键盘：

// 隐藏软键盘
((InputMethodManager) getSystemService(INPUT_METHOD_SERVICE)).hideSoftInputFromWindow(SearchActivity.this.getCurrentFocus().getWindowToken(),InputMethodManager.HIDE_NOT_ALWAYS);

&nbsp;

//显示软键盘,

<span style="color: #3b3b3b;">控件ID可以是EditText,TextView ((InputMethodManager)getSystemService(INPUT_METHOD_SERVICE)).showSoftInput(控件ID, 0);   </span>