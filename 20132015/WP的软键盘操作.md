title: WP的软键盘操作
categories:
  - WP8
date: 2013-06-20 15:55:49
tags:
  - WP8
---

前台UI：
<pre>
<phone:PhoneApplicationPage
<Grid x:Name="LayoutRoot" Background="Transparent">
<StackPanel Orientation="Vertical">
<!--SIP 包含数字和小数点，按住句号键可以显示“.,-”-->
<TextBox InputScope="Number" />
<!--SIP 按“123”键切换到电话号码键盘，按住句号键可以显示“.,-”-->
<TextBox InputScope="NameOrPhoneNumber" />
<!--SIP 默认显示数字和符号键盘-->
<TextBox InputScope="CurrencyChinese" />
<!--SIP 显示电话拨号键盘-->
<TextBox>
<TextBox.InputScope>
<InputScope>
<InputScopeName NameValue="TelephoneNumber" />
</InputScope>
</TextBox.InputScope>
</TextBox>
<!--后台将此 TextBox 的 InputScope 设置为“EmailUserName”-->
<!--SIP 包括 @ 和 .com 键，按住 .com 键可以显示“.org .com .edu .net”-->
<TextBox Name="textBox" KeyDown="textBox_KeyDown" />
</StackPanel>
</Grid>
</phone:PhoneApplicationPage>

后台：
//获取软键盘上面的搜索键，也就是在此判断搜索的结果
private void textBox_KeyDown(object sender, KeyEventArgs e)
{
// 判断用户是否按下了 SIP 上的回车键
if (e.Key == Key.Enter)
{
MessageBox.Show("用户按下了回车键");
// 转移焦点，虚拟键盘会自动隐藏
this.Focus();
}
}
}Input scopes</pre>
![Keyboard 4](http://i.msdn.microsoft.com/dynimg/IC530993.png "Keyboard 4")
描述：Includes auto-correction, suggestions, and emoticons.
**Input scopes：**Text
![Keyboard 1](http://i.msdn.microsoft.com/dynimg/IC530994.png "Keyboard 1")
描述：The default keyboard
**Input scopes：**
AddressCity, AddressCountryName,AddressCountryShortName, AddressStateOrProvince,AddressStreet*, AlphanumericFullWidth,AlphanumericHalfWidth, Bopomofo, DateDayName,DateMonthName, Default, FileName, FullFilePath, Hanja,Hiragana, KatakanaFullWidth, KatakanaHalfWidth,LogOnName, OneChar, Password, PersonalFullName,PersonalGivenName, PersonalMiddleName,PersonalNamePrefix, PersonalNameSuffix, Yomi*AddressStreet produces this keyboard when the keyboard language on the phone or emulator is set to any language other than English, French, Filipino, Malay, or Indonesian.
![Keyboard 6](http://i.msdn.microsoft.com/dynimg/IC530995.png "Keyboard 6")
描述：
Includes the @ and .comkeys. Press and hold the.com key to display additional options (.org .com .edu .net).
**Input scopes：**EmailNameOrAddress, EmailSmtpAddress, EmailUserName
![Keyboard 10](http://i.msdn.microsoft.com/dynimg/IC530996.png "Keyboard 10")
描述：
Includes the .com key. Press and hold the .comkey to display additional options (.com .org .edu .net). Press and hold the period key to display additional options (- + &amp; " : . /).
**Input scopes：**Url
![Keyboard 8](http://i.msdn.microsoft.com/dynimg/IC530997.png "Keyboard 8")
描述：
Press the 123 key to change to the telephone number keyboard. Press and hold the period key to display additional options (- _ , .).
**Input scopes：**NameOrPhoneNumber
![Keyboard 2](http://i.msdn.microsoft.com/dynimg/IC530998.png "Keyboard 2")
描述：Contains numbers and symbols.
**Input scopes：**
AddressStreet*, CurrencyAmountAndSymbol,CurrencyChinese, PostalAddress, PostalCode, Time*AddressStreet produces this keyboard when the keyboard language on the phone or emulator is set to English, French, Filipino, Malay, or Indonesian.
![Keyboard 9](http://i.msdn.microsoft.com/dynimg/IC530999.png "Keyboard 9")
描述：
Mimics the telephone keypad. Press and hold the period key to display additional options (, ( ) X .). Press and hold the 0 key to enter +.
**Input scopes：**
TelephoneAreaCode, TelephoneCountryCode,TelephoneLocalNumber, TelephoneNumber
![Keyboard 5](http://i.msdn.microsoft.com/dynimg/IC531000.png "Keyboard 5")
描述：Contains numbers and a decimal point. Press and hold the period key to display additional options (. , -).
**Input scopes：**
CurrencyAmount, DateDay, DateMonth, DateYear, Digits,Number, NumberFullWidth, NumericPassword, TimeHour,TimeMinorSec
![Keyboard 7](http://i.msdn.microsoft.com/dynimg/IC531001.png "Keyboard 7")
描述：Includes suggestions.
**Input scopes：**Maps, Search
![Keyboard 3](http://i.msdn.microsoft.com/dynimg/IC531002.png "Keyboard 3")
描述：
Includes suggestions. Press and hold the equal key for additional options ( ( = ) : < > ). Press the&amp;123 key to change to the number and symbol keyboard, optimized for entering numeric formulas.
**Input scopes：**Formula
![Keyboard 4](http://i.msdn.microsoft.com/dynimg/IC530993.png "Keyboard 4")
描述：Includes suggestions and emoticons, but not auto-correction.
**Input scopes：**Chat
<div>**END：**</div>
<div>![Important note](http://i.msdn.microsoft.com/areas/global/content/clear.gif "Important note")**Important Note:**
The following Input scopes are not supported in Windows Phone applications: ApplicationEnd, EnumString, PhraseList, Private,RegularExpression, Srgs, Xml.</div>
<table>
<tbody>
<tr>
<th>Keyboard</th>
<th>Notes</th>
</tr>
</tbody>
</table>