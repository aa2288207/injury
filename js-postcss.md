```
Author: holdlg
Last updated: 2016-03-07 10:23:04
```

# 使用条件
- git
- nodejs
- npm 或 cnpm

# 安装cnpm
(淘宝镜像，解决下载慢, 我测试下载不了)
<code>npm install -g cnpm --registry=https://registry.npm.taobao.org</code>

# postcss 安装, 个人结合gulp使用
```
# gulp自动化工具
npm install --save-dev gulp
# postcss 集成
npm install --save-dev gulp-postcss
# 自动前辍 autoprefixer
npm install --save-dev autoprefixer
# css转译器 cssnext
npm install --save-dev cssnext
# 预处理 precss
npm install --save-dev precss
```

# 初始化
 - npm init  生成package.json
 - gulp init 生成gulpfile.js


# 目录结构
```
app
| - dest
| - node-modules
| - - gulp
| - - gulp-postcss
| - - autoprefixer
| - - cssnext
| - - precss
| - src
| - gulpfile.js
| - package.json
```


# gulpfile.js
```
var gulp = require('gulp');
var postcss = require('gulp-postcss');
var autoprefixer = require('autoprefixer');
var cssnext = require('cssnext');
var precss = require('precss');

gulp.task('css', function () {
  var processors = [
    autoprefixer,
    cssnext,
    precss
  ];
  return gulp.src('./src/*.css')
    .pipe(postcss(processors))
    .pipe(gulp.dest('./dest'));
});
```

# package.json
```
{
  "name": "heart",
  "version": "1.0.0",
  "description": "heart style",
  "main": "index.js",
  "dependencies": {
    "precss": "^1.4.0",
    "cssnext": "^1.8.4",
    "autoprefixer": "^6.2.3",
    "gulp": "^3.9.0",
    "gulp-postcss": "^6.0.1"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "heart"
  ],
  "author": "holdlg",
  "license": "ISC"
}
```

# 测试
- /src/style.css
```
/* 测试 autoprefixer 插件生效 */
.autoprefixer {
  display: flex;
}

/* 测试 cssnext 插件生效 */
.cssnext {
  background: color(red alpha(-10%));
}

/* 测试 precss 插件生效 */
.precss {
  @if 3 < 5 {
    background: green;
  }
  @else {
    background: blue;
  }
}
```

- cmd -> gulp css 然后查看 /dest/style.css
```
/* 测试 autoprefixer 插件生效 */
.autoprefixer {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
}
 
/* 测试 cssnext 插件生效 */
.cssnext {
  background: rgba(255, 0, 0, 0.9);
}
 
/*  测试 precss 插件生效 */
.precss {
  background: green
}
```