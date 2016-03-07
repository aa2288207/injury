title: windows phone 中弹出提示框
categories:
  - WP8
date: 2013-07-17 11:05:56
tags:
  - WP8
---

```
if (MessageBoxResult.OK != 
        MessageBox.Show("确定要退出吗？", "温馨提示", MessageBoxButton.OKCancel))
    {
    e.Cancel = true;
    }
```