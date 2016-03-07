title: Android Intent选择铃声
categories:
  - Android
date: 2014-10-28 06:48:25
tags:
  - Android
---

<span lang="EN-US" xml:lang="EN-US">1.</span>

<span lang="EN-US" xml:lang="EN-US">//onActivityResult</span>用常量

<span lang="EN-US" xml:lang="EN-US">private int RESULTCODE_CHOOSE_RING=10;</span>

<span lang="EN-US" xml:lang="EN-US">private int RESULTCODE_RECODING_VOICE=11;</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US">2.</span>

<span lang="EN-US" xml:lang="EN-US">//</span>调出文件管理器选择铃声

<span lang="EN-US" xml:lang="EN-US">Intent intent = new Intent(Intent.ACTION_GET_CONTENT);</span>

<span lang="EN-US" xml:lang="EN-US">intent.setType("audio/*");</span>

<span lang="EN-US" xml:lang="EN-US">Intent intent1=Intent.createChooser(intent, "</span>选择铃声<span lang="EN-US" xml:lang="EN-US">");</span>

<span lang="EN-US" xml:lang="EN-US">startActivityForResult(intent1, RESULTCODE_CHOOSE_RING);</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US">//</span>录音

<span lang="EN-US" xml:lang="EN-US">Intent intent = new Intent(Intent.ACTION_GET_CONTENT);</span>

<span lang="EN-US" xml:lang="EN-US">intent.setType("audio/*");</span>

<span lang="EN-US" xml:lang="EN-US">intent.setClassName("com.android.soundrecorder",</span>

<span lang="EN-US" xml:lang="EN-US">"com.android.soundrecorder.SoundRecorder");</span>

<span lang="EN-US" xml:lang="EN-US">startActivityForResult(intent, RESULTCODE_RECODING_VOICE);</span>

&nbsp;

//调用系统铃声

<span lang="EN-US" xml:lang="EN-US">   Intent intent=new Intent(RingtoneManager.ACTION_RINGTONE_PICKER);
intent.putExtra(RingtoneManager.EXTRA_RINGTONE_TYPE, RingtoneManager.TYPE_ALARM);
intent.putExtra(RingtoneManager.EXTRA_RINGTONE_TITLE, "设置闹铃铃声");
startActivityForResult(intent, AlarmButton);   <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US">3.</span>

系统铃声

&nbsp;

<span lang="EN-US" xml:lang="EN-US">@Override</span>

<span lang="EN-US" xml:lang="EN-US">protected void onActivityResult(int requestCode, int resultCode, Intent data)</span>

<span lang="EN-US" xml:lang="EN-US">{</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> // TODO Auto-generated method stub</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> super.onActivityResult(requestCode, resultCode, data);</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>返回铃声<span lang="EN-US" xml:lang="EN-US">uri</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> if(requestCode==RESULTCODE_CHOOSE_RING)</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> {</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> if(resultCode==RESULT_OK)</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> {</span>

//得到我们选择的铃声
Uri pickeduri = data.getParcelableExtra(RingtoneManager.EXTRA_RINGTONE_PICKED_URI);

}
}

<span lang="EN-US" xml:lang="EN-US">@Override</span>

<span lang="EN-US" xml:lang="EN-US">protected void onActivityResult(int requestCode, int resultCode, Intent data)</span>

<span lang="EN-US" xml:lang="EN-US">{</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> // TODO Auto-generated method stub</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> super.onActivityResult(requestCode, resultCode, data);</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>返回铃声<span lang="EN-US" xml:lang="EN-US">uri</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> if(requestCode==RESULTCODE_CHOOSE_RING)</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> {</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> if(resultCode==RESULT_OK)</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> {</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>将返回的<span lang="EN-US" xml:lang="EN-US">uri</span>转为<span lang="EN-US" xml:lang="EN-US">path</span>，方便后续利用

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> Uri uri=data.getData();</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> Cursor cursor = getContentResolver().query(uri, null, <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr />  <wbr />null, null, null);</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr />  <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>第一行第二列保存路径<span lang="EN-US" xml:lang="EN-US">strRingPath</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> cursor.moveToFirst(); <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> strRingPath = cursor.getString(1); <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> cursor.close();</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //.........</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> }</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> }</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>返回录制语音<span lang="EN-US" xml:lang="EN-US">uri</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> if(requestCode==RESULTCODE_RECODING_VOICE)</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> {</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> if(resultCode==RESULT_OK)</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> {</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>将返回的<span lang="EN-US" xml:lang="EN-US">uri</span>转为<span lang="EN-US" xml:lang="EN-US">path</span>，方便后续利用

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> Uri uri=data.getData();</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> Cursor cursor = getContentResolver().query(uri, null, <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr />  <wbr />null, null, null);</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr />  <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //</span>第一行第二列保存路径<span lang="EN-US" xml:lang="EN-US">strRingPath</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> cursor.moveToFirst(); <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> strRingPath = cursor.getString(1); <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> cursor.close();</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> //.........</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /></span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> }</span>

<span lang="EN-US" xml:lang="EN-US"> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> }</span>

<span lang="EN-US" xml:lang="EN-US">}</span>