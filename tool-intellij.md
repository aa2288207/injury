```
Author: holdlg
Last updated: 2016-04-14 16:20:04
```

# intellij 创建java文件
<cdoe>intellij</cdoe>里面<code>new</code>没有<code>java class</code>选项
需要设置<code>File</code>-><code>Project Structure</code>-><code>Modules</code>设置你的项目的<code>Sources</code>目录，即可。

# intellij gradle 刷新更新依赖
<cdoe>intellij</cdoe>左下角黑色小方块<code>Gradle</code>有个刷新标志点一下就可以了。

# 有关intellij有表生成类的操作
[有关intellij有表生成类的操作](http://blog.csdn.net/code4j/article/details/11095451)

# eclipse 和 intellij
- eclipse默认自动编译
- intellij默认手动编译,菜单-><code>Biuld</code>-><code>make project</code> 且推荐手动编辑
- eclipse智能提示不爽
- intellij智能提示爽
- intellij可以设置自动编译菜单-><code>File</code>-><code>Setting</code>-><code>build</code>-><code>Complier</code>-><code>make project automatically</code> 后面提示<code>Running</code>和<code>Debugging</code>状态不运行，这有个dan用。
- intellij推荐自动编译增量编译插件<code>JRebel</code>本人木有用过，歪果仁的。
