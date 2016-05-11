```
Author: holdlg
Last updated: 2016-03-30 11:00:04
```

# Angular 2 入门

## 有关angular 1 
没学过，没用过，不评价

## 有关angular 2 
知道多少说多少,参考[Angular 2 quickstart](https://angular.io/docs/ts/latest/quickstart.html),不要问为什么。
![angular2 5分钟入门](https://raw.githubusercontent.com/holdlg/injury/master/img/js/angular2.png)
## 有关组件化说明
组件化的思想，什么是组件化？组件化就是组件化呗。大概就和搭积木一样了，自己脑补一下吧，o(^▽^)o。。。。

## angular 2 配置

### tsconfig.json
告诉程序如何将TypeScript编译成JavaScript
```
{
  "compilerOptions": {
    "target": "es5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  },
  "exclude": [
    "node_modules",
    "typings/main",
    "typings/main.d.ts"
  ]
}
```

### typings.json
是为了搞好兼容性，解决TypeScript不能识别的语法处理，神马的吧。
```
{
  "ambientDependencies": {
    "es6-shim": "github:DefinitelyTyped/DefinitelyTyped/es6-shim/es6-shim.d.ts#7de6c3dd94feaeb21f20054b9f30d5dabc5efabd",
    "jasmine": "github:DefinitelyTyped/DefinitelyTyped/jasmine/jasmine.d.ts#7de6c3dd94feaeb21f20054b9f30d5dabc5efabd"
  }
}
```

### package.json
node的包管理工具npm的配置文件,<code>npm install</code>开始按照配置文件安装所需要的包.
其中<code>scripts</code>是<code>npm run script</code>的操作,自行google了。
```
{
  "name": "angular2-quickstart",
  "version": "1.0.0",
  "scripts": {
    "start": "concurrently \"npm run tsc:w\" \"npm run lite\" ",    
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "lite": "lite-server",
    "typings": "typings",
    "postinstall": "typings install" 
  },
  "license": "ISC",
  "dependencies": {
    "angular2": "2.0.0-beta.12",
    "systemjs": "0.19.24",
    "es6-shim": "^0.35.0",
    "reflect-metadata": "0.1.2",
    "rxjs": "5.0.0-beta.2",
    "zone.js": "0.6.6"
  },
  "devDependencies": {
    "concurrently": "^2.0.0",
    "lite-server": "^2.1.0",
    "typescript": "^1.8.9",
    "typings":"^0.7.9"
  }
}
```

## angular 2 元素

### app/app.components.ts
```
import {Component} from 'angular2/core';  // 导入angular2包

@Component({   // 组件装饰器
    selector: 'my-app',   // 标签选择器，对应html页面的<my-app></my-app>标签
    template: '<h1>My First Angular 2 App</h1>'  // 使用template的值去解析 my-app 标签。
})  

// 在上面的代码中html页面的 <my-app></my-app> 标签最终显示为 <h1>My First Angular 2 App</h1>

export class AppComponent { }  // 可以被引用的根组件，是个类，类内可以定义其他属性或函数，这些可以被组件装饰器直接使用
```

### app/main.ts
```
import {bootstrap}    from 'angular2/platform/browser';  // 引导组件
import {AppComponent} from './app.component';  // 导入自定义根组件

bootstrap(AppComponent);  // 引导至根组件
```

### index.html
- SystemJs 管理js包

```

<html>
  <head>
    <title>Angular 2 QuickStart</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">    
    <link rel="stylesheet" href="styles.css">
    <!-- 1. Load libraries -->
    <!-- IE required polyfills, in this exact order -->
    <script src="node_modules/es6-shim/es6-shim.min.js"></script>
    <script src="node_modules/systemjs/dist/system-polyfills.js"></script>
    <script src="node_modules/angular2/es6/dev/src/testing/shims_for_IE.js"></script>   
    <script src="node_modules/angular2/bundles/angular2-polyfills.js"></script>
    <script src="node_modules/systemjs/dist/system.src.js"></script>
    <script src="node_modules/rxjs/bundles/Rx.js"></script>
    <script src="node_modules/angular2/bundles/angular2.dev.js"></script>
    <!-- 2. Configure SystemJS -->
    <script>
      System.config({
        packages: {        
          app: {
            format: 'register',
            defaultExtension: 'js'
          }
        }
      });
      // 程序入口
      System.import('app/main')
            .then(null, console.error.bind(console));
    </script>
  </head>
  <!-- 3. Display the application -->
  <body>
    <my-app>Loading...</my-app>
  </body>
</html>
```

### styles.css
```
/* Master Styles */
h1 {
  color: #369; 
  font-family: Arial, Helvetica, sans-serif;   
  font-size: 250%;
}
h2, h3 { 
  color: #444;
  font-family: Arial, Helvetica, sans-serif;   
  font-weight: lighter;
}
body { 
  margin: 2em; 
}
body, input[text], button { 
  color: #888; 
  font-family: Cambria, Georgia; 
}

/* 
 * See https://github.com/angular/angular.io/blob/master/public/docs/_examples/styles.css
 * for the full set of master styles used by the documentation samples
 */
```

### npm start
- 查看浏览器 http://localhost:3000

# @Component
- <code>selector</code>
- <code>template</code>
- <code>templateUrl</code>
- <code>host</code>给<code>selector</code>添加class属性
- <code>style</code>
- <code>styleUrls</code>
- <code>inputs</code>

# Angular 编码风格
- [angular2 编码风格](https://angular.io/styleguide)

### 01 单一职责

##### Style 01-01 一个规则
- 每个文件定义一件事情(component 或 service 或 bootstrap)
- 每个文件不超过400行

##### Style 01-02 小函数
- 定义小函数
- 不超过75行

### 02 命名

##### Style 02-01 通用命名规则
- 依据文件类型使用统一的后缀命名
- 如：<code>hero.type.ts</code> 

##### Style 02-02 文件名
- 命名使用“-”连字符和“.”点链接
- 使用常规后缀 <code>*.service.ts</code> , <code>*.component.ts</code> , <code>*.pipe.ts</code> 

##### Style 02-03 组件和指令
- 文件名和类名一致 (e.g <code>class HoldlgDataComponent</code> <code>holdlg-data.component.ts</code>)
- 同一功能模块的命名一直(e.g <code>class HoldlgDataComponent</code> <code>class HoldlgServiceComponent</code>)
- 类名用骆驼命名法

##### Style 02-04 服务名称
- 使用统一的后缀命名所有的服务(e.g <code>*.service.ts</code>)
- 使用骆驼命名法

##### Style 02-05 引导
- 引导放入main.ts文件中
- 不要在引导文件中写逻辑

### Style 01-02

##### Style 05-14 成员序列
- 对象属性在上，对象函数在下
- 先公有对象后私有对象

##### Style 05-15 逻辑尽量写在服务中
- 视图这不要写逻辑
- 逻辑写入Service中，方便重用

##### Style 05-16 前缀属性和函数
- 不要使用<code>on</code>开头
- <code>on-*</code>绑定错误

##### Style 05-17 逻辑展示
- 不要再模板中显示逻辑算法的过程
- 如<code>+</code>,<code>-</code>计算，在组件中实现
