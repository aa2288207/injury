title: Android 调用闹钟
categories:
  - Android
date: 2014-10-27 06:31:14
tags:
  - Android
---

&nbsp;

一.创建广播

/* 建立Intent和PendingIntent，来调用目标组件 */
Intent intent = new Intent(ReadBibleActivity.this,AlarmReceiver.class);
PendingIntent pendingIntent = PendingIntent.getBroadcast(ReadBibleActivity.this, 0,intent, 0);
AlarmManager am;
/* 获取闹钟管理的实例 */
am = (AlarmManager) getSystemService(ALARM_SERVICE);
/* 设置闹钟 */
am.set(AlarmManager.RTC_WAKEUP, calendar.getTimeInMillis(), pendingIntent);
/* 设置周期闹 */
am.setRepeating(AlarmManager.RTC_WAKEUP, System.currentTimeMillis()+ (10 * 1000), (24 * 60 * 60 * 1000),pendingIntent);
String tmpS = format(hourOfDay)+ ":" + format(minute);
tv_time.setText(tmpS);

&nbsp;

二. 取消广播

Intent intent = new Intent(ReadBibleActivity.this, AlarmReceiver.class);
PendingIntent pendingIntent = PendingIntent.getBroadcast(ReadBibleActivity.this, 0, intent, 0);
AlarmManager am;
/* 获取闹钟管理的实例 */
am = (AlarmManager) getSystemService(ALARM_SERVICE);
/* 取消 */
am.cancel(pendingIntent);
Toast.makeText(ReadBibleActivity.this, "闹钟已取消！", Toast.LENGTH_SHORT).show();

三、广播的实现

&nbsp;

public class AlarmReceiver extends BroadcastReceiver {
private NotificationManager manager;
public void onReceive(Context context, Intent intent) {
Toast.makeText(context, "你设置的闹钟时间到了", Toast.LENGTH_LONG).show();

final MediaPlayer mp = new MediaPlayer();
try {
String ur=Environment.getExternalStorageDirectory().getPath()+"/hdt/video/20140810-02wuweiqing.mp3";   //如果调用默认的也要指明路径否则日志会输出异常
Uri uri=Uri.parse(ur);//RingtoneManager.getDefaultUri(RingtoneManager.TYPE_ALARM)
mp.setDataSource(context,uri);

mp.prepareAsync();   //最后使用异步，不容易堵塞主线程
// mp.setLooping(true); //是否开启循环模式
mp.setOnPreparedListener(new OnPreparedListener() {

@Override
public void onPrepared(MediaPlayer arg0) {
mp.start();
}

});

} catch (IllegalArgumentException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (SecurityException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (IllegalStateException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (Exception e) {
// TODO Auto-generated catch block
e.printStackTrace();
}
}

}