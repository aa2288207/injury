title: Android的Notification
categories:
  - Android
date: 2014-11-10 07:55:16
tags:
  - Android
---

一、Notification 的使用

private void setNotification(Context context,Uri uri) {
Intent intent = new Intent();
String lastReader = SharedPreferenceUtil.lastReader(context);
intent.setClass(context, BibleActivity.class);
intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK| Intent.FLAG_ACTIVITY_RESET_TASK_IF_NEEDED);
//PendingIntent.FLAG_UPDATE_CURRENT:Extra会被更新为最后一个传入的Intent的Extra
PendingIntent pendingNotify = PendingIntent.getActivity(context, 0,intent,PendingIntent.FLAG_UPDATE_CURRENT);
// 第一个参数图标，第二个参数，状态栏显示的文本提示,第三个参数通知产生的时间
long when = System.currentTimeMillis();
Notification notification = new Notification(R.drawable.stat_notify_alarm, context.getString(R.string.toast_read_bible), when);
notification.setLatestEventInfo(context, context.getString(R.string.toast_read_bible), context.getString(R.string.notification_content),pendingNotify);
if(uri!=null)
notification.sound=uri;
else{
notification.defaults|=Notification.DEFAULT_SOUND; //默认铃声
}
Log.v("Log.v", ":::::::::::::::::::::::::::::::::::::::"+uri);
// String
// url=Environment.getExternalStorageDirectory().getPath()+"/hdt/video/20140810-02wuweiqing.mp3";
notification.defaults |= Notification.DEFAULT_VIBRATE;// 振动模式
// 如果想要让声音持续重复直到用户对通知做出反应，则可以在notification的flags字段增加"FLAG_INSISTENT"
notification.flags |= Notification.FLAG_ONGOING_EVENT| Notification.FLAG_AUTO_CANCEL;
notification.contentIntent = pendingNotify; // |
// Notification.FLAG_NO_CLEAR;//表明在点击了通知栏中的"清除通知"后，此通知不清除，
NotificationManager nm = (NotificationManager) context.getSystemService(Context.NOTIFICATION_SERVICE);
nm.notify(0, notification);
}

&nbsp;

二、intent.setFlags的设置

<span lang="EN-US">      </span><span lang="EN-US">//</span>使用这个标志，如果正在启动的<span lang="EN-US">Activity</span>的<span lang="EN-US">Task</span>已经在运行的话，那么，新的<span lang="EN-US">Activity</span>将不会启动；代替的，当前<span lang="EN-US">Task</span>会简单的移入前台。

<span lang="EN-US">       intent.setFlags(Intent.</span>_<span lang="EN-US">FLAG_ACTIVITY_NEW_TASK</span>_<span lang="EN-US">);</span>

三、 nm.notify(id, notification)：id 在一个app里面不能一样，要不会覆盖前面的通知栏，或不弹出通知栏，这点尤为重要

&nbsp;

&nbsp;