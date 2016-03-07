title: 监听EditText完成
categories:
  - Android
date: 2015-02-26 03:52:41
tags:
  - Android
---

```
mEditTextl.setOnEditorActionListener(new onEditorActionListener() {
    @Override
    public boolean onEditorAction(TextView v， int actionId, keyEvent event) {
        Log.d(TAG, mEditText.getText().toString());
        return false;
    }
});
```
如上方法，当在你按下键盘上的“完成”键时，就会打印出此时mEditText中的内容