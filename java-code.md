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

