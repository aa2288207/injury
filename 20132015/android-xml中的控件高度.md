title: Android 获取xml中的控件高度
categories:
  - Android
date: 2015-02-27 08:13:48
tags:
  - Android
---

**注：以下代码不能在onCreate里面使用，否则获取状态栏高度为0**

<div class="tools">Rect frame = <span class="keyword">new</span> Rect();</div>

getWindow().getDecorView().getWindowVisibleDisplayFrame(frame);

<span class="keyword">int</span> statusBarHeight = frame.top;

——————————————————————————————————————————————————

**可以直接在OnCreate中调用**

<pre lang="java">
public int getStatusHeight() {
        int statusHeight = 0;
        Rect localRect = new Rect();
        getWindow().getDecorView().getWindowVisibleDisplayFrame(localRect);
        statusHeight = localRect.top;
        if (0 == statusHeight) {
            Class<?> localClass;
            try {
                localClass = Class.forName("com.android.internal.R$dimen");
                Object localObject = localClass.newInstance();
                int i5 = Integer.parseInt(localClass
                        .getField("status_bar_height").get(localObject)
                        .toString());
                statusHeight = getResources().getDimensionPixelSize(i5);
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            } catch (InstantiationException e) {
                e.printStackTrace();
            } catch (NumberFormatException e) {
                e.printStackTrace();
            } catch (IllegalArgumentException e) {
                e.printStackTrace();
            } catch (SecurityException e) {
                e.printStackTrace();
            } catch (NoSuchFieldException e) {
                e.printStackTrace();
            }
        }
        return statusHeight;
    }
</pre>

或者
<pre>
这种方式也可以获取状态栏高度：

     /** 
     * 获取状态栏高度 
     *  
     * @return 
     */  
    public int getStatusBarHeight()  
    {  
        Class<?> c = null;  
        Object obj = null;  
        java.lang.reflect.Field field = null;  
        int x = 0;  
        int statusBarHeight = 0;  
        try  
        {  
            c = Class.forName("com.android.internal.R$dimen");  
            obj = c.newInstance();  
            field = c.getField("status_bar_height");  
            x = Integer.parseInt(field.get(obj).toString());  
            statusBarHeight = getResources().getDimensionPixelSize(x);  
            return statusBarHeight;  
        }  
        catch (Exception e)  
        {  
            e.printStackTrace();  
        }  
        return statusBarHeight;  
    }
</pre>

<pre lang="java">
<span class="keyword">private</span> <span class="keyword">void</span> init(){

Rect rect = <span class="keyword">new</span> Rect();

Window window = getWindow();

tv.getWindowVisibleDisplayFrame(rect);

<span class="comment">// 状态栏的高度</span>

<span class="keyword">int</span> statusBarHeight = rect.top;

<span class="comment">// 标题栏跟状态栏的总体高度</span>

<span class="keyword">int</span> contentViewTop = window.findViewById(Window.ID_ANDROID_CONTENT).getTop();

<span class="comment">// 标题栏的高度：用上面的值减去状态栏的高度及为标题栏高度</span>

<span class="keyword">int</span> titleBarHeight = contentViewTop - statusBarHeight;

System.out.println(statusBarHeight+<span class="string">"..."</span>+contentViewTop+<span class="string">"..."</span>+titleBarHeight);

}
</pre>

<pre lang="java">
<span class="annotation">@Override</span>
<span class="keyword">public</span> <span class="keyword">void</span> onCreate(Bundle savedInstanceState) {
<span class="keyword">super</span>.onCreate(savedInstanceState);
setContentView(R.layout.main);

tv = (TextView) findViewById(R.id.tv);
<span class="comment">// 必须用这种方法获得。不用得到的数据为0</span>
tv.post(<span class="keyword">new</span> Runnable() {

<span class="keyword">public</span> <span class="keyword">void</span> run() {
init();

}

});

<span class="comment">// 获取控件的高度</span>

ViewTreeObserver vto = tv.getViewTreeObserver();

vto.addOnPreDrawListener(<span class="keyword">new</span> ViewTreeObserver.OnPreDrawListener() {
<span class="keyword">public</span> <span class="keyword">boolean</span> onPreDraw() {
<span class="keyword">int</span> height = tv.getMeasuredHeight();
<span class="keyword">int</span> width = tv.getMeasuredWidth();

System.out.println(height+<span class="string">",,"</span>+width);
<span class="keyword">return</span> <span class="keyword">true</span>;
}
});
}
</pre>

如果想得到在xml里面设置的布局宽高的话 可以通过

Log.i("Log",imageView.getLayoutParams().width+"--"+imageView.getLayoutParams().height);

&nbsp;

参考：http://blog.csdn.net/johnny901114/article/details/7839512