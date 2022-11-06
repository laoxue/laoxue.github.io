---
title: LESS与SASS的区别
date: 2017-06-09 10:13:24
tags:
    - CSS
categoroes:
    - 前端技术
keywords: "LESS与SASS的区别||LESS||SASS"
description: 
top_img:
cover: https://dali-saymore-public.oss-cn-shanghai.aliyuncs.com/lessvssass.jpg
---

![](http://img0.imgtn.bdimg.com/it/u=861104756,4244471114&fm=26&gp=0.jpg)
### 前言

　首先sass和less都是css的预编译处理语言，他们引入了mixins，参数，嵌套规则，运算，颜色，名字空间，作用域，JavaScript赋值等 加快了css开发效率,当然这两者都可以配合gulp和grunt等前端构建工具使用

　sass和less主要区别:在于实现方式 less是基于JavaScript的在客户端处理 所以安装的时候用npm，sass是基于ruby所以在服务器处理。

　很多开发者不会选择LESS因为JavaScript引擎需要额外的时间来处理代码然后输出修改过的CSS到浏览器。关于这个有很多种方式，我选择的是只在开发环节使用LESS。一旦我完成了开发，我就复制然后粘贴LESS输出的到一个压缩器，然后到一个单独的CSS文件来替代LESS文件。另一个选择是使用LESS.app来编译和压缩你的LESS文件。两个选择都将最小化你的样式输出，从而避免由于用户的浏览器不支持JavaScript而可能引起的任何问题。尽管这不大可能，但终归是有可能的

#### LESS详细

首先扩展文件名的格式是 xxx.less 

在此推荐大家在练习环节可以用 

	<script src="less.js"...> 这种方式编译less

但在实际项目中 还是用命令行的 lessc xxx.less>xxx.css 方式然后引入编译后的css文件 这样减少在运行时上面出现的问题

	//安装less
	npm install -g less

##### 变量
	
	@变量名:值
	@width：100px;
	.box{
		width:@width;
	}


##### 混合

	定义classa 然后可以将classa引入到classb中
	.classa(a){
		width:@width;
	}

	.classb{
		.classa(a);
	}

##### 嵌套规则

	父级{
		子集
	}

##### 函数和运算

	可以将值计算
	@the-border: 1px;
	@base-color: #111;
	@red:        #842210;

	#header {
	  color: @base-color * 3;
	  border-left: @the-border;
	  border-right: @the-border * 2;
	}
	#footer { 
	  color: @base-color + #003300;
	  border-color: desaturate(@red, 10%);
	}


#### SASS详细

首件扩展文件名的格式是 xxx.scss 或者是 xxx.sass 

使用方法: sass xxx.scss xxx.css 

#####　编译风格：
	
	nested:嵌套缩进的css代码，默认
	expanded:没有缩紧的,扩展的css代码
	campact:简介格式的css代码
	compressed:压缩后的css代码(生产环境)

使用的时候　sass --style compressed xxx.sass xxx.css 

##### 监听目录

	sass --watch xxx.scss:xxx.css //监听文件
	sass --watch scsspath:csspath //监听文件夹

##### 变量 

	$变量名:值
	$width：100px;

	.box{
		width:$width;
	}

	如果变量包含字符串则写在 #{}之中
	$c:color;

	.box{
		border-#{$c}:red;
	}

##### 嵌套计算

less和sass嵌套相同，计算同理


##### 继承

同less混合相同 定义classa 然后再classb可饮用classa值

	//使用方法 定义classa 
	.classb{
		@extend .classa
	}

##### Mixin

即重用代码块

	//使用方法先用@mixin命令定义一个代码块
	@mixin left(参数1，参数2){
		float:left;
		margin-left:10px;
	}
	//使用@include调用刚刚定义的代码块
	.box{
		@inclidu left(参数1，参数2);
	}

##### 颜色函数 lighten(颜色，百分比)

##### 插入文件

	@import命令插入外部文件 .scss和css都可

##### 条件语句

	//@if 可以用来判断 @else 则是配套

	.box{
		@if 1+1>1 {width:100px;}@else {
			width:200px;
		}
	}

##### 循环语句

	//@for @while @each

	@for $i from 1 to 10{
		border-#{$i}{
			border:#{$i}px solid red;
		}
	}

	//@while
	$i:6;
	@while $i>0{
		.item-#{$i}{
			width:2em*$i;
		}
		$i:$i-2;
	}

	//@each
		@each $member in a, b, c, d {
	　　　　.#{$member} {
	　　　　　　background-image: url("/image/#{$member}.jpg");
	　　　　}
	　　}

##### 自定义函数

	@function name($n){
		@return $n*2;
	}

	.box{
		width:name(value);
	}

### 总结
　总体来说sass和less都有各自的好处，这要根据每个开发者的习惯和爱好来使用，都可提高开发效率，当然还有stylus等工具，因为目前未使用过所以不做评判，个人比较倾向sass，至于比较，两者都有其优缺点，如果你开发环境中并没有ruby 并且你不想安装ruby 你就可以使用less，如果你觉得sass的语法你更倾向并且你安装了ruby 你就可以使用sass。总之工具不重要，码出一手好代码才是真理。
