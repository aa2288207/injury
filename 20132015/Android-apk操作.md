title: Android apk操作
categories:
  - Android
date: 2014-08-18 09:59:52
tags:
  - Android
---

/**
* 判断apk是否安装过
* @param pm
* @param packageName 包名
* @param versionCode 版本号
* @return
*/
private int doType(PackageManager pm,String packageName,int versionCode)
{
List&lt;PackageInfo&gt; pakageinfos=pm.getInstalledPackages(PackageManager.GET_UNINSTALLED_PACKAGES);
for(PackageInfo info:pakageinfos){
String pi_packageName=info.packageName;
int pi_versionCode=info.versionCode;
//如果包名在系统已经安装过的应用中存在
if(packageName.endsWith(pi_packageName))
{
if(versionCode==pi_versionCode)
{
Log.i(TAG, "已经安装，不用更新，可以卸载该应用");
return INSTALLED;
}else if(versionCode&gt;pi_versionCode)
{
Log.i(TAG, "已经安装，有更新");
return INSTALLED_UPDATE;
}
}
}
Log.i(TAG, "未安装");
return UNINSTALLED;
}

&nbsp;

&nbsp;

/**
* 判断本地是否有apk 及apk是否完整
* @return
*/
private PackageInfo apkIntact() {
File apkfile = new File(Conf.APP_INSTALL, Conf.fileName);
if (apkfile.exists()) {
String name = apkfile.getName();
if (name.toLowerCase().endsWith(".apk")) {
PackageManager pm = MainActivity.this.getPackageManager();
String apk_path = apkfile.getAbsolutePath();// apk文件的绝对路劲
PackageInfo packageInfo = pm.getPackageArchiveInfo(apk_path,PackageManager.GET_ACTIVITIES);
if (packageInfo != null) {
return packageInfo;
}

}
}
return null;
}

&nbsp;

//安装本地APK
private void installApk(String noteInfo, String newVersionName)
{
AlertDialog dialog;
AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setTitle("发现新版本" + newVersionName);
builder.setMessage(noteInfo);
//弹出框显示时，拦击系统键
builder.setOnKeyListener(new DialogInterface.OnKeyListener() {

@Override
public boolean onKey(DialogInterface arg0, int keyCode,
KeyEvent arg2) {
if (keyCode == KeyEvent.KEYCODE_BACK) {
return true;
} else {
return false;
}
}
});
builder.setPositiveButton("立即升级",
new DialogInterface.OnClickListener() {
@Override
public void onClick(DialogInterface dialog, int which) {
dialog.dismiss();
File apkfile = new File(Conf.APP_INSTALL, Conf.fileName);
Toast.makeText(MainActivity.this, "开始安装", Toast.LENGTH_SHORT).show();
// 通过Intent安装APK文件
Intent i = new Intent(Intent.ACTION_VIEW);
i.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
i.setDataAndType(Uri.parse("file://" + apkfile.toString()),"application/vnd.android.package-archive");
startActivity(i);
}
});

dialog = builder.create();
dialog.setCanceledOnTouchOutside(false);
dialog.show();
}