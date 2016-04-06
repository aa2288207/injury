```
Author: holdlg
Last updated: 2016-04-06 15:23:04
```

# Gradle 构建web项目
## 创建eclipse web项目
```
apply plugin: 'eclipse-wtp'
```
- 执行<code>gradle eclipse</code>
- 在eclipse中导入，<code>Server</code>服务可以识别添加至tomcat运行。


## 创建eclipse java项目
```
apply plugin: 'eclipse'
```
- 执行<code>gradle eclipse</code>
- 在eclipse中导入。


## gradle构建war包 和 eclipse中的导出war一样
```
apply plugin: 'war'
```
执行<code>gradle build</code>

## buildscript代码块
- 声明gradle脚本自身需要使用的资源，非项目业务使用
- 优先执行

## repositories代码库
- 依赖项、第三方插件的仓库地址

## dependencies 依赖项
- 项目所依赖的库


## 完整的build.gradle
```
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.3.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'war'
apply plugin: 'eclipse-wtp'
apply plugin: 'spring-boot'

repositories {
   mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-thymeleaf")
    compile("org.springframework.boot:spring-boot-devtools")
    testCompile("junit:junit")
}
```

# 参考链接
- [使用Gradle构建Java Web应用](http://www.blogjava.net/jiangshachina/archive/2014/01/23/409285.html)
- [Gradle中的buildScript代码块](http://www.cnblogs.com/huang0925/p/3940528.html)
- [eclipse-wtp](https://docs.gradle.org/current/dsl/org.gradle.plugins.ide.eclipse.model.EclipseWtp.html)