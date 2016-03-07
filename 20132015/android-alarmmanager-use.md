title: Android  AlarmManager的使用
categories:
  - Android
date: 2014-11-22 09:13:40
tags:
  - Android
---

一、设置闹钟时Type的差别
/* 获取闹钟管理的实例 */
AlarmManager  am = (AlarmManager) getSystemService(ALARM_SERVICE);   am.setRepeating(AlarmManager.RTC_WAKEUP,selectTime,(24 * 60 * 60 * 1000), pendingIntent);

1.  AlarmManager .RTC_WAKEUP：是绝对时间，能唤醒系统，系统值为0，如果系统设置的什么时间那么它就会按照设置的时间算，它不是代表延迟时间，没有按照真实时间流逝,如果需要设置时间差则是System.currentTimeMillis()+时间差（延迟时间），System.currentTimeMillis()代表从1970.1.1到现在的毫秒，

2.AlarmManager.ELAPSED_REALTIME_WAKEUP：是相对时间，能唤醒系统，系统值为      3，如果要使用这个类型，应该调用SystemClock.elapsedRealtime()获取相对时间+设定的延迟时间

3、AlarmManager.PRC:用法和第一种一样，和第一种差别主要是这个不会唤醒系统

4、AlarmManager.ELAPSED_REALTIME :用法和第二种用法一样，和第二种差别是这个不会唤醒系统

&nbsp;

&nbsp;

&nbsp;

&nbsp;

二、Demo的实现

&nbsp;

public void setCalendar(int hourOfDay, int minute) {
// 这里时区需要设置一下，不然会有8个小时的时间差
calendar.setTimeZone(TimeZone.getTimeZone("GMT+8"));
calendar.setTimeInMillis(System.currentTimeMillis());
calendar.set(Calendar.HOUR_OF_DAY, hourOfDay);
calendar.set(Calendar.MINUTE, minute);
calendar.set(Calendar.SECOND, 0);
calendar.set(Calendar.MILLISECOND, 0);

String tmpS = format(hourOfDay) + ":"+ format(minute);
tv_time.setText(tmpS);

long systemTime = System.currentTimeMillis();
// 选择的每天定时时间
selectTime = calendar.getTimeInMillis();
// 如果当前时间大于设置的时间，那么就从第二天的设定时间开始
if(systemTime &gt; selectTime) {
//Toast.makeText(AlarmWarnActivity.this,"设置的时间小于当前时间", Toast.LENGTH_SHORT).show();
calendar.add(Calendar.DAY_OF_MONTH, 1);
selectTime = calendar.getTimeInMillis();
}
// 计算现在时间到设定时间的时间差
firstTime=selectTime - systemTime;
long days = firstTime / (1000 * 60 * 60 * 24);
long hours = (firstTime-days*(1000 * 60 * 60 * 24))/(1000* 60 * 60);
long minutes = (firstTime-days*(1000 * 60 * 60 * 24)-hours*(1000* 60 * 60))/(1000* 60)+1;
if(minutes==60){
hours=hours+1;
minutes=0;
}
String str="已将闹钟设置为距现在起";
if(days!=0){
str+=""+days+"天";
}
if(hours!=0){
str+=hours+"小时";
}
if(minutes!=0){
str+=minutes+"分";
}
if(days==0&amp;&amp;hours==0&amp;&amp;minutes==0){
str+="0分";
}
str+="后提醒。";
setAlarmAlert();
Toast.makeText(ReadBibleActivity.this, str, Toast.LENGTH_SHORT).show();

}

&nbsp;

&nbsp;

private void setAlarmAlert(){
read.date=tv_time.getText().toString();
read.name=tv_sound_path.getText().toString();
if(ring_uri==null){
ring_uri=RingtoneManager.getActualDefaultRingtoneUri(this, RingtoneManager.TYPE_ALARM);
Ringtone ringtone=RingtoneManager.getRingtone(this, ring_uri);
String title=getString(R.string.tv_no_ringtone);
if(ringtone!=null)
{
title=ringtone.getTitle(this);
}
tv_sound_path.setText(title);
}
read.path=ring_uri.toString();
read.theFirstNotifyBeginTime =selectTime;// 存储响铃时间
read.lastNotifyTime=0;
SharedPreferenceUtil.setReadBible(ReadBibleActivity.this,read);
//如果第一个参数是ELAPSED_REALTIME_WAKEUP，第二个参数就要使用SystemClock.elapsedRealtime()，如果使用RTC_WAKEUP则要使用System.currentTimeMillis() 当前系统时间
//firstTime=SystemClock.elapsedRealtime()+firstTime;

/* 建立Intent和PendingIntent，来调用目标组件 */
Intent intent = new Intent(this,AlarmReceiver.class);
intent.putExtra("activity", "readbible");
intent.setData(ring_uri);

PendingIntent pendingIntent = PendingIntent.getBroadcast(ReadBibleActivity.this, Conf.NOTIFICATION_READING_ID,intent, PendingIntent.FLAG_UPDATE_CURRENT);
AlarmManager am;
/* 获取闹钟管理的实例 */
am = (AlarmManager) getSystemService(ALARM_SERVICE);
/* 设置闹钟 */
//am.set(AlarmManager.RTC_WAKEUP,calendar.getTimeInMillis(), pendingIntent);//设置一次性闹钟
/* 设置周期闹,第2个参数指运行时要等待的时间，也就是执行延迟时间，第三个参数，表示执行的时间间隔， */
am.setRepeating(AlarmManager.RTC_WAKEUP,selectTime,(24 * 60 * 60 * 1000), pendingIntent);
}

