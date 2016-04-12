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


# gradle构建java项目

### 目录结构
```
domeboot
|
├─.gradle
│  └─2.12
│      └─taskArtifacts
├─build
│  ├─classes
│  │  └─main
│  │      └─hello
│  ├─dependency-cache
│  ├─libs
│  └─tmp
│      ├─compileJava
│      │  └─emptySourcePathRef
│      └─jar
├─gradle
│  └─wrapper
├─src
│   └─main
│        ├─java
│        │  └─hello
│        ├─resources
│        └─test
├─build.gradle
├─gradlew
└─gradlew.bat
```
- <code>.gradle</code> gradle自动生成的文件，无视即可。
- <code>build/classes</code> 编译之后的class文件
- <code>build/dependency-cache</code> 依赖缓存文件
- <code>build/libs</code> 编译生成的 <code>jar</code> 或 <code>war</code> 文件，可执行或部署。
- <code>build/tmp</code>临时文件夹
- <code>gradle/wrapper</code> 便于其他开发人员在没有gradle的环境中构建项目 
- <code>src/main/java</code>java源码
- <code>src/main/resources</code>java资源，如css,js,image,html
- <code>src/main/test</code> 测试用例
- <code>gradlew</code>linux系统下的gradle包装器，没有安装gradle的时候执行这个就行可以了
- <code>gradlew.bat</code>windows系统下的gradle包装器
```
// java项目
apply plugin: 'java'
// 可执行
apply plugin: 'application'
// 编译执行的入口
mainClassName = 'hello.HelloWorld'

// 仓库地址
repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

// 依赖关系
dependencies {
    compile "joda-time:joda-time:2.2"
}

// 打包文件信息
jar {
    baseName = 'gs-gradle'  // 名称
    version =  '0.1.0'      // 版本
}

// gradle wrapper 在没有安装gradle的情况下，构建项目
// 1. $ gradle wrapper  2. $ ./gradlew build
task wrapper(type: Wrapper) {
    gradleVersion = '2.12'
}
```
## 参考链接
- [gradle构建java项目](https://spring.io/guides/gs/gradle/)