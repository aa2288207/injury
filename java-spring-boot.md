```
Author: holdlg
Last updated: 2016-04-06 16:20:04
```

# spring-boot
- 简化spring项目的配置管理
- [完整代码参考](https://spring.io/guides/gs/serving-web-content/)

## 内嵌tomcat方式启动
目录结构
```
└── src
    └── main
        └── java
            └── hello
```
引导启动代码<code>src/main/java/hello/Application.java</code>

```
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```
- 启动：<code>java -jar build/libs/gs-serving-web-content-0.1.0.jar</code>
- 访问：<code>http://localhost:8080/greeting</code>

## 部署到已有tomcat启动
目录结构
```
└── src
    └── main
        └── java
            └── hello
```
引导启动代码<code>src/main/java/hello/Application.java</code>
```
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.context.web.SpringBootServletInitializer;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan
@EnableAutoConfiguration
public class Application extends SpringBootServletInitializer {

    public static void main(String[] args) {
        SpringApplication.run(applicationClass, args);
    }

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(applicationClass);
    }

    private static Class<Application> applicationClass = Application.class;
}
```
- 启动tomcat即可
- 访问：<code>http://localhost:8080/greeting</code>