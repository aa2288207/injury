title: Android 判断12小时还是24时间制
categories:
  - Android
date: 2014-09-12 10:09:07
tags:
  - Android
---

private boolean JudgeTime(Context context){
int hour=Calendar.getInstance().get(Calendar.HOUR_OF_DAY);
if (DateFormat.is24HourFormat(context))// 24小时制
{
return true;
}
else{
if(Calendar.getInstance().get(Calendar.AM_PM)!=0){ //AM 代表上午值是0，PM下午值是1，
return true;
}

}
return false;

}