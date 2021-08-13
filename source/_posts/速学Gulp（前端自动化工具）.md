---
title: 速学Gulp（前端自动化工具）
date: 2021-08-13 11:36:40
tags:
    - gulp
categoroes:
    - 前端技术
keywords: "速学Gulp（前端自动化工具）||gulp||教学"
description: 
top_img:
cover: https://bs-uploads.toptal.io/blackfish-uploads/blog/post/seo/og_image_file/og_image/15409/0820-an-introduction-to-automation-with-gulp-Waldek_Social-f4d913f00bb7819cd315d99b95eb2765.png
---

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497834217&di=d35221240a49828e2fb34e28f153abf6&imgtype=jpg&er=1&src=http%3A%2F%2Fimages2015.cnblogs.com%2Fblog%2F968549%2F201607%2F968549-20160711235626529-1718382852.png)

### 前端自动化

　随着前端方面的知识越来越多，需求也变得越多，加上一些编译语言的出现如 sass，less，typescript等的出现需要我们在项目中不停地重复编译他们把他们转换为浏览器可以识别的css和javascript,这就代表着如果没有前端自动化，我们就需要不停地重复编译这个过程，为了解决这一问题，于是乎就出现了 gulp，grunt等前端自动化工具，顾名思义，gulp和grunt就是帮我们省去重复这一步，我们只需要一个配置文件就可以让gulp和grunt帮我们完成那些需要我们在开发中重复的步骤，更好的去提高开发效率。

　本文以gulp为例介绍安装(确保安装了node.js和npm包管理工具)和使用方法:

#### gulp

	//安装gulp
	npm install -g gulp (此为全局安装)
	npm install --save-dev gulp (此为项目开发依赖)

上面两种安装方式可以根据自己的实际开发进行选择

然后我们在根目录创建一个名为**gulpfile.js**文件(gulp的配置文件，告诉gulp要执行什么任务)，内容如下：

	//gulp.js
	var gulp = require('gulp') //引入gulp相关文件
	gulp.task('default',function(){
			这里放入默认任务代码
		})
	//然后再终端输入gulp 即可运行

上面的操作就是gulp的大概流程，下面我们来细致讲解一下：

	//gulp分为四个api
	+ gulp.src(globs[, options])  //告诉gulp的要配置的文件路径
	+ gulp.dest(path[,options])  //告诉gulp写入文件地址
	+ gulp.task(name[, deps], fn) //告诉gulp你的这个任务的名字和要做点什么
	+ gulp.watch(glob[, opts], tasks)  //告诉gulp你要帮我监控这个任务有变化就执行它

使用的时候大概如下：(例子是一个简单的任务gulpfile.js配置)

	var gulp = require('gulp')
		xxx  = require('xxx') //引入其他插件 xxx代表名字

	gulp.task('sass',function(){  //这里定义一个任务名字叫做sass
		gulp.src(path) //以sass插件为例 这里告诉gulp，sass源文件存放的位置
		.pipe(sass())  //这里告诉gulp我要用sass()插件执行任务
		.pipe(gulp.dest('path') //这里告诉gulp 我要把转化后的css放到path这个目录
		})

如果定义其他任务依旧用**gulp.task**方法
	
	//然后我们建造一个监控方法 时刻监控刚刚的sass任务，让我们改变sass文件自动执行sass任务
	gulp.task('watch',function(){
		gulp.watch(path,[xxx])  //这里告诉gulp 监控path这个路径，有改变就用xxx方法去执行它
		})

最后我们把这个watch函数绑定到默认任务上(切记在使用插件的时候先用npm下载插件)
	
	gulp.task('default',['watch','sass']) //把watch任务绑定到默认任务上 这样我们执行gulp就可以执行任务



#### 插件 (下面是一些常用的gulp插件)

	gulp-rename  //重命名
	gulp.uglify  //js文件压缩
	gulp-minify-html //html压缩
	gulp-minify-css  //css压缩
	gulp-jshint  //js代码检查
	gulp-concat  //文件合并
	gulp-less gulp-sass  //sass和less插件
	gulp-imagemin //图片压缩
	gulp-livereload //自动刷新插件

### 总结
　这就是前端自动化工具gulp的简易使用方式，千万切记使用前一定要先下载对应的插件要不然无效，gulp和grunt都是方便我们开发效率的工具，也让前端开发越来越规范化，最后的最后如果这篇文章对你的开发有帮助，请不要吝啬你的喜欢和关注，我会定期发布一些自己对前端方面的见解，希望能与更多开发者一同进步，“Hello,world".