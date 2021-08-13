---
layout: es5
title: ES6(ECMA2016)
date: 2017-06-09 13:47:34
tags:
    - javascript
categoroes:
    - 前端技术
keywords: "ES6(ECMA2016)||JavaScript"
description: 
top_img:
cover: https://blog.jscrambler.com/content/images/2017/07/quick-introduction-to-es6-modules.png
---

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1497007302343&di=2c3a60a86cb9ec749ffd3cc197f7ff16&imgtype=0&src=http%3A%2F%2Fww1.sinaimg.cn%2Flarge%2F8c81192fjw1eoi8dzns49j20go0dpta5.jpg)
### 前言

>　首先说下什么是ECMAscript ，ECMAscript是Javascript的标准，也就是他的规格。
Javascript是脚本语言，所以ECMAscript就是规定了Javascript如何去更好的去运行脚本语言。

　ECMAscript 从最初开始发布过很多个版本，ES6因为是2015年发布，所以也叫ECMAscript2015. 记录本篇文章的想法是巩固ES5的内容，并且学习ES6的新特性。下面开始学习吧！

#### ES5

　ES5 多半是扩展原生对象的功能，主要扩展了 **Object**， **Array**， **Function** 等对象功能，并且加入了 **strict mode** 严格模式(即是 在使用前输入 use strict 就会进入严格模式 对后方代码书写进行严格控制，不规范就会报错)，和JSON.parse等功能。

　ES5的大部分特性 在ie9+ 都得到支持所以都可实现在JavaScript。

##### Objest

传入参数o必须是object类型，如果不是则会抛出异常

	Object.getPrototypeOf(o) //获取o的prototype对象，等价于以前的o.__proto__ 
	Object.getOwnPropertyDescriptor(o,p) //获取对象描述，和Object.defineProperty相关方法 
	Object.getOwnPropertyNames(o) //获取自由属性名列表，结果列表将不包含原型链上的属性
	Object.create(o,p) //以o为prototype创建新的对象并返回，如果对象描述p存在 就是用刚刚定义创建的对象
	Object.defineProperty(o,p,attrs) //根据规则attrs定义对象o上，属性名为p的属性
	Object.defineProperties(o,props) //根据对象描述props来定义对象o，通常props包含多个属性的定义
	Object.seal(o) //一个对象在默认状态下，
		extensible: 可以添加新的属性
		configurable: 可以修改已有属性的特性
		Object.seal会改变这两个特性，既不能扩展新属性，也不能修改已有属性的特性。
	Object.freeze(o) //将对象的每个自有自有属性(own property)做如下操作：
		属性的writable特性置为false
		属性的configurable特性置为false
		同时，该对象将不可扩展。可见，该方法比Object.seal更加严格的限制了对一个对象的未来改动。
	Object.preventExtensions(o) //将对象置为不可扩展
	Object.isSealed(o) //判断一个对象是否sealed：
		对象的每个自有属性：如果属性的configurable特性为true，则返回false
		如果对象为extensible的，那么返回false
		不满足以上两个条件，则返回true
	Object.isFrozen(o) //
		对每个自有属性，如果该属性的configurable或writable特性为true，则返回false
		如果对象为extensible的，那么返回false
		不满足以上两个条件，则返回true
	Object.isExtensible(o) //判对一个对象是否可扩展
	Object.keys(o) //返回对象o的所有可枚举(enumerable)属性的名称
	Object.prototype.isPrototypeOf(v) //检查对象是否是位于给定对象v的原型链上
	Object.prototype.propertyIsEnumerable(p) //检查一个对象上的属性p是否可枚举

##### Array 

	Array.isArray(a) //判断a是否为为真正的Array
	Array.prototype.indexOf(e,i) //使用“严格等”来判断元素e在数组中的索引号。一个可选的搜索起点i
	Array.prototype.lastIndexOf(e,i) //获取元素e在数组中最后出现的位置。起始位置i为可选
	Array.prototype.every(t,c) //测试数组中的每个元素都满足测试t。之后介绍的所有数组遍历方法，都支持一个可选的上下文对象c，可以灵活设置回调函数的执行上下文。传递给数组的测试函数、遍历函数通常有如下签名：
		function(item, index, array) {}
	Array.prototype.some(t,c) //测试数组中是否有元素满足测试t
	Array.prototype.forEach(f,c) //使用函数f遍历每个数组的元素
	Array.prototype.map(f,c) // 使用函数f修改每个数组的每个元素。按顺序收集f的每个返回值，并返回这个新组成的数组
	Array.prototype.filter(f,c) //收集通过函数测试f的书组元素
	Array.prototype.reduce(r,v) //从左向右，使用函数r聚集数组的每个元素。可以可选的制定一个初始值v
	Array.prototype.reduceRight(r,v) //Array.prototype.reduce的从右向左的版本 

