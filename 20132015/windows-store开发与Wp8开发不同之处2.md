title: windows store开发与Wp8开发不同之处2
categories:
  - WP8
date: 2013-05-23 18:26:31
tags:
  - WP8
---

**1\. Win8****中如何从照相机或图库获取****WriteableBitmap****类型的图像**
这是我在移植中遇到的第一个问题。因为Hello! Papercut应用中对图像的操作非常多，可处理的图像类型，当然要用WriteableBitmap了。还有一种图像类型：BitmapImage，它和WriteableBitmap类型在WP7中相处非常友好，可以按照如下操作方便地将BitmapImage类型的图像转化为WriteableBitmap类型：
**【****WP7****】**
**必要的引用集：**
using System.Windows.Media;
using System.Windows.Media.Imaging;
**代码实现：**
BitmapImage bmpImg;
WriteableBitmap wbImg;
wbImg = new WriteableBitmap(bmpImg);
走进Win8的世界，却发现BitmapImage通向WriteableBitmap的桥梁断了，上述转化操作无法再用，原因是Win8中的WriteableBitmap()不再有1个参数的构造函数，只有一个WriteableBitmap(int width, int height)了！我不清楚微软如此改变的初衷是什么，但是对使用者而言，这无异于Windows 8电脑操作系统中没有了“开始”按钮，总让人觉得少了些什么。

这个看似微小的改变却带来了大问题：当我需要通过照相机或相册获取图像且无法提前预知图像大小的时候，我无法获得WriteableBitmap类型的图像进行后续处理了！原因都在于这个仅存的鸡肋又无趣的构造函数：WriteableBitmap(int width, int height).

查阅了大量的技术博文和微软官网提供的代码资料后发现：他们的内容居然都非常非常巧妙的避开了我遇到的这个问题，要么只是获取BitmapImage的图像就停止，不再对它进行后续处理，要么就是按照存放对应图像容器控件的固定大小初始化WriteableBitmap的图像

摸索出了一种又简单又傻瓜的解决方案：先获取BitmapImage类型的图像bmpImg（因为只需要BitmapImage bmpImg = new BitmapImage()即可完成对bmpImg存储空间的初始化，后续不存在图像大小不匹配的问题），再通过构造函数WriteableBitmap(int width, int height)完成WriteableBitmap图像的获取。是的，你猜对了，括号中的两个参数，分别就是已经获取的bmpImg图像的width和height了。下面贴一段示例代码吧，它完成的功能是：调用照相机拍照，并把得到的WriteableBitmap类型的图像在图像控件image1中进行显示，等待后续处理

