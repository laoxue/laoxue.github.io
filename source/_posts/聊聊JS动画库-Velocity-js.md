---
title: '聊聊JS动画库:Velocity.js'
date: 2021-08-13 11:37:31
tags:
    - javascript
categoroes:
    - 前端技术
keywords: "Velocity||JS动画||JS库"
description: 
top_img:
cover: https://www.theengineeringprojects.com/wp-content/uploads/2021/05/what-is-velocity.png
---

![Javascript动画](http://img5.imgtn.bdimg.com/it/u=4235123183,3168817216&fm=26&gp=0.jpg)
### 前言

  又到了炎热的7月，很久没有更新技术文章了，原因是上月月底实习结束，从公司离职。然后最近在弄自己的项目和考驾照，为了下次公司的应聘做准备，送别了女朋友到外地，哩哩啦啦半个月把一切事情都办妥后，还是静下心来学习新技术和写一写技术文章，希望能继续坚持下去吧。
  
#### JS动画

  随着互联网越来越丰富多样，网页端的美化和新技术层出不穷，作为一个网站的浏览者，更多吸引他们的除了保证网站的流畅之外还有各种炫酷的交互动效。

  网页的交互动效大概分为 `css动画`，`js动画` 。

#### JS动画的优点

  既然我们大概了解了这两类动画，那么我们来分析下他们不同的优点

  + css动画 由于css3可以根据css属性自定义动画 所以这类动画的优点就是不用进行计算和更改dom 会显得非常流畅。
  + JS动画 js动画拥有强大的性能，并且优于css动画的特点就是 既然是根据js来改变属性值 所以没有css那样的局限性，可以实现更多的功能和动效，或许有人说js动画某些库会很慢，其实js动画本质很快，只是jquery让它慢了下来。因为有时候由于配合jquery使用，所以由于jquery本身的一些功能，所以在实现的时候就会显得很慢。
  
#### velocity.js 使用方法

  JS动画的库非常多，各有各的有点，比如jquery自带的animate动画还有 webGL,或者利用canvas，SVG等实现其他效果，本次来讲的就是众多库中的其中一个 `velocity.js` 动画库。

  velocity.js 既可以单独用JavaScript使用，也可以配合jquery使用，使用方法(**注意先将velocity.js下载好后在body标签下引入，然后在新script标签中书写以下代码**) ：
  

  	//jquery方法 
  	var $div = $('div')
  	$div.velocity({属性:值,属性:值})
  	//javascript 方法
  	var oDiv = document.getElementById('div')
  	oDiv.velocity({属性:值,属性:值})

这里需要注意得几点：

1.里面的属性不能加引号写入，而后面的值如果有字符串则加引号，如果为整数则不用 比如 width:100 和 width："100px"
2.里面的属性值不可一次传入多个，比如在css中 padding:5px 5px 6px 5px;我们可以这样传入 但是在velocity中如果想传入多个值则为 {paddingLeft：5, paddingRirght:5 省略} 
3.里面的属性值 如果是多个转折的需要第二个`首字母大写` 如上

#### velocity.js 详细介绍

上面已经讲到 需要改变的值作为对象传入velocity的第一个参数，那么第二个参数就是 它的`指定动画选项`包含：
	
	+ duration 持续时间
	+ easing 缓动方式
	+ delay 延迟执行
	+ loop 循环次数
	+ begin 和 complete 回调函数
	+ display(值与css相同，可设置为auto)

在讲velocity指定动画选项前 我们先说一下velocity支持的值: px em rem % vm vh 或者 利用运算符 *=2 表示当前值的2倍 或者 /=2 等运算方式

下面一个一个分析下指定动画选项：

#### duration 持续时间 

这个是代表动画的持续时间默认值为`毫秒(ms)` 你可以这样使用：
	
	// 表示一秒内将透明度从1到0
	$div.velocity({opacity:0},{duration:1000})

也可以这样使用:
	
	// 效果相同
	$div.velocity({opacity:0},1000)

velocity也自定了三种持续方式：`slow（600ms)` ,`normal（400ms）`,`fast(200ms)`,可根据自己实际需求使用

#### easing 缓动方式

这个是代表着动画以何种方式进行变换：`ease-in-out(逐加逐减)`,`ease-in (先加速后匀速)`,`dase-out (先匀速后减速)`

也可以根据 `三角函数缓动` "easeInOutSine" ，`css贝塞尔曲线`[0.17,0.67,0.83,0.67] 或者`弹簧物理` [张力，摩擦力] 等值进行实现

#### delay 延迟执行

表示这个动画`延迟多少时间执行` 默认单位毫秒(ms)

	// 五秒后执行此动画
	delay：5000

#### loop 循环次数 

表示这个动画需要的`循环次数`:

	// 循环五次
	loop:5
	// 无限循环
	loop:true 

#### begin和complete回调函数

这两个表示在动画开始前和动画结束后所执行的函数：

	begin:function(){ somgthing... },complete:function(){ somgthing... }

#### 其他功能：

velocity还有一些其他功能，这里就日后再说，比如：`reverse(反转)`，`scrolling(滚动)`，`color(颜色)`，`transform(变换` 包含`scale缩放` `rotate旋转` `translation平移`等)

#### 结语

总之前端技术现在层出不穷，作为程序员的我们更应学习一些新的技术，既然热爱，就永无止境，我日后还会分享一些技术文章，纯自己个人总结，也当做个人技术笔记，如果喜欢，不妨关注，哪里有错，私信给我，我会即是更改，希望能同大家一同进步。