##### String

	String.prototpye.trim //去掉字符串两头的空白符和换行符
	字符订阅:
		//property access on strings
		"abc"[2] === "b"

##### Function

	Function.prototype.bind(thisTarget, arg1,...argn) //为了指定当前函数的上下文对象和运行参数，该函数创建一个新的函数，保留给定的this对象和运行参数

##### Json 

	JSON.parse(text) //根据rfc4627标准解析JSON文本
	JSON.stringify(obj) //将指定的对象obj序列化为JSON文本

##### Date

	Date.now //获取当前时间距1970.1.1 00:00:00的毫秒数
	Date.prototype.toISOString //根据ISO8601生成时间字符串
		(new Date).toISOString()
		'2014-04-02T08:31:53.049Z'

#### ES6

　复习完ES5，下面我们来学习ES6吧，ES6加入了很多新特性，但是ES6还没有完全可以在JavaScript中直接书写，我们可以用Babel来把你书写的ES6转换为ES5。所以我们先来讲下Babel

Babel:一个广泛使用的ES6转码器，可以将ES6代码转为ES5代码.
	
	//首先在你的项目根目录下 配置文件.babelrc 用来设置转码规则和插件
		{
			"presets":[],
			"plugin":[]
		}
	字段设定转码规则 需要根据自己的需求进行安装 
	npm install --save-dev 转码规则
	//安装命令行转码工具 babel-cli 用于命令行转换。
	npm install --global babel-cli 

使用方法:

	babel xxx.js  //标准输出
	babel xxx.js  --out-file（或者-o） xxx.js //指定输出文件
	babel src --out-dir lib（或者-d） 指定输出目录
	babel src -d lib -s //加入-s参数生成source map文件
	注意：在命令行使用babel的时候要确定全局安装babel 或者在根目录下安装项目中如下
	npm install --save-dev babel-cli 
	然后改写package.json 
	{
	// ...
	"devDependencies":{
		"babel-cli": "^6.0.0"},
		"scripts": {
    	"build": "babel src -d lib"},
	}

转码的时候执行下面命令即可：
	
	npm run build

此外还有一些其他相关babel的工具，自行参考。

#### ES6新特性 

##### let 和 const

ES6新增了let命令 用来声明变量 同var相同 但是作用域却不同，let声明变量为块级作用域

	for(let i=1;i<8;i++){

	}
	console.log(i) // 这里会在控制台提示i找不到 因为let声明的i只作用在函数内部

+ 这样做的好处就是避免了变量提升即在用var 声明一个变量前先调用会提示 undifind 但是用了let后如果在声明前就调用会报错
+ 避免污染全局变量
+ let 不允许在同一个作用域中声明相同变量

而const也用来声明变量 但是声明的是常量，如果我们声明后再改变const变量就会报错

##### Class

ES6中引入了类的概念，使的Javascript更加规范，成为面向对象变成的语法。

	class Name{
		//构造方法 constructor  this代表实力对象
		constructor(){
			this.name = 'tom'
		}
		says(say){
			console.log(this.name+'is'+say)
		}
	}
	//创建一个是实例
	let person = new Name()
	person.syas('hello,world')

Class 的继承 用extends关键字实现 比如一个 Mingzi类需要继承 Name 

	class Mingzi extends Name{
		constructor(){
			super()
			this.type = 'girl'
		}
	}
这里super只带父类的实例，子类必须在constructor方法中调用super 否则会报错 如果不调用super方法 子类就得不到this对象。

然后我们实例化Mingzi 

	let girl = new Mingzi()
	girl.says('i am a sexy girl')


##### 箭头函数 arrow function

	function(i){return i*5}  ==  (i) => i*5

	如果函数内内容比较多用{}括起来

##### template string 

这个应用于 如果我们利用js中写好一个html模板 然后再加入html中这个情形，如果之前那种方法会很容易出错，因为会加入很多+和单双引号问题。

在es6中使用模板字符串 `` 和 ${} 即可
	
	用反引号`表明起始，用${}来引用变量

##### 函数默认值
	
	function names(name = 'dali'){
		console.log(name)
	}
	names()

### 总结

　总体来说ES6加入了很多新特性，来方便开发和使js代码更加规范和安全。个人推荐学习ES6后再学习Typescript，这样会更容易些，因为这些新特性在Typescript中都有，在以后的文章中我会再详细介绍 Typescript,"求机若渴，虚心若愚"，不要吝啬你的喜欢，发动小手点一点。

