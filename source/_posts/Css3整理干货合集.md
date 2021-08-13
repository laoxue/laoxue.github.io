---
title: Css3整理干货合集
date: 2021-08-13 11:34:25
tags:
    - CSS
categoroes:
    - 笔记
keywords: "Css3整理干货合集||CSS||教学"
description: 
top_img:
cover: http://upload-images.jianshu.io/upload_images/3612487-2a72179c9ccffc6f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

###### **前言:** 
![](http://upload-images.jianshu.io/upload_images/3612487-2a72179c9ccffc6f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
把以前的手写笔记整理到`博客`中...
***
>### css3边框：

	border-radius 圆角
	border-image 边背景图
	box-shadow 阴影

>#### border-radius圆角

设置百分比或者值px都可以 50% 为正圆 一个值为默认设置所有边角 四个值代表设置四个边角

>#### box-shadow 阴影


设置`四个值` 按顺序分别是 

>`offset-x` 代表x轴偏移值 值为正则代表右侧，负代表左侧

![](http://upload-images.jianshu.io/upload_images/3612487-b78cfb8c1147e57d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>`offset-y` 代表y轴偏移值
值为正则代表上方，负代表下方

![](http://upload-images.jianshu.io/upload_images/3612487-6d9440de122ac4d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>`blur` 代表阴影的模糊半径
值越大则越模糊 负值不合法

![](http://upload-images.jianshu.io/upload_images/3612487-7311ce605579fc5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>`color` 代表模糊的颜色 可设置**red**或者**#f1f1f1**或者**rgba**等类型值

>`多重阴影` 一个div上可以添加多个阴影效果，方法只需把添加的效果用 **逗号** 隔开即可

![](http://upload-images.jianshu.io/upload_images/3612487-e0ee8ed439513a0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

参考文章:[http://www.iyangqiong.com/web/318.html](http://www.iyangqiong.com/web/318.html)

>#### border-image边角背景图

`三个值` 第一个是`url(文件路径)` 第二个是`裁剪位置(默认像素`) 第三个是`重复性`
这个一定程度赶上跟`border宽度`上有关系

>border-image: <‘border-image-source’> || <‘border-image-slice’> [ / <‘border-image-width’> | /

### css3背景

	backgournd-image
	background-size
	background-origin
	background-clip

#### background-image 

可添加多个背景图 用 **逗号** 相隔
对应 **background-position** **background-repeat** 设置背景图的位置和重复

#### background-size 

可指定`background-size` 为背景图片设置大小
可设置宽和高

#### background-origin

指定了背景图的位置区域 三个值对应区域如图

![](http://upload-images.jianshu.io/upload_images/3612487-663da47160b908bc.gif?imageMogr2/auto-orient/strip)

#### background-clip

这个属性是指从指定位置开始绘制 三个值跟上边的一样

>### css3渐变

分两种渐变：`线性渐变（Linear Gradients）`- 向下/向上/向左/向右/对角方向和`径向渐变（Radial Gradients）`- 由它们的中心定义

也就是一个是从`一边到另一边` 一个是从`中间到四周`的方式渐变

>##### 首先linear-gradient 线形渐变(默认从上到下)

	background: linear-gradient(direction, color-stop1, color-stop2, ...);
	direction值可为开始方向也可为角度deg 后面是开始颜色和结束颜色(可为rgba也可为多个颜色值)
	repeating-linear-gradient()重复性渐变

>##### 然后radial-gradient 线形渐变(四周向外扩)

	background: radial-gradient(center, shape size, start-color, ..., last-color);
	分别代表 渐变中心(默认center)，形状，大小，开始颜色，结束颜色


>### css3文本效果

	text-shadow
	box-shadow 
	text-overflow
	word-wrap
	word-break

>##### text-shadow 文本阴影

	text-shadow:四个值 如同 box-shadow

>##### text-soverflow 文本溢出

	text-overflow: 一个值 两个内容
	elipsis 溢出裁剪省略号  clip溢出裁剪

>##### word-wrap 文本换行

	word-wrap:break-word;强制自动换行

>##### word-break 文本拆分换行

	word-break:一个值 两个内容
	keep-all 保持单词完整 break-all 保持每行够满字符

>### @font-face自定义字体

	@font-face{
    //自定义字体名字
    font-family:name;
    src:url('字体文件.ttf'),
    //ie9专用字体
    url('字体文件.eot');
    //使用粗体文本
    font-weight:bold;
    }

使用的时候`font-family：`自定义名字

## 动画相关

### css3 2d转换 **transform:**

	translate()
	rotate()  旋转
	scale()  缩放
	skew()
	matrix()

#### translate() 位移

	transform:translate(x,y) 
	两个值 x正即向右移动，负值即是向左移动 y正向上负向下
	也可单独位移 **translateX(n)**  **translateY(n)**

#### rotate() 旋转

	rotate(deg) 正是准时针负是逆时针

#### scale() 缩放

	scale(x,y) x是宽度x倍   y是长度y倍
	也可单独缩放 **scaleX(n)**  **scaleY(n)**

####　skew() 倾斜

	skew(deg,deg) 表示向x轴和y轴倾斜的方向
	也可单独倾斜 **　skewX(n)**  **　skewY(n)**

#### matrix() 集合

	matrix(位移，旋转，缩放，倾斜)表示所有transform的集合都可以写在这里

### css3 3d转换 改变xyz轴实现效果

	matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n)定义 3D 转换，使用 16 个值的 4x4 矩阵。

	translate3d(x,y,z)定义 3D 转化

	translateX(x)定义 3D 转化，仅使用用于 X 轴的值

	translateY(y)定义 3D 转化，仅使用用于 Y 轴的值

	translateZ(z)定义 3D 转化，仅使用用于 Z 轴的值

	scale3d(x,y,z)定义 3D 缩放转换

	scaleX(x)定义 3D 缩放转换，通过给定一个 X 轴的值

	scaleY(y)定义 3D 缩放转换，通过给定一个 Y 轴的值

	scaleZ(z)定义 3D 缩放转换，通过给定一个 Z 轴的值

	rotate3d(x,y,z,angle)定义 3D 旋转

	rotateX(angle)	定义沿 X 轴的 3D 旋转。

	rotateY(angle)定义沿 Y 轴的 3D 旋转。

	rotateZ(angle)定义沿 Z 轴的 3D 旋转 

	perspective(n)	定义 3D 转换元素的透视视图

### CSS3 过渡

	transition 总集合用于在一个属性中设置四个过渡属性。
	transition: p(名称) d(花费时间) f(时间曲线) d(何时开始) 
	transition-delay 规定过渡效果何时开始。默认是 0。
	transition-duration 定义过渡效果花费的时间。默认是 0
	transition-property 规定应用过渡的 CSS 属性的名称
	transition-timing-function 	规定过渡效果的时间曲线。默认是 "ease"

### CSS3 动画

	@feyframes规则
	animation

1.首先使用@keyframes创建动画 把它绑定到一个选择器。否则动画不会有效果

	+ 规定动画的名称
	+ 规定动画的时长

2.然后用 animation 动画捆绑到div元素

	animation是一个综合简写属性(除animation-play-state) 分开分别是
	animation-name 	规定 @keyframes 动画的名称。
	animation-duration 	规定动画完成一个周期所花费的秒或毫秒。默认是 0。规定动画完成一个周期所花费的秒或毫秒。默认是 0。
	animation-timing-function 规定动画的速度曲线。默认是 "ease"。
	animation-delay 规定动画何时开始。默认是 0。
	animation-iteration-count 	规定动画被播放的次数。默认是 1。
	animation-direction 	规定动画是否在下一周期逆向地播放。默认是 "normal"。
	animation-play-state 	规定动画是否正在运行或暂停。默认是 "running

###