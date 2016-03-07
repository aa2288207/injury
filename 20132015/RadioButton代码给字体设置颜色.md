title: RadioButton代码给字体设置颜色
categories:
  - Android
date: 2014-11-07 02:35:50
tags:
  - Android
---

开发中避免不了用代码实现自定义RadioButton，但是用常规的直接setColor却是不行，然而

for (int i = 0; i &lt; menus.length; i++) {
RadioButton rbMenu = new RadioButton(this);

ColorStateList colors=getResources().getColorStateList(R.color.radio_font_color);
rbMenu.setTextColor(colors);

&nbsp;

用ColorStateList可以实现，^_^