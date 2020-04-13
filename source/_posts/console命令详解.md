---
title: console命令详解
date: 2017-6-03 16:11
tags: console
categories: 工具
summary_img: http://p56w6hcyq.bkt.clouddn.com/H5.jpg
---
熟悉前端的不会对console和alert陌生，两者在调试的时候可谓是法宝级别的工具，但是关于console，其实远远不止于console.log这一个简单的命令，它能做的事情有很多，那么让我们慢慢了解一下，它有哪些功能吧。

<!--more-->

### 一、显示信息的命令

​	最常用的就是console.log，查看效果的方法：如果是Chrome浏览器，就打开“开发者工具”，按快捷键“Ctrl+F12”，或者右键点击页面，选择“检查”菜单。然后在“Console”面板可以查看输出结果。

​        	![p1](http://hovertree.com/hvtimg/bjafaa/ba2y5r8i.png)

​	如果是火狐浏览器的话，按组合键“Ctrl+Shift+K”可以打开“网页控制台”。

![p2](http://hovertree.com/hvtimg/bjafaa/vi8de0vc.png)

​	示例代码：

```HTML
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/><meta name="viewport" content="width=device-width, initial-scale=1" />
<title>常用console命令之显示信息_何问起</title><base target="_blank" />
<meta charset="utf-8" />
<style>a{color:blue;}</style>
</head>
<body>
<div>常用console命令之显示信息，请查看浏览器的console面板。

<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a>
</div>
<script type="text/javascript">
console.log('hello hovertree');
console.info('信息 何问起');
console.error('错误');
console.warn('警告');
</script>
</body>
</html>

```

### 二：占位符

​	console上述的集中度支持printf的占位符格式，支持的占位符有：字符（%s）、整数（%d或%i）、浮点数（%f）和对象（%o）

​	代码如图：

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>console命令之占位符何问起</title><base target="blank" />
<meta charset="utf-8" />
<style>a{color:blue;}</style>
</head>
<body>
<div>console命令之占位符 说明
首页</div>
<script type="text/javascript">
console.log("%d年%d月%d日",2016,11,11);
</script>
</body>
</html>
```

​	效果如图：

![p3](http://hovertree.com/hvtimg/bjafaa/ni4dheny.png)

### 三、信息分组

​	示例代码：

```HTML
<!DOCTYPE html>
<html>
<head><meta name="viewport" content="width=device-width, initial-scale=1" />
<title>常用console命令_何问起</title><base target="_blank" />
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<style>a{color:blue;}</style>
</head>
<body>
<div>常用console命令之信息分组
<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a>
</div>
<script type="text/javascript">
console.group("第一组信息");
console.log("第一组第一条:何问起(http://hovertree.com)");
console.log("第一组第二条:柯乐义(http://keleyi.com)");
console.groupEnd();
console.group("第二组信息");
console.log("第二组第一条:HoverClock 一个jQuery时钟插件");
console.log("第二组第二条:欢迎使用");
console.groupEnd();
</script>
</body>
</html>
```

​	效果如图：

​	![p4](http://hovertree.com/hvtimg/bjafaa/s8l7eslm.png)

### 四、查看对象的信息

​	console.dir()可以显示一个对象所有的属性和方法。

​	示例代码：

```html
<!DOCTYPE html>
<html>
<head><meta name="viewport" content="width=device-width, initial-scale=1" />
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<title>用console.dir方法查看对象信息_何问起</title><base target="_blank" />
<meta charset="utf-8" />
<style>a{color:blue;}</style>
</head>
<body>
<div>
用console.dir方法查看对象信息
<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a>
</div>
<script type="text/javascript">
var info = {
blog:"http://hovertree.com",
时钟插件:"HoverClock",
message:"欢迎使用！"
};
console.dir(info);
</script>
</body>
</html>
```

​	效果图：

​	![p5](http://hovertree.com/hvtimg/bjafaa/hdal6y82.png)

### 五、显示某个节点的内容

​	console.dirxml()用来显示网页的某个节点（node）所包含的html/xml代码。

​	示例代码：

```html
<!DOCTYPE html>
<html>
<head><meta name="viewport" content="width=device-width, initial-scale=1" />
<title>常用console命令_何问起</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" /><base target="_blank" />
<style>a{color:blue;}</style>
</head>
<body>
<div>
console.dirxml()用来显示网页的某个节点（node）所包含的html/xml代码
<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a>
</div>
<div id="info">
<h3>我的博客：hovertree.com</h3>
<p>HoverTreeImg插件,欢迎使用</p>
</div>
<script type="text/javascript">
var info = document.getElementById('info');
console.dirxml(info);
</script>
</body>
</html>
```

​	效果图：

![p6](http://hovertree.com/hvtimg/bjafaa/s54ts251.png)

### 六、判断变量是否是真

​	console.assert()用来判断一个表达式或变量是否为真。如果结果为否，则在控制台输出一条相应信息，并且抛出一个异常。

​	示例代码：

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>console.assert使用_何问起</title><base target="_blank" />
<meta charset="utf-8" />
<style>a{color:blue;}</style>
</head>
<body>
<div>
console.assert方法的使用
<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a>
</div>
<script type="text/javascript">
var result = 1;
console.assert( result );
var year = 2014;
console.assert(year == 2018 );
</script>
</body>
</html>
```

​	效果图：

![p7](http://hovertree.com/hvtimg/bjafaa/ck69uec4.png)

### 七、追踪函数的调用轨迹。

​	console.trace()用来追踪函数的调用轨迹。

​	示例代码：

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>追踪函数的调用轨迹_何问起</title><base target="_blank" />
<meta charset="utf-8" />
<style>a{color:blue;}</style>
</head>
<body>
<div>javascript中console.trace()方法示例
<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a></div>
<script type="text/javascript">
/*函数是如何被调用的，在其中加入console.trace()方法就可以了 -- 何问起*/
function add(a,b){
console.trace();
return a+b;
}
var x = add3(1,1);
function add3(a,b){return add2(a,b);}
function add2(a,b){return add1(a,b);}
function add1(a,b){return add(a,b);}
</script>
</body>
</html>
```

​	效果图：

![p8](http://hovertree.com/hvtimg/bjafaa/7rvtay5j.png)

### 八、计时功能

​	console.time()和console.timeEnd()，用来显示代码的运行时间。

​	示例代码：

```HTML
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>显示代码的运行时间_何问起</title><base target="_blank" />
<meta charset="utf-8" />
</head>
<body>
<div>console.time()和console.timeEnd()，用来显示代码的运行时间。
<a href="http://hovertree.com/h/bjaf/gk6698g3.htm">说明</a>
<a href="http://hovertree.com">首页</a></div>
<script type="text/javascript">
console.time("控制台计时器一");
for(var i=0;i<10000;i++){
for(var j=0;j<1000;j++){}
}
console.timeEnd("控制台计时器一");
</script>
</body>
</html>
```



​	效果图：

![p9](http://hovertree.com/hvtimg/bjafaa/qqd99k71.png)



本文转载自[云栖社区](https://yq.aliyun.com/articles/68438)