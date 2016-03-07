```
Author：holdlg
Last updated: 2015-12-28 10:39:04
```

# vim

 ## Common Command
  ```
  文档操作
  ggVG 全选
  d    删除所选内容
  y    复制所选内容
  dd   删除当前行
  yy   复制当前行
  p    粘贴
  gg   首行
  G    末行
  0    当前行开头
  $    当前行结尾
  10j  向下移动10行
  10l  向后移动10列
  w    下一个单词开头
  b    上一个单词开头
  e    下一个单词末尾
  ge   上一个单词末尾
  u        撤销
  ctrl+r   恢复撤销
  ctrl+s   停止输入
  ctrl+q   恢复输入
  ```

  ```
  标签页操作
  :tabe filename 用标签页打开文件 
  :tabnew filename 用标签页打开文件 
  :tab split 用标签页打开当期编辑的文件 
  :tabf filename* 用标签页打开与通配符匹配的一个文件 
  :tabs 显示所有标签页，> 指示当前页，+ 显示修改未保存 

  :tabc 关闭当前标签页，功能等同于:q 
  :tabo 关闭所有标签页 

  :tabn 跳转后一个标签页 
  :tabp 跳转前一个标签页 
  :tabfirst 跳转第一个标签页 
  :tabr 跳转第一个标签页 
  :tablast 跳转最后一个标签页 

  :tabm 0/1/2 将当前标签页移动到第1/2/3个页面位置 

  :tabdo 对多个标签页同时执行命令，如 
  :tabdo %s/aaa/bbb/g 


  gt 跳转后一个标签页 
  gT 跳转前一个标签页
  ```


 ## 插件管理器 Vundle
  - [github 链接](https://github.com/VundleVim/Vundle.vim)
  - 安装请参考github文档。如下条件为必须，请确保目录和文件存在。
   - 1. mkdir ~/.vim/bundle/
   - 2. vim ~/.vimrc
  - 帮助
  ```
  :PluginList       - lists configured plugins
  :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
  :PluginSearch foo - searches for foo; append `!` to refresh local cache
  :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
  ```


 ## YouCompleteMe 自动补全
  - [github 链接](https://github.com/Valloric/YouCompleteMe)


 ## NERDTree 目录管理
  - [github 链接](https://github.com/scrooloose/nerdtree)
  - 操作
  ```
  ctrl + w + h    光标 focus 左侧树形目录
  ctrl + w + l    光标 focus 右侧文件显示窗口
  ctrl + w + w    光标自动在左右侧窗口切换 #！！！
  ctrl + w + r    移动当前窗口的布局位置
  ```

  ```
  o       在已有窗口中打开文件、目录或书签，并跳到该窗口
  go      在已有窗口 中打开文件、目录或书签，但不跳到该窗口
  t       在新 Tab 中打开选中文件/书签，并跳到新 Tab
  T       在新 Tab 中打开选中文件/书签，但不跳到新 Tab
  i       split 一个新窗口打开选中文件，并跳到该窗口
  gi      split 一个新窗口打开选中文件，但不跳到该窗口
  s       vsplit 一个新窗口打开选中文件，并跳到该窗口
  gs      vsplit 一个新 窗口打开选中文件，但不跳到该窗口
  !       执行当前文件
  O       递归打开选中 结点下的所有目录
  x       合拢选中结点的父目录
  X       递归 合拢选中结点下的所有目录
  e       Edit the current dif

  双击    相当于 NERDTree-o
  中键    对文件相当于 NERDTree-i，对目录相当于 NERDTree-e

  D       删除当前书签

  P       跳到根结点
  p       跳到父结点
  K       跳到当前目录下同级的第一个结点
  J       跳到当前目录下同级的最后一个结点
  k       跳到当前目录下同级的前一个结点
  j       跳到当前目录下同级的后一个结点

  C       将选中目录或选中文件的父目录设为根结点
  u       将当前根结点的父目录设为根目录，并变成合拢原根结点
  U       将当前根结点的父目录设为根目录，但保持展开原根结点
  r       递归刷新选中目录
  R       递归刷新根结点
  m       显示文件系统菜单 #！！！然后根据提示进行文件的操作如新建，重命名等
  cd      将 CWD 设为选中目录

  I       切换是否显示隐藏文件
  f       切换是否使用文件过滤器
  F       切换是否显示文件
  B       切换是否显示书签

  q       关闭 NerdTree 窗口
  ?       切换是否显示 Quick Help
  ```

  ```
  :tabnew [++opt选项] ［＋cmd］ 文件      建立对指定文件新的tab
  :tabc   关闭当前的 tab
  :tabo   关闭所有其他的 tab
  :tabs   查看所有打开的 tab
  :tabp   前一个 tab
  :tabn   后一个 tab

  标准模式下：
  gT      前一个 tab
  gt      后一个 tab

  MacVim 还可以借助快捷键来完成 tab 的关闭、切换
  cmd+w   关闭当前的 tab
  cmd+{   前一个 tab
  cmd+}   后一个 tab
  ```

  ```
  自定义选项
  loaded_nerd_tree            不使用NerdTree脚本
  NERDChristmasTree           让Tree把自己给装饰得多姿多彩漂亮点
  NERDTreeAutoCenter          控制当光标移动超过一定距离时，是否自动将焦点调整到屏中心
  NERDTreeAutoCenterThreshold 与NERDTreeAutoCenter配合使用
  NERDTreeCaseSensitiveSort   排序时是否大小写敏感
  NERDTreeChDirMode           确定是否改变Vim的CWD
  NERDTreeHighlightCursorline 是否高亮显示光标所在行
  NERDTreeHijackNetrw         是否使用:edit命令时打开第二NerdTree
  NERDTreeIgnore              默认的“无视”文件
  NERDTreeBookmarksFile       指定书签文件
  NERDTreeMouseMode           指定鼠标模式（1.双击打开；2.单目录双文件；3.单击打开）
  NERDTreeQuitOnOpen          打开文件后是否关闭NerdTree窗口
  NERDTreeShowBookmarks       是否默认显示书签列表
  NERDTreeShowFiles           是否默认显示文件
  NERDTreeShowHidden          是否默认显示隐藏文件
  NERDTreeShowLineNumbers     是否默认显示行号
  NERDTreeSortOrder           排序规则
  NERDTreeStatusline          窗口状态栏
  NERDTreeWinPos              窗口位置（'left' or 'right'）
  NERDTreeWinSize             窗口宽

  使用方法：$ vim ~/.vimrc

  let NERDTreeIgnore = ['\.pyc$']
  let NERDChristmasTree=1
  let NERDTreeAutoCenter=1
  let NERDTreeMouseMode=2
  let NERDTreeShowBookmarks=1
  let NERDTreeShowFiles=1
  let NERDTreeShowHidden=1
  let NERDTreeShowLineNumbers=1
  let NERDTreeWinPos='left'
  let NERDTreeWinSize=31
  nnoremap f :NERDTreeToggle
  ```

## vimrc
  ```
  " Vim Configure Start
  colorscheme Tomorrow-Night-Bright  " 设置主题方案
  set number          " 显示行号
  set cursorline      " 突出显示当前行
  set tabstop=4       " 设置tab键的宽度
  syn on              " 打开语法高亮
  set showmatch       " 设置匹配模式，类似当输入一个左括号时会匹配相应的那个右括号
  set smartindent     " 智能对齐方式
  set shiftwidth=4    " 换行时行间交错使用4个空格
  set autoindent      " 自动对齐
  set ai!             " 设置自动缩进
  set guifont=Courier_new:h14:b:cDEFAULT " 设置字体和大小
  " Vim Configure End


  " Plugin nerdtree Configure Start
  let NERDTreeIgnore = ['\.pyc$']
  let NERDChristmasTree=1
  let NERDTreeAutoCenter=1
  let NERDTreeMouseMode=2
  let NERDTreeShowBookmarks=1
  let NERDTreeShowFiles=1
  let NERDTreeShowHidden=1
  let NERDTreeShowLineNumbers=1
  let NERDTreeWinPos='left'
  let NERDTreeWinSize=31
  nnoremap f :NERDTreeToggle
  " Plugin nerdtree Configure End

  " Vundle Configure Start
  set nocompatible              " be iMproved, required
  filetype off                  " required
  set rtp+=~/.vim/bundle/Vundle.vim

  call vundle#begin()
  Plugin 'VundleVim/Vundle.vim'
  Plugin 'scrooloose/nerdtree'
  Plugin 'Valloric/YouCompleteMe'
  call vundle#end()            " required

  filetype plugin indent on    " required
  " Vundle Configure End
  ```
