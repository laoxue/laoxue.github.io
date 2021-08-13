---
title: Gulp配置文件详解
date: 2017-06-15 11:37:23
tags:
    - gulp
categoroes:
    - 前端技术
keywords: "Gulp配置文件详解||gulp"
description: 
top_img:
cover: http://img0.imgtn.bdimg.com/it/u=204367319,272230027&fm=26&gp=0.jpg
---

### 前言
![gulpfile.js](http://img0.imgtn.bdimg.com/it/u=204367319,272230027&fm=26&gp=0.jpg)
前几天写了gulp的基础自动化构建的api。

	gulp.src 文件源位置
	gulp.task 构建任务名和函数
	gulp.dest 放置文件位置
	gulp.watch 监控

这次介绍下gulp的几个常用插件和其基本配置：

#### gulp常用插件

注意: + "使用插件前要先安装对应插件 npm install 插件名字 --save-dev"
	  + "如果构建的任务没有放在默认任务default中 命令行执行的时候 gulp 任务名"
      + "task中路径都是与gulpfile放在同一级下"
      + "gulp.dest()指明的目录可以自动被创建"

##### **js压缩，合并，重命名任务**

	let gulp = require('gulp');
	let concat = require('gulp-concat');  // 合并
	let uglify = require('gulp-uglify');  // 压缩
	let rename = require('gulp-rename');  // 重命名

	 let jshint = require('gulp-jshint');  // 注意需要同时安装 jshint
	 gulp.task('scripts', function() {  // 这个任务的名称是 scripts
     gulp.src('src/js/*.js')  // 将 src/js/ 目录下的所有 js 文件合并
    	 .pipe(jshint())
    	 .pipe(jshint.reporter('default'))
    	 .pipe(concat('all.js'))  // 指定合并后的文件名为 all.js
    	 .pipe(gulp.dest('dist/js/'))  // 保存合并后的文件
    	 .pipe(uglify())  // 压缩
    	 .pipe(rename('all.min.js'))  // 重命名
    	 .pipe(rename({suffix: '.min'}))  // 和上一行等效
    	 .pipe(gulp.dest('dist/js/'));
	});

##### **sass编译**

	let gulp = require('gulp');
	let sass = require('gulp-sass');  // sass -> css
	let prefixer = require('gulp-autoprefixer');  // 增加前缀
	let minify = require('gulp-minify-css');  // css 压缩
	let notify = require('gulp-notify');  // 打印提醒语句
	let concat = require('gulp-concat');  // 合并

	// 编译Sass
	 gulp.task('css', function() {  // 任务名
	 gulp.src('sass/*.scss')  // 目标 sass 文件
    	  .pipe(sass())  // sass -> css
    	  .pipe(prefixer('last 2 versions'))  // 参数配置参考 <https://github.com/ai/browserslist>
     	  .pipe(minify())  // 压缩
    	  .pipe(gulp.dest('css'))  // 目标目录
    	  .pipe(notify({message: 'done'}))
    	  .pipe(concat('all.min.css'))  // 合并
    	  .pipe(gulp.dest('css'));  // 目标目录
	});

##### **图片压缩**

	let gulp = require('gulp');
	let imagemin = require('gulp-imagemin');
	let cache = require('gulp-cache');  // 减少重复压缩

	gulp.task('images', function() {
		gulp.src('src/images/*')
    		.pipe(cache(imagemin({ optimizationLevel: 3, progressive: true, interlaced: true })))
    		.pipe(gulp.dest('dist/images/'));
	});

##### **监控文件**

	gulp.task('watch', function() {  // 指定任务名为 watch
		gulp.watch('src/sass/a.scss', ['sass']);// 监控 a.scss 文件，如果有修改，则执行 sass 任务
	});

##### **删除文件**

	let gulp = require('gulp');
	let clean = require('gulp-clean');

	gulp.task('clean', function() {
		return gulp.src(['dist/js/*', 'dist/sass/*', 'dist/images/*'], {read: false})
    	.pipe(clean());
	});

##### **ES6->ES5**

安装插件 npm install gulp-babel babel-preset-es2015 --save-dev

	let gulp = require('gulp');
	let babel = require('gulp-babel');

	gulp.task('scripts', function() {
		gulp.src('src/js/a.js')
    	    .pipe(babel({  // es6 -> es5
           presets: ['es2015']
    }))
            .pipe(gulp.dest('dist/js/'))
	});

> 参考文章：[http://www.cnblogs.com/zichi/p/6250504.html](http://www.cnblogs.com/zichi/p/6250504.html)

### 总结

除此之外还有很多插件可供安装，如果引入插件很多可以尝试使用 gulp-load-plugin模块、还有borswer-sync等模块，由于这方面我还没有认真看过所以这里就不详细介绍了，如果个人在刚学gulp的话，我推荐多敲几遍gulpfile.js的配置文件，尝试一些自动化构建自己的小项目，然后根据项目需求再引入其他插件使用或者使用模块。
