title: windows  phone  对SQLite的通用类
categories:
  - WP8
date: 2013-09-04 13:15:45
tags:
  - WP8
---

public class SQLiteHelper
{
private static SQLiteConnection mySQLiteDB =null;
private String _dbName;
// public static string sqlitePath = Path.ChangeExtension(Assembly.GetExecutingAssembly().GetName().CodeBase, "db");
//数据库连接字符串(web.config来配置)，可以动态更改connectionString支持多数据库.
public SQLiteHelper(string assemblyName, string dbName)
{
IsolatedStorageFile store = IsolatedStorageFile.GetUserStoreForApplication();
if (!store.FileExists(dbName))
{
CopyFromContentToStorage(assemblyName,dbName);
}
_dbName = dbName;
}
/// &lt;summary&gt;
/// 打开数据库连接
/// &lt;/summary&gt;
private void Open()
{
if (mySQLiteDB == null)
{
mySQLiteDB = new SQLiteConnection(_dbName);
mySQLiteDB.Open();
}
}
/// &lt;summary&gt;
/// 构析函数（类销毁时调用）
/// &lt;/summary&gt;
~SQLiteHelper()
{
Close();
}
/// &lt;summary&gt;
/// 关闭数据库连接
/// &lt;/summary&gt;
private void Close()
{
if (mySQLiteDB != null)
{
mySQLiteDB.Dispose();
mySQLiteDB = null;
}
}
/// &lt;summary&gt;
/// 添加数据
/// &lt;/summary&gt;
/// &lt;typeparam name="T"&gt;&lt;/typeparam&gt;
/// &lt;param name="obj"&gt;&lt;/param&gt;
/// &lt;param name="statement"&gt;Sql语句&lt;/param&gt;
/// public int Insert(string obj,string parameter) // 原来的 T 被替换为 string { return obj.ToString(); }
/// where T:class{} //这句表示T必须是一个类，这是一个约束。
/// &lt;returns&gt;&lt;/returns&gt;
public int Insert&lt;T&gt;(T obj, string statement) where T : new()
{
try
{
Open();
SQLiteCommand cmd = mySQLiteDB.CreateCommand(statement);
int rec = cmd.ExecuteNonQuery(obj);
return rec;
}
catch (SQLiteException ex)
{
System.Diagnostics.Debug.WriteLine("Insert failed: " + ex.Message);
throw ex;
}
}
/// &lt;summary&gt;
/// 删除数据
/// &lt;/summary&gt;
/// &lt;typeparam name="T"&gt;&lt;/typeparam&gt;
/// &lt;param name="statement"&gt;Sql语句&lt;/param&gt;
public void Delete&lt;T&gt;(string statement) where T : new()
{
try
{
Open();
SQLiteCommand cmd = mySQLiteDB.CreateCommand(statement);
cmd.ExecuteNonQuery();
}
catch (SQLiteException ex)
{
System.Diagnostics.Debug.WriteLine("Deletion failed: " + ex.Message);
throw ex;
}
}

public List&lt;T&gt; SelectList&lt;T&gt;(String statement) where T : new()
{
Open();
SQLiteCommand cmd = mySQLiteDB.CreateCommand(statement);
var lst = cmd.ExecuteQuery&lt;T&gt;();
return lst.ToList&lt;T&gt;();
}
/// &lt;summary&gt;
/// 查询数据
/// &lt;/summary&gt;
/// &lt;typeparam name="T"&gt;实体类对象&lt;/typeparam&gt;
/// &lt;param name="statement"&gt;sql语句&lt;/param&gt;
/// &lt;returns&gt;返回集合&lt;/returns&gt;
public ObservableCollection&lt;T&gt; SelectObservableCollection&lt;T&gt;(string statement) where T : new()
{
List&lt;T&gt; lst = SelectList&lt;T&gt;(statement);
ObservableCollection&lt;T&gt; oc = new ObservableCollection&lt;T&gt;();
foreach (T item in lst)
{
oc.Add(item);
}
return oc;
}
private void CopyFromContentToStorage(string assemblyName, string dbName)
{
IsolatedStorageFile store = IsolatedStorageFile.GetUserStoreForApplication();
Stream localDBPath = Application.GetResourceStream(new Uri("/" + assemblyName + ";component/" + dbName,UriKind.Relative)).Stream;
IsolatedStorageFileStream dest = new IsolatedStorageFileStream(dbName,FileMode.OpenOrCreate,FileAccess.Write,store);
localDBPath.Position = 0;
CopyStream(localDBPath, dest);
dest.Flush();
dest.Close();
localDBPath.Close();
dest.Dispose();
}
private static void CopyStream(Stream input, IsolatedStorageFileStream output)
{
byte[] buffer=new byte[32768];
long TempPos = input.Position;
int readCount;
do
{
readCount=input.Read(buffer,0,buffer.Length);
if(readCount&gt;0)
{
output.Write(buffer,0,readCount);
}
} while(readCount&gt;0);
input.Position = TempPos;
}
}

&nbsp;

&nbsp;

windows phone UI中的使用：

App设置：

`public` `partial ``class` `App : Application`

{

`private` `DBHelper _db;`

public SQLiteHelper Db
{
get {
Assembly assem = Assembly.GetExecutingAssembly();
if (_db == null)
{
_db = new SQLiteHelper(assem.FullName.Substring(0, assem.FullName.IndexOf(',')), "database1.sqlite");
}
return _db; }
}

}

页面中的使用：

`public` `partial ``class` `TestDataEditor : PhoneApplicationPage`

{

`ObservableCollection&lt;Customer&gt; _customerEntries = ``null``;`

`public` `TestDataEditor()`

{

InitializeComponent();

`string` `strSelect = ``"SELECT ID,Name,Email,Desc FROM Customer ORDER BY ID ASC"``;`

`_customerEntries = (Application.Current ``as` `App).db.SelectObservableCollection&lt;Customer&gt;(strSelect);`

`foreach` `(Customer data ``in` `_customerEntries)`

{

TextBlockID.Text += data.ID + Environment.NewLine;

TextBlockEmail.Text +=data.Email + Environment.NewLine;

TextBlockName.Text +=data.Name + Environment.NewLine;

TextBlockDesc.Text +=data.Desc + Environment.NewLine;

}

`private` `void` `btnAdd_Click(``object` `sender, RoutedEventArgs e)`

{

DateTime start = DateTime.Now;

`int` `rec;`

`Random rnd = ``new` `Random();`

`string` `strInsert = ``" Insert into Customer (Name,Email,Desc) values (@Name,@Email,@Desc)"``;`

`for` `(``int` `i = 0; i &lt; 5; i++)`

{

`Customer tst = ``new` `Customer`

{

`Name = ``"Name "` `+ i,`

`Email = Name + ``"@"` `+ ``"aaa.com"``,`

`Desc = ``"Desc for "` `+ i`

}

`rec = (Application.Current ``as` `App).db.Insert &lt; Customer&gt;(tst,strInsert);`

}

`System.Diagnostics.Debug.WriteLine(``"\nInserted 5 "` `+ ``" rows\r\nGenerated in "` `+ (DateTime.Now - start).TotalSeconds);`

}

`.``private` `void` `btnDel_Click(``object` `sender, RoutedEventArgs e)`

{

DateTime start = DateTime.Now;

`string` `strDel = ``" Delete from Customer where ID="``+ ``"(SELECT COUNT(*) FROM Customer)"` `;`

`(Application.Current ``as` `App).db.Delete&lt;Customer&gt;(strDel);`

}

}

后续测试更正