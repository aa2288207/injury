```
Author: holdlg
Last updated: 2016-03-21 17:23:04
```

# java写文件
```
import java.util.Random;

public class Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        String logPath = "C:\\login.log";
        String loginStr = "登录日志信息：ip";
        File writename = new File(logPath);
        writename.createNewFile(); 

        // new FileWriter(writename, true) 参数true代表追加
        BufferedWriter out = new BufferedWriter(new FileWriter(writename, true));  
        out.write(loginStr); 
        out.flush();
        out.close();
    }

}
```

# java读取配置
```
import java.io.IOException;
import java.util.Properties;

public class ReadConfig {
    private static Properties properties = new Properties();
    
    static{
        try {
            // message.properties 在项目src目录下
            properties.load(ReadConfig.class.getClassLoader().getResourceAsStream("message.properties"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    public static String getConfigInfo(String key){
        return (String)properties.get(key);
    }
}
```

# java时间格式化
```
import java.text.SimpleDateFormat;
import java.util.Locale;

public class Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss",Locale.SIMPLIFIED_CHINESE);
        String timeStr = sdf.format(new Date());
        System.out.println(timeStr);
    }

}
```

# java随机数
```
import java.util.Random;

public class Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Random random = new Random();
        int x = random.nextInt(10);
        System.out.println(x);
    }

}
```

# java String.format
### 占位符说明
|转  换  符 |说    明| 示    例
| --------| ----------------| ----------|
| %s  | 字符串类型 | "mingrisoft"|
| %c  | 字符类型 | 'm'|
| %b  | 布尔类型 | true|
| %d  | 整数类型（十进制） | 99|
| %x  | 整数类型（十六进制）| FF|
| %o  | 整数类型（八进制）| 77|
| %f  | 浮点类型 | 99.99|
| %a  | 十六进制浮点类型 | FF.35AE|
| %e | 指数类型 | 9.38e+5|
| %g | 通用浮点类型（f和e类型中较短的） | - |
| %h | 散列码 | - | 
| %%  | 百分比类型 | % | 
| %n | 换行符 | - |
| %tx | 日期与时间类型（x代表不同的日期与时间转换符  | - |

### 用例
```
public static void main(String[] args) {
        String str=null;
        str=String.format("Hi,%s", "王力");
        System.out.println(str);
        str=String.format("Hi,%s:%s.%s", "王南","王力","王张");          
        System.out.println(str);                         
        System.out.printf("字母a的大写是：%c %n", 'A');
        System.out.printf("3>7的结果是：%b %n", 3>7);
        System.out.printf("100的一半是：%d %n", 100/2);
        System.out.printf("100的16进制数是：%x %n", 100);
        System.out.printf("100的8进制数是：%o %n", 100);
        System.out.printf("50元的书打8.5折扣是：%f 元%n", 50*0.85);
        System.out.printf("上面价格的16进制数是：%a %n", 50*0.85);
        System.out.printf("上面价格的指数表示：%e %n", 50*0.85);
        System.out.printf("上面价格的指数和浮点数结果的长度较短的是：%g %n", 50*0.85);
        System.out.printf("上面的折扣是%d%% %n", 85);
        System.out.printf("字母A的散列码是：%h %n", 'A');
    }
```
输出
```
Hi,王力
Hi,王南:王力.王张
字母a的大写是：A 
3>7的结果是：false 
100的一半是：50 
100的16进制数是：64 
100的8进制数是：144 
50元的书打8.5折扣是：42.500000 元
上面价格的16进制数是：0x1.54p5 
上面价格的指数表示：4.250000e+01 
上面价格的指数和浮点数结果的长度较短的是：42.5000 
上面的折扣是85% 
字母A的散列码是：41 
```

参考链接：[String.format](http://blog.csdn.net/lonely_fireworks/article/details/7962171)