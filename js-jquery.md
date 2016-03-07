title: jquery 学习
categories:
  - jquery
tags:
  - jquery
date: 2015-12-18 18:08:24
---

# jquery 嵌套选择和class多项选择

## 情景一
html文件
```
<div class="tab-content">
    <div class="tab-pane">test1</div>
    <div class="tab-pane active">test2</div>
    <div class="tab-pane">test3</div>
    <div class="tab-pane">test4</div>
</div>
```
选择test2
```
$('div.tab-content div.tab-pane.active').val() (推荐)
或者
$('div.tab-content div.tab-pane.filter('active')
```

## 情景二
如果html内容如下
```
<div class="tab-content">
    <div class="tab-pane">test1</div>
    <div class="tab-pane fad active">test5</div>
    <div class="tab-pane active">test2</div>
    <div class="tab-pane">test3</div>
    <div class="tab-pane">test4</div>
</div>
```
则<code>$('div.tab-content div.tab-pane.active').val()</code>是选不中
test2,选中的是test5。这样可以是用
```
$('div.tab-content div[class="tab-pane active"]').val()
```

## 总结
情景一JQuery在选择的时候class的值书写不要求顺序。
情景二JQuery在选择的时候class的值书写顺序不能变。