**【Win8】**
**必要的引用集：**
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Media.Imaging; //图像类型相关
using Windows.Media.Capture; //调用照相机相关
using Windows.Storage; //文件操作相关
using Windows.Storage.Streams;
**代码实现：**
//注意，下面的函数是“按钮”控件的点击事件，“点击”操作触发该函数调用
private async void btnShot_Click(object sender, RoutedEventArgs e) //留意async关键字，这个不懂的话去问度娘
{

WriteableBitmap srcImage;
CameraCaptureUI cct = new CameraCaptureUI();
cct.PhotoSettings.Format = CameraCaptureUIPhotoFormat.Png; //set the format of image
StorageFile file = await cct.CaptureFileAsync(CameraCaptureUIMode.Photo);
if (file != null)
{
BitmapImage bmpImg = new BitmapImage();
using (IRandomAccessStream fileStream = await file.OpenAsync(FileAccessMode.Read))
{
bmpImg.SetSource(fileStream); // 获取bmpImg
srcImage = new WriteableBitmap(bmpImg.PixelWidth, bmpImg.PixelHeight); //根据获取到的bmpImg初始化WriteableBitmap类型
}

using (IRandomAccessStream wbFileStream = await file.OpenAsync(FileAccessMode.Read))
{
srcImage.SetSource(wbFileStream); //成功无误差拿到srcImage
}
image1.Source = srcImage; //在image1控件显示。

//接着调用你伟大的算法去处理srcImage吧！

}

从图库获取WriteableBitmap的思路同上，不一样的只是对图库的操作，简单贴一下代码：

**【Win8】**
**必要的引用集：**
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Media.Imaging; //图像类型相关
using Windows.Storage; //文件操作相关
using Windows.Storage.Streams;
using Windows.Storage.Pickers; //文件选择器
using Windows.Storage.FileProperties;
**代码实现：**
private async void btnGallery_Click(object sender, RoutedEventArgs e)
{

FileOpenPicker picker = new FileOpenPicker();
picker.SuggestedStartLocation = PickerLocationId.PicturesLibrary;
picker.FileTypeFilter.Add(".png"); //可选的文件后缀设置
picker.FileTypeFilter.Add(".jpeg");
picker.FileTypeFilter.Add(".jpg");

StorageFile file = await picker.PickSingleFileAsync();
BitmapImage bmpImg = new BitmapImage();
if (file != null)
{
//同btnShot_Click()方法
}
}

**2\. Win8****应用中背景音乐的实现**
不得不说，这个问题当初也困扰了我良久。记得在**WP7**版本中，实现应用的背景音乐并不难，因为可以通过使用相关的类（非“控件”类）和对应的方法完成这个任务。为了实现背景音乐能在整个应用运行期间都有效，即：不会随着页面的跳转而停止，我把相关的变量声明放在了App.xaml.cs中，具体的实现放在了MainPage.xaml.cs的构造函数中。在此简单贴一下代码：
**【WP7】**
**必要的引用集：**
using System.Windows.Resources;
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Audio;
**代码实现：**
**//App.xaml.cs****中的声明**
public static Stream stream = null;
public static StreamResourceInfo info;
public static SoundEffect sound;
public static SoundEffectInstance soundInstance;
**//MainPage.xaml.cs****中在构造函数****public MainPage()****中的实现**
//…………………………我的音乐文件sound.wav放在了sound文件夹中
App.info = Application.GetResourceStream(new Uri("sound/sound.wav", UriKind.Relative));
if (App.info != null)
{
App.stream = App.info.Stream;
}
App.sound = SoundEffect.FromStream(App.stream); //创建音频播放实例
App.soundInstance = App.sound.CreateInstance();
App.soundInstance.IsLooped = true; //设置循环播放
App.soundInstance.Play(); //启动播放
//…………………………
但是在**Win8**中，想要重现背景音乐的时候却让我犯了难。一是因为Win8中不再可以引用性能优良的XNA程序集，不再可以调用所提供的友好的方法；二是几乎网上所有的示例，包括微软官网提供的例子都是通过在当前页面添加一个声音控件MediaElement来完成的，这个方法简直糟糕透了，因为页面一跳转，音乐也戛然而止，这是无法忍受的，而谁又能保证一个好玩的应用从头到尾就只有一个页面呢？

网上搜寻无果，必须自己解决了。迷茫的时候我突然意识到一个问题：一般情况下使用控件，都是拖拽到当前设计的页面中，再去实现某个方法事件，比如“点击”，“触控”……用代码实现控件的使用却被我，相信也是被大多数开发者忽略了。灵光一现，顿时敲出了如下代码：

**【Win8】**
**必要的引用集：**
using Windows.UI.Xaml.Media;
using Windows.Storage;
using Windows.Storage.Streams;
**代码实现：**
**//App.xaml.cs****中的变量声明以及在****public App()****构造函数中的实现**
public static MediaElement myMediaElement = new MediaElement(); //依然采用MediaElement
public static IRandomAccessStream soundStream = null;
public App()
{
//…………………………
myMediaElement.AudioCategory = AudioCategory.BackgroundCapableMedia;
myMediaElement.IsLooping = true; //循环播放开启
}

**//MainPage.xaml.cs****中在****ApplicationPage_Loaded(object sender, RoutedEventArgs e)****方法里实现，这个方法如不懂，可以问谷哥****.**
private async void ApplicationPage_Loaded(object sender, RoutedEventArgs e)
{
if (App.soundStream == null)
{
string fileLocation = "ms-appx:///sound/";
string filename = "sound.wav"; //音乐文件sound.wav同样在sound文件夹中
var fs = RandomAccessStreamReference.CreateFromUri(new Uri(fileLocation + filename));
App.soundStream = await fs.OpenReadAsync();
App.myMediaElement.SetSource(App.soundStream, ""); //这里已经开始播放了
//如要控制“播放”与“停止”，可以如下进行：
//App.myMediaElement.Play(); //播放
//App.myMediaElement.Stop(); //停止
}
}

这就完美实现了整个应用程序可以不间断循环播放背景音乐。肿么样，看到这里是不是觉得也特别简单？其实就是思维的一个小小的转变，我们无法为App.xaml设计页面，但是可以通过代码完成对MediaElement控件的使用；虽然“拖拽”控件的方式令人青睐，但是用“代码”这种最原始的方式却可以解决通过“拖拽”无法办到的事情！“不忘初心，方能始终”也是这个道理吧！
**3\. Win8保存图像**
现在依然能够清楚的记得当初因为这个问题所做过的尝试，几乎不下10种。因为WP7中保存图像的过程实在是太简单太简单了，有了XNA的帮助，一个函数搞定！代码如下：
**【WP7】**
**必要的引用集：**
using System.Windows.Media;
using System.Windows.Media.Imaging;
using Microsoft.Xna.Framework.Media;
using System.IO;
using System.IO.IsolatedStorage; //独立存储相关
**代码简贴（保存图像到独立存储根目录下）：**
using (var store = IsolatedStorageFile.GetUserStoreForApplication())
{
string fileName = “test.jpg”;
IsolatedStorageFileStream fs = store.CreateFile(fileName);
Extensions.SaveJpeg(bmpImg, fs, bmpImg.PixelWidth, bmpImg.PixelHeight, 0, 100);
fs.Close();
}

注意：上面的Extensions.SaveJpeg函数中的bmpImg是你想要保存的WriteableBitmap类型的图像。

WP7里保存图像是不是简单疯了？不要高兴的太早，在Win8中，这一切都变了……

没有了XNA的支持，保存图像真的烦的让人吐血。我曾尝试了将近10种通过不同流之间进行转化来完成图像信息的保存，很不幸的是所有的尝试都以保存的图片无法正常打开告终……贴一下曾经做过的那些努力吧，如果你正在尝试这么做，那么恭喜你，这些路子真心都行不通的。

&nbsp;

**【Win8】**

**必要的引用集：**

using Windows.UI.Xaml.Media;

using Windows.UI.Xaml.Media.Imaging;

using Windows.Storage;

using Windows.Storage.Streams;

using Windows.Graphics.Imaging;

using Windows.Graphics.Display;

**代码实现：**

string fileName = “test.jpg”;

folder = await ApplicationData.Current.LocalFolder.GetFolderAsync(folderName);

//上面的folderName是独立存储中的某个文件夹，自己设定

StorageFile outputFile = await folder.CreateFileAsync(fileName, CreationCollisionOption.ReplaceExisting); //新建文件fileName

//以下是对待保存图像进行编码并存在独立存储的指定文件夹中

IRandomAccessStream stream = await outputFile.OpenAsync(FileAccessMode.ReadWrite);

BitmapEncoder encoder = await BitmapEncoder.CreateAsync(BitmapEncoder.PngEncoderId, stream);

Stream pixelStream = toBeStored.PixelBuffer.AsStream(); // toBeStored是欲保存的WriteableBitmap类型的图像，在本段代码之前生成的

byte[] pixels = new byte[pixelStream.Length];

pixelStream.Read(pixels, 0, pixels.Length);

encoder.SetPixelData(BitmapPixelFormat.Bgra8, BitmapAlphaMode.Straight, (uint)papercut_back.PixelWidth, (uint)papercut_back.PixelHeight, 96.0, 96.0, pixels);

await encoder.FlushAsync();

**4\. Win8****保存图像****Win8****数据绑定中，如何从独立存储中动态获取数据**

先贴一个数据绑定的例子，是在DevDiv社区看到的，当时觉着这个例子视觉效果非常好，就想要应用到Win8的Hello! Papercut中了。原文在[点击这里](http://www.devdiv.com/Windows_8_Metro_App%E5%BC%80%E5%8F%91_38_FlipView%E6%8E%A7%E4%BB%B6%E7%9A%84%E4%BB%8B%E7%BB%8D%E5%92%8C%E4%BD%BF%E7%94%A8-thread-147222-1-1.html)

&nbsp;

这个例子涉及到的东西偏多，既有数据绑定的内容，又有用户体验很好的FlipView控件的使用。直接从DevDiv上拿来图展示一下效果，这个控件的效果是不是真的很棒呢！

![](http://bcs.duapp.com/myabby/201305%2Foriginal_kRu1_51cb000019e41191.jpg)

可惜的是，上面图中这些照片，原作者采用的是静态绑定的方式，也就是假设这些要显示的图不会再有变动了。但是在实际的应用中，如果想跟进用户对软件的使用情况，从数据库或动态变化的独立存储文件夹中获取图像才是靠谱的做法。

原作者的实现框架如下：

假设上图所示的页面文件是FlipView.xaml，对应的源代码文件自然就是FlipView.xaml.cs了。首先要在FlipView.xaml中声明数据源，如是声明：

![](http://bcs.duapp.com/myabby/201305%2Foriginal_4ZAF_4a4e000056ae118f.jpg)

而对应的数据资源（即上图中显示的图片）是在另外一个类文件MainPageViewModel.cs中存放的，而对应的类名则与上图中的“MainPageViewModel”一致。具体代码如下图所示：

![](http://bcs.duapp.com/myabby/201305%2Foriginal_4S6f_24030000562d118c.jpg)

可以看到，作者将所有图片逐张列出，此为静态实现。

那如果想要动态实现，也就是：要从独立存储空间的某个文件夹中读取图片文件，又该如何做呢？可能你会想：不就是简单的独立存储那套操作吗，直接替换上面这段繁琐的代码就欧了~

起初我也这么想，但是“想法很美好，实施起来很困难”，这个现象在计算机软件行业太常见了！上面的“美好想法”不能正常实施，因为：

（1） Win8中的独立存储操作是需要异步完成，也就是说，函数前需要有关键字async。但是在构造函数（上图中的public MainPageViewModel()）前面冠上这么一顶帽子，法理不容（Win8不支持），情理上也是说不过去的，此方案只能作罢。

（2） 也许你接着会像我一样如是想：把异步操作写在另外一个函数中，这样就可以冠冕堂皇的完成独立存储的操作，拿到想要显示的图片，剩下的只是在构造函数public MainPageViewModel()中调用这个异步函数即可；实践证明，这个做法并不可行，究其原因，是因为当有上上图（黑色背景的小图）的数据源声明时，所提供的图像资源在构造函数中必须已经是现成的，上述调用异步函数实现独立存储操作的思路是把获取图像的过程放在了另外一个函数中来实现，如此做，图像数据在构造函数中并非现成的，因而是做无法成功进行数据绑定的。

到这里，我得到了启发：既然在MainPageViewModel.cs中，想要显示的图像资源既要在构造函数中现成提供，又要满足动态获取，那我只能有一种解决办法了：在程序进入到这个类的构造函数之前就将想要得到的图像获取完毕！

思路已经很清晰了，我在App.xaml.cs中定义了存储图像资源的全局变量imgList，找一个合适的位置（除了在MainPageViewModel.cs中）访问独立存储空间获取想要的图像并存储在imgList中，然后再在MainPageViewModel.cs的构造函数中将imgList的内容与FlipView控件进行数据绑定，这个good job就完成啦！这样，每次进入图片展示页面时，任何时候显示的都是此时此刻之前产生的所有的美丽图片，再配上这般华丽的FlipView控件，真是精神和视觉双享受！

------------------------------------------------------------------------------------------------------------

以上4点就是自己在移植过程中摸索出来的个人觉得比较精华的东西了。之所以说是精华，一方面是因为个人觉得这些东西在Win8开发，尤其是跟图像关系更紧密的Win8应用开发中显得非常重要，像获取图像、保存图像这些看似简单的操作，在WP7中可以非常方便的完成，在Win8中却不那么容易，甚至万能的网络也无法帮到你；另一方面，上面遇到的这几个问题都融入了我的个人思考，甚至有的是在数十次失败的尝试后得来的，这些个探索的过程让我沉醉其中，当结果真的实现了我想要的功能的时候，这种感觉非常棒，这种在网络求助无果后独创出来的东西让我感受到强大的向前驱动力！

好吧，4点东西写了这么多。这一点不像技术博文，更像流水日志。额呵呵，随它去吧，写成啥就是啥。下面简单总结一下其他几个部分。

**5\. WP7 -&gt; Win8****移植，引用集的替换**

最令人欣慰的一点就在这里了，WP7开发中，你所using的引用集如果以“System.Windows”开头，那么执行全局搜索与替换，将“System.Windows”替换为“Windows.UI.Xaml”是丝毫没错的。更多的Win8引用集的情况可以参考这里：

[http://msdn.microsoft.com/zh-cn/library/windows/apps/br211377.aspx#__](http://rrurl.cn/81dUfR)

**6\. Win8****屏幕翻转的处理**

在WP7中，可以设置任何页面为Landscape（仅横屏模式）或Portrait（仅竖屏模式），或者二者兼可（通过翻转手机屏幕实现横竖屏切换）。但是在Win8中，这个灵活性没有了，任何页面都默认既有横屏模式又可翻转到竖屏模式。

这就带来一个问题：如果页面布局没有精心考虑，在横屏模式下设计的页面翻转为竖屏就没法正常显示了！如果是以竖屏设计的，同样会遇到横屏时页面一团糟的问题！

在WP7中可以强制是否可翻转，而在Win8中既然你没有权利选择，就只能面对和handle这个问题了！

显然，做过网站或网页，熟悉CSS的觉得这不会是个问题，因为通过CSS可以灰常好的进行页面布局设计，让页面自动去适应不同的屏幕模式。没错，这是一种很好，很专业的解决方法，其缺点就是不够业余……好吧，我没有专业学习过网页设计，CSS我不熟悉，我只能另寻他法了。

这里我跟大家分享一种简单的方式，说白了，就是对每个页面设计Landscape和Portrait两种布局，再让你的设备（平板电脑）去感知屏幕翻转的事件，并在代码中控制页面翻转，具体的实现可以参考下面的例子：

[http://www.devdiv.com/_DevDiv%E5%8E%9F%](http://rrurl.cn/ogUvch)

[E5%88%9B_Windows_8_Metro_
App%E5%BC%80%E5%8F%91_8_%E5%A](http://rrurl.cn/ogUvch)

[4%84%E7%90%86Fullscreen__Snapped%E5%92](http://rrurl.cn/ogUvch)

[%8CFilled%E7%8A%B6%E6%80%81
-thread-131457-1-1.html](http://rrurl.cn/ogUvch)

BY THE WAY，在这里给大家推荐一个学习Win8开发的好地方，前面忘了说，这里补上，DevDiv社区，很多精美的帖子，我看了之后的感觉是欣喜若狂，如果你有机会接触Win8开发，相信你也会为之动情：

[http://www.devdiv.com/Windows_8_Metro_App%E5%BC%80%](http://rrurl.cn/82tJf2)

[E5%8F%91Step_by_Step---%E6%8C%81%E7%BB%AD%E6%9B%B4%E6%96%B0_](http://rrurl.cn/82tJf2)

[2012%E5%B9%B49%E6%9C
%8811%E6%97%A5%E6%9B%B4%E6%96%B0_-thread-130633-1-1.html](http://rrurl.cn/82tJf2)

**7\. WP7****图像处理**** VS. Win8****图像处理**

做过图像处理的童鞋一定很清楚，几乎任何不同开发环境或语言下进行图像处理代码都是不一样的，但是万变不离其宗，其核心框架是没变的（那个两层循环^_^）。下面以“将图像处理为灰度图”为例贴一下WP7和Win8中的区别，再进行任何其他方面的图像处理都可以照猫画虎了。

**WP7****中，将****src****转化为灰度图像：**

public WriteableBitmap toGray(WriteableBitmap src)

{

gray = new WriteableBitmap(src);

int i, j, k;

int row_gray;

byte pixel;

byte R, G, B, A = 0;

int tmp_A = gray.Pixels[0];

A = (byte)((tmp_A &amp; 0xFF000000) &gt;&gt; 24);

for (i = 0; i &lt; gray.PixelHeight; i++)

{

row_gray = i * gray.PixelWidth;

for (j = 0; j &lt; gray.PixelWidth; j++)

{

int pixel_gray = gray.Pixels[row_gray + j];

R = (byte)((pixel_gray &amp; 0x00FF0000) &gt;&gt; 16);

G = (byte)((pixel_gray &amp; 0x0000FF00) &gt;&gt; 8);

B = (byte)(pixel_gray &amp; 0x000000FF);

pixel = (byte)(0.299 * R + 0.587 * G + 0.114 * B);

R = G = B = pixel;

pixel_gray = (A &lt;&lt; 24) | (R &lt;&lt; 16) | (G &lt;&lt; 8) | B;

gray.Pixels[row_gray + j] = pixel_gray;

}

}

return gray;

}

**Win8****中，****将****src****转化为灰度图像：**

public WriteableBitmap toGray2(WriteableBitmap src)

{

gray = cloneImg(src, gray); //自己写的函数，等效于WP7中的gray = new WriteableBitmap(src); 没办法，谁让Win8的WriteableBitmap()变傻了呢…..

int i, j;

int row_gray, index_gray;

byte pixel;

byte[] temp_src = src.PixelBuffer.ToArray();

byte[] temp_gray = new byte[temp_src.Length];

for (i = 0; i &lt; gray.PixelHeight; i++)

{

row_gray = i * gray.PixelWidth;

for (j = 0; j &lt; gray.PixelWidth; j++)

{

index_gray = (row_gray + j) * 4;

for (int k = 0; k &lt; 3; k++)

temp_gray[index_gray + k] = (byte)(0.299 * temp_src[index_gray + 2] + 0.587 * temp_src[index_gray + 1] + 0.114 * temp_src[index_gray]);

temp_gray[index_gray + 3] = 255;

}

}

Stream sTemp = gray.PixelBuffer.AsStream();

sTemp.Seek(0, SeekOrigin.Begin);

sTemp.Write(temp_gray, 0, gray.PixelWidth * 4 * gray.PixelHeight);

return gray;

}

到这里，具体的实现部分就总结完了。下面用两句话把控件相关部分简单说一下。

**二、 控件相关**

**1\. WP7****的枢轴控件**** VS. Win8****的****TopAppBar**

不得不说，WP7中的枢轴控件用起来感觉还是很爽的，但是当我的视线转向Win8时，枢轴控件没有了，我必须得寻找一种合理的替换方案了。

幸运的是，Win8提供TopAppBar这个玩意，它出现的位置在屏幕最上方，可以合理利用TopAppBar中的有限个按钮来实现页面的导航。

如果你正愁找不到枢轴控件的替代方案，不妨去试试TopAppBar吧！

**2\. WP7****的****ApplicationBar VS. Win8****的****BottomAppBar**

同样，WP7中的ApplicationBar在Win8中也改名易姓了，与TopAppBar遥相呼应，它在Win8中叫BottomAppBar. 使用方法如下，在页面的xaml文件中：

&lt;Page.BottomAppBar&gt;

&lt;AppBar&gt;

&lt;Grid HorizontalAlignment="Left" Width="768"&gt;

&lt;Grid.ColumnDefinitions&gt;

&lt;ColumnDefinition Width="425*"&gt;&lt;/ColumnDefinition&gt;

&lt;ColumnDefinition Width="248*"&gt;&lt;/ColumnDefinition&gt;

&lt;/Grid.ColumnDefinitions&gt;

&lt;StackPanel Orientation="Horizontal" Grid.Column="0" HorizontalAlignment="Left"&gt;

&lt;Button x:Name="xx1" Style="{StaticResource SaveAppBarButtonStyle}" AutomationProperties.Name="save" Click="AppBarButton_Click"/&gt;

&lt;/StackPanel&gt;

&lt;StackPanel Orientation="Horizontal" Grid.Column="1" HorizontalAlignment="Right"&gt;

&lt;Button x:Name="home" Style="{StaticResource HomeAppBarButtonStyle}" Click="AppBarButton_Click"/&gt;

&lt;/StackPanel&gt;

&lt;/Grid&gt;

&lt;/AppBar&gt;

&lt;/Page.BottomAppBar&gt;

只需要将上述代码中的BottomAppBar改为TopAppBar即为TopAppBar的使用方法。