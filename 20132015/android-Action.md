title: Android之Action返回结果
categories:
  - Android
date: 2013-11-13 06:42:49
tags:
  - Android
---

第一个页面：

class addFiledButtonListener implements OnClickListener {

@Override
public void onClick(View v) {
// TODO Auto-generated method stub
// 如果是向两个action跳转时，不需要说明跳转action，只需要finish会回到进来的页面
Intent intent = new Intent();
// 设置返回结果
AddFieldActivity.this.setResult(RESULT_OK, intent);
// 结束当前Activity
AddFieldActivity.this.finish();
}
}

/*
* 接受Action返回的结果
*
* @param requestCode 启动新Activity时的带过去的requestCode值
*
* @param resultCode为回传的标记，子页面中回传的是RESULT_OK
*/
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
// 从Itent中获得Bundle
if (requestCode == GET_CODE) {
if (resultCode == RESULT_OK) {
Bundle b = data.getExtras();
// 获取返回的结果，处理结果数据

}
}
}
第二个页面：

class ItemClickListener implements OnItemClickListener {

@Override
public void onItemClick(AdapterView&lt;?&gt; parent, View view,
final int position, long id) {
Map&lt;String, String&gt; item = (HashMap&lt;String, String&gt;) parent
.getItemAtPosition(position);

Intent intent = new Intent();
String name = item.get("name").toString();
intent.putExtra("name", name);
/* 将数据打包到intent Bundle 的过程略,设置返回结果 */
FertilizerListActivity.this.setResult(RESULT_OK, intent);// 这理有2个参数(int
// resultCode,
// Intent
// intent),第一个参数是返回值的标志
// 结束当前Activity
FertilizerListActivity.this.finish();

}
}

&nbsp;