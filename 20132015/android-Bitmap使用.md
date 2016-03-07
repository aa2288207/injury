title: Android 开发之Bitmap使用
categories:
  - Android
date: 2013-10-17 14:13:20
tags:
  - Android
---

pop的showPopup弹出的内容怎么设置

LayoutInflater inflater= (LayoutInflater)mContext.getSystemService(Context.LAYOUT_INFLATER_SERVICE);

View   viewCache = (View) inflater.inflate(R.layout.custom_text_view,null);

LinearLayout layout=(LinearLayout)viewCache.findViewById(R.id.linear_poipopup);  //新创建一个页面

Bitmap bitmasps=BMapUtil.getBitmapFromView(layout);

pop.showPopup(bitmasps,mCurItem.getPoint(),32);//最后一个参数弹窗在y轴上的偏移量,取值范围yOffset&gt;=0。单位：像素

&nbsp;

怎么读取Assets文件下的图片

Bitmap[] bitMaps=new Bitmap[3];

Bitmap[] bitMaps={

Drawable mark =this.mContext.getResources().getDrawable(R.drawable.popup_bg);

bitMaps[2]=BMapUtil.getImageFromAssetsFile(mContext, "marker3.png");

}

也可以这样写：（不指定Bitmap数组长度）

Bitmap[] bitMaps={
// BMapUtil.getBitmapFromView(popupLeft),
//BMapUtil.getBitmapFromView(popupText),
BMapUtil.getBitmapFromView(layout)
// BMapUtil.getBitmapFromView(popupText),
// BMapUtil.getBitmapFromView(btnImage)
};

/**
* 读取Assets文件夹中的图片资源
* @param context
* @param fileName 图片名称
* @return
*/
public static Bitmap getImageFromAssetsFile(Context context,String fileName)
{
Bitmap image=null;
AssetManager am=context.getResources().getAssets();
try
{
InputStream is=am.open(fileName);
image=BitmapFactory.decodeStream(is);
is.close();
}
catch(IOException e)
{
e.printStackTrace();
}
return image;
}