&nbsp;

&nbsp;

三、手机重启后设定的闹钟时间会被消为0，这时需要重新设置闹钟

&lt;!-- 手机开机广播 --&gt;
&lt;receiver android:name="org.hdt.info.BootReceiver"&gt;
&lt;intent-filter&gt;
&lt;action android:name="android.intent.action.BOOT_COMPLETED" /&gt;
&lt;/intent-filter&gt;
&lt;/receiver&gt;

&nbsp;

public class BootReceiver extends BroadcastReceiver {

@Override
public void onReceive(Context context, Intent intent) {
Calendar calendar = Calendar.getInstance();
// 这里时区需要设置一下，不然会有8个小时的时间差
calendar.setTimeZone(TimeZone.getTimeZone("GMT+8"));
// 得到当前时间并设置到日历里面
calendar.setTimeInMillis(System.currentTimeMillis());
String action = intent.getAction();
if (action.equals(Intent.ACTION_BOOT_COMPLETED)) {
// 重新计算闹铃时间，读取闹钟响铃时间
ReadBible read = SharedPreferenceUtil.getReadBible(context);

String readSwitch=SharedPreferenceUtil.getReadBibleSwitch(context);

if (read != null&amp;&amp;readSwitch.equals("ok")) {

long nextNofifyTime;
if( read.theFirstNotifyBeginTime&lt;System.currentTimeMillis()){ //如果闹铃时间小于当前时间，闹铃过期
nextNofifyTime = 24 * 60 * 60 * 1000 + read.theFirstNotifyBeginTime;
}else{//闹铃还没响
nextNofifyTime=read.theFirstNotifyBeginTime;
Log.v("Log.v", "读经PPPPPPPPPPPPPPPPPPPPPP"+nextNofifyTime);
}

/* 建立Intent和PendingIntent，来调用目标组件 */
intent = new Intent(context, AlarmReceiver.class);
intent.putExtra("activity", "readbible");
Uri uri = null;
if (read.path != null) {
uri = Uri.parse(read.path);
}
intent.setData(uri);
read.theFirstNotifyBeginTime=nextNofifyTime;
read.lastNotifyTime=0;
SharedPreferenceUtil.setReadBible(context, read);
PendingIntent pendingIntent = PendingIntent.getBroadcast(context, Conf.NOTIFICATION_READING_ID, intent,PendingIntent.FLAG_UPDATE_CURRENT);
/* 获取闹钟管理的实例 */
AlarmManager am = (AlarmManager) context.getSystemService(Context.ALARM_SERVICE);
/* 设置周期闹,第2个参数指运行时要等待的时间，也就是执行延迟时间，第三个参数，表示执行的时间间隔， */
am.setRepeating(AlarmManager.RTC_WAKEUP,nextNofifyTime, (24 * 60 * 60 * 1000), pendingIntent);
}
ReadBible alarmWarn = SharedPreferenceUtil.getAlarmWarn(context);
String alarmWarnSwitch=SharedPreferenceUtil.getAlarmWarnSwitch(context);
if(alarmWarn!=null&amp;&amp;alarmWarnSwitch.equals("ok")){
long nextNofifyTime_Alarm;
if( alarmWarn.theFirstNotifyBeginTime&lt;System.currentTimeMillis()){ //如果闹铃时间小于当前时间，闹铃过期
nextNofifyTime_Alarm = 24 * 60 * 60 * 1000 + alarmWarn.theFirstNotifyBeginTime;
}else{//闹铃还没响
nextNofifyTime_Alarm=alarmWarn.theFirstNotifyBeginTime;
Log.v("Log.v", "音频PPPPPPPPPPPPPPPPPPPPPP"+nextNofifyTime_Alarm);
}
// if(nextNofifyTime&lt;=System.currentTimeMillis()){
// nextNofifyTime=System.currentTimeMillis();
// Log.v("Log.v", "读经PPPPPPPPPPPPPPPPPPPPPP");
// }
alarmWarn.theFirstNotifyBeginTime=nextNofifyTime_Alarm;
alarmWarn.lastNotifyTime=0;
SharedPreferenceUtil.setAlarmWarn(context, alarmWarn);
//nextNofifyTime = SystemClock.elapsedRealtime() + nextNofifyTime;
/* 建立Intent和PendingIntent，来调用目标组件 */
LocalVideo video=new LocalVideo();
video.name=alarmWarn.name;
video.savePath=alarmWarn.path;
Intent intent_alarm = new Intent(context,AlarmReceiver.class);
intent_alarm.putExtra("activity", "audioplayer");
intent_alarm.putExtra("URL", video);
PendingIntent pendingIntent = PendingIntent.getBroadcast(context, Conf.NOTIFICATION_AUDIO_ID, intent_alarm,PendingIntent.FLAG_UPDATE_CURRENT);
/* 获取闹钟管理的实例 */
AlarmManager am = (AlarmManager) context.getSystemService(Context.ALARM_SERVICE);
/* 设置周期闹,第2个参数指运行时要等待的时间，也就是执行时间，第三个参数，表示执行的时间间隔， */
am.setRepeating(AlarmManager.RTC_WAKEUP,nextNofifyTime_Alarm, (24 * 60 * 60 * 1000), pendingIntent);
}
}

}