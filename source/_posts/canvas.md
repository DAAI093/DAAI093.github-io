---
title: canvas
date: 2018-2-15 4:54
tags: canvas
categories: web
summary_img: http://p56w6hcyq.bkt.clouddn.com/canvas.gif
---
# canvas

## canvas画线条基本步骤

1. 编写canvas标签

   ```javascript
   <canvas>/<canvas>
   ```

2. 获取canvas的dom元素

   ```javascript
   var cas=document.querySelector("canvas");
   ```

3. 获取canvas的上下文对象(画笔)

   ```javascript
   var ctx=cas.getContext("2d");
   ```
   <!--more-->

4. 设置起点

   ```javascript
   ctx.moveTo(x,y);
   ```

5. 设置终点

   ```javascript
   ctx.lineTo(x,y);
   ```

6. 描边(连线)

   ```javascript
   ctx.stroke();
   ```

   ​

## 设置canvas的宽度和高度

1. 在css中直接设置宽度和高度 其实是拉伸
2. 在标签中通过属性的方式写宽度和高度(不叫做行内!!! )

## 注意点

1. 如果不写moveTo的话 那么lineTo 既是终点也是起点

2. 首尾相连:  

   1. 手动写lineTo
   2. ctx.closePath();

3. h5新标签

   1. color标签 一般结合 onchange一起使用

      ```html
      <input type="color" />
      ```

      > <input type="color" />

   2. number标签

      1. min 最小值
      2. max 最大值
      3. value 当前的值
      4. step 步长

      ```html
      <input type="number" min=0 max=10 value=0 step=1 >
      ```

      > <input type="number">

4. 操作数组的4个方法

   1. **原数组 arr=[a,b,c,d,e];**

   2. push 往屁股添加一个值 返回数组的长度  如: 

      > 6= arr.push(f)  arr= [a, b, c, d,e,f];

   3. pop   从屁股移除一个值 返回被删除的值 如: 

      > e= arr.pop()   arr=[a,b,c,d];

   4. unshift 从头部添加一个值 返回数组的长度如:

      > 6= arr.unshift(f)  arr=[f,a,b,c,d,e];

   5. shift 从头部删除一个值 返回被删除的值 如:

      > a= arr.shift()  arr=[b,c,d,e];

5. eval 方法 可以把字符串变成代码执行  不要在工作里面出现 

## stroke和fill

1. stroke 描边-对在同一条路径上的图形进行描边(封闭和不封闭)
2. fill 填充 对同一条路径上的**用线条画(不能填充strokeRect()的矩形)**的封闭图形进行填充

## 路径

1. 路径也是图形
2. 判断两个图形是否在同一条路径上 不能够靠视觉上的首尾相连来判断
3. 而是看有没有调用 ctx.beginPath();
4. 一般在画新图形之前,最好要 开启一条新的路径 

## 线条属性

1. 颜色

   > ctx.strokeStyle="red";
   >
   > ctx.fillStyle="red";

2. 宽度

   > ctx.lineWidth=10;

3. 线段末端类型

   1. miter 默认
   2. round 突出圆角
   3. square 突出矩形
   4. ctx.lineCap="miter";

4. 线段相交点的类型

   1. butt 屁股 默认值
   2. round 圆角
   3. bevel 平切
   4. ctx.lineJoin="butt";

5. 虚线

   1. setLineDash([实线的长度,实线的间隙的长度......])  设置虚线
   2. getLineDash() 获取虚线
   3. lineDashOffset=1 设置虚线的偏移值

## 内置画矩形和擦除

1. 画矩形 stokeRect(x,y,width.height)
2. 填充矩形 fillRect(x,y,width,height)
3. 擦除 clearRect(x,y,width,height)

## 内置画圆弧

1. 360 度=PI*2   
2. return  Math.PI/180* num
3. ctx.arc(圆心x,圆心y,半径,开始的**弧度**,结束的**弧度**,?是否反向)

## 内置 画图片

### 步骤:

```javascript
var img=new Image();
img.src="路径";
img.onload=function(){
  ctx.drawImage()......
}
```

### 方法解释

1. 3个参数  drawImage(图片对象,画在画布的x,画在画布的y);
2. 5个参数  drawImage(图片对象,画在画布的x,画在画布的y,画多宽,画多高);
3. 9个参数 drawImage(图片对象, 原图的x,原图的y,原图的宽,原图的高, 画在画布的x,画在画布的y,画多宽,画多高);

## 渐变

决定渐变图案的因素

1. 颜色
2. 方向
3. 长度

代码:

```javascript
var g=ctx.creatLinearGradient(开始的坐标x,y,结束的坐标x,y);
g.addColorStop(0,"red");
g.addColorStop(1,"black");
ctx.strokeStyle=g;
ctx.fillStyle=g;
ctx.fillRect(0,0,50,50);
```

## 文字

ctx.strokeText("文本",x,y);

ctx.fillText("文本",x,y);

ctx.font="50px 宋体"

> font的设置和在css中的设置一样

## 阴影

ctx.shadowBlur  模糊值

ctx.shadowColor 颜色

ctx.shadowOffsetX x 偏移

ctx.shadowOffsetY y 偏移

```javascript
  ctx.shadowBlur=10;
  ctx.shadowColor="red";
  ctx.shadowOffsetX=10;
  ctx.shadowOffsetY=10;
```

## canvas中的转换

### 移动

#### css3中的移动和canvas中的移动的区别

##### css3中的移动

1. 移动的是自身的dom元素
2. 移动的值 是覆盖的 先 translateX(100px) 再 tranlateX(200px) 最终的值 是 ranlateX(200px)
3. 移动的单位 一个 百分比 %  一个是像素 px 

##### canvas中的移动

1. 移动的是坐标系

2. 移动的值是叠加的  先 translateX(100px) 再 tranlateX(200px) 最终的值 是 ranlateX(300px)

3. 单位  不用写单位

   ```
   ctx.translate(1,1)
   ```

### 旋转

#### css3中的旋转和canvas中的旋转的区别

##### css3中的旋转

1. 旋转的自身的dom元素
2. 旋转的值 是覆盖的 
3. 单位 是  角度
4. 旋转的中心点 是元素的中心 center center

##### canvas中的旋转

1. 旋转的是坐标系
2. 旋转的值 是叠加的
3. 单位 是 弧度!!!! 
4. 旋转的中心点是坐标系的圆点 0 0 

```
 ctx.rotate(degToArc(10));
```

## 环境

环境 值 坐标系和线条属性 

### 保存和还原

保存的是 坐标系 和 线条属性

还原的是 坐标系 和 线条属性

保存了几次 就可以还原几次 

```
ctx.save()
ctx.restore();
```

### 擦除和重置

#### 擦除

ctx.clearRect(**0,0**,100,100)   有时候 坐标系改变了的话 再使用擦除这个代码  坐标不一定是 **0   0**  

不能擦除坐标系  不能擦除线条属性(颜色 大小 虚线 末端  相交🍌)

#### 重置

cas.width=cas.width  

可以擦除画图的图案  可以重置坐标系  可以重置线条属性  

## 下载

### 标签实现

```html
<a href="资源路径" download="资源名字(可以随便写)" ></a>
```

### 代码实现

```
// 1 创建a标签
var aDom=document.createElement("a");
// 2 指定 href
aDom.href="资源路径";
// 3 设置download属性
aDom.download="五年高考";
// 4 手动触发 a标签的点击行为
aDom.click();//它是个方法 不是 事件 
```

## 画布保存和下载

### 获取canvas画布的路径 cas.toDataURL()

#### cas.ToDataURL(图片类型,质量)

##### 图片类型

1. image/png
   1. 默认值 即 cas.toDataURL() 既可以
   2. 不能压缩
2. image/jpeg
   1. 可以压缩  
   2. 默认会把透明背景填充成黑色
   3. 建议在使用它的时候 先手动fill 画布 成白色

##### 质量(0-1) 0 最低 1 最高

## 画视频

将video标签传入 ctx.drawImage(video,0,0) 即可 参数和 之前画图片的一样

### 在线视频截图下载

报错: `Uncaught DOMException: Failed to execute 'toDataURL' on 'HTMLCanvasElement': Tainted canvases may not be exported.`

解决:**以服务器的形式打开即可**



## 和canvas相关的技术

1. echartjs
   1. 百度 数据展示 文档详细 基于配置
2. konvajs
   1. 国外 自定义图形 类jq和js的关系
3. three.js
   1. 国外 3d模拟 门槛高 电脑性能要求高
4. d3.js
   1. 国外 大数据 门槛中 数据分析

# 移动web

## 失真

### 原因

图片的清晰度和设备的清晰度不一致

### 解决方案:

1. 不用解决 忍受 模糊 

2. 全部高清图 最常用 

3. srcset 设备像素比的方式 devicePixelRatio  

   ```html
   <img src="./images/科比.png" srcset="./images/赵丽颖.png 2x,./images/高圆圆.png 3x" alt="">
   ```

   ​

## 基本概念

1. 逻辑分辨率:屏幕的宽和高 单位 是px  
2. 设备分辨率:屏幕里面一共拥有的物理像素点的个数!!!
3. 对角线:一般说的手机屏幕尺寸都是指对角线的长度 单位 是英寸 
4. PPI (Pixels Per Inch)也叫像素密度，所表示的是每英寸所拥有的像素数量 值越高,越清晰



## 视口

### 布局视口

被手机厂商设置宽度为980px的视口

### 理想视口

视口宽度和屏幕等宽并且使用绝对长度单位写元素大小 是固定

在代码里面如何写处理

` meta:vp+tab` 

#### 不标准的

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

#### 标准的写法

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1,minimum-scale=1,user-scalable=no">
```



## less

### 编译工具

#### 考拉

##### 注意事项

1. 需要将 整个 **css文件夹**  都拖放到考拉当中
2. 存放less文件的文件夹的名字不能够包含 **less** 字段
3. 新创建less文件的时候 需要手动点击一下 考拉 里面的刷新按钮 **reflash**

#### vs code 中的插件 easyless

直接在vs code中下载 启用即可  

### 语法:

#### 变量

```less
@myColor:red;
body{
  color:@myColor;
}
```

#### 函数

```less
// 不带参数的函数
.changeColor1(){
  color:red;
}
body{
  .changeColor1();
}
// 带参数的函数
.changeColor2(@c){
  color:@c;
}
body{
  .changeColor2(red);
}
// 带默认参数的函数
.changeColor3(@c:black){
  color:@c;
}
body{
  .changeColor3();// color:black;
  .changeColor3(red);// color:red;
}
```

​

#### 嵌套

```less
div{
  &:after{}
  p{}
  >section{}
}
```

​

#### 导入

```less
@import "base.less";
```

​

#### 注释

```less
// 这种注释不会被编译到css中
/* 这种注释会被编译到css中 */
```

### 真机调试

ghostlab

[云真机](http://wetest.qq.com/cloud/index.php/help/cloudindex)

工作中如何对待:

1 公司里面有测试 开发者的只要确保在 模拟器上 没有bug 就可以了.

2 大公司里 有第三方的测试团队去测试  

3 小小的公司  公司人少 只能够自己去测试 (再去研究真机调试的步骤)

5 在学习的时候 可以先不用管真机调试 .以后用到的时候再去搭建环境和步骤就可以 了 !!! 



## 触屏事件

### 触屏事件的种类

touchstart  手指按下屏幕

touchemove  手指在屏幕上滑动

touchend 手指离开屏幕

### 三个触摸点数组

touches  屏幕上所有的触摸点的集合

targetTouches 目标元素上的触摸点的集合

changedTouches 在目标元素上发生了状态改变(进入 离开 移动)的触摸点的集合

### 三对坐标信息

clientX/Y 相对于视口的坐标

pageX/Y 相对于页面的坐标

screenX/Y 相对屏幕的坐标

### 触屏事件的注意点

#### 需求:

1. 鼠标事件不能模拟多指触控
2. click点击事件在移动端存在延迟
   1. 原因  手机厂商为了用户更方便的放大页面
   2. 延迟机制:
      1. 第一次点击后,先等待一段时间 这一段时间过后 
         1. 判断有没有第二次的点击发生 有 触发双击放大
         2. 没有的再触发单击
      2. 不管有没有第二次的点击 都需要等待 -  延迟
3. 触屏事件不能在pc端上触发
4. 建议绑定事件的时候 用 addEventListener  来绑定  

#### 手势封装tap

判断依据:

1. 手指个数不能超过1
2. 按下时间不能超过300ms
3. 滑动距离不能超过5px

#### 手势封装swipe

判断依据:

1. 手指个数不能超过1
2. 按下时间不能超过800ms
3. 滑动距离不能小于15px

### 京东轮播图

#### 过渡结束事件

transitionend 每一次过渡结束的时候 都会触发一次

### 移动端轮播图插件 swiper.js

我们使用的版本是3.x版本

使用教程看官网即可 

[网站](http://www.swiper.com.cn/)

### vs code 插件

1 安装 ease Server 插件 (同步刷新功能)

2 在当前的html页面中 输入 `ctrl+shift+enter`

### 自己构建zepto

1 先安装好 **nodejs**   在cmd中输入 `node -v`  如果出现了版本号 证明安装成功了 

2 在zepto文件夹内 按下 `shift+鼠标右键` 弹出命令行窗口

3 输入 `npm install `

4 执行编译 `npm run-script dist`

5 自己设置要编译的模块 `SET MODULES=zepto event data touch`  

6 执行编译 `npm run-script dist`



# 响应式布局

## 概念:

用一套代码 可以做一个适应不同宽度的设备,还可以提供比较友好的用户体验

## 核心原理:

媒体查询

## 媒体查询

一种css的语法,可以根据设备的不同(主要是宽度),去加载对应的css代码

## 媒体查询的知识点

### 媒体类型

1. all 包括一下两个类型
2. screen 带正常屏幕的设备
3. print 打印机

### 媒体特性

1. 宽度

2. 高度

3. 视口的宽高比      

   ```
   // 2/1 不能改为  2
   @media screen and (aspect-ratio:2/1){
     body{
       
     }
   }
   ```

### 媒体关键字

1. and
2. or 代码中写逗号 来体现
3. not 取反
4. only 用来做兼容 

### 媒体查询的引入方式

1. **在css(和一般的样式代码是同层级)中直接写媒体查询-用得最多**
2. 在style标签上 通过属性的方式 
3. 在link标签上 通过属性的方式 

## bootstrap框架

## 栅格系统

是把所有屏幕(4种屏幕) 分成了12份 每一列占一份

### 4种宽度不同的屏幕

1. 极小屏幕  xs < 768px
2. 小屏幕  sm   768-992
3. 中等-普通屏幕   md   992-1200
4. 大屏幕  lg  > 1200

### 步骤:

1. 先写容器 .container(版心的宽度)  .container-fluid (全屏)
2. 写 .row
3. 再去写栅格(要注意标明屏幕的种类)

## 工具提示

用法:

1. 直接粘贴标签的代码
2. 必须要写上一段初始化的js代码 

## 微金所

### 知识点

### a标签不能嵌套a标签

### nth-child和nth-of-type的区别

1. nth-child 计算子元素索引的时候 会计算其他类型的标签
2. nth-of-type 计算子元素的索引的时候 不会计算其他类型的标签

### 列嵌套-有时候代码怎么简单怎么写

### 在做大的布局的时候容器的时候 建议使用 块级元素 (千万不要写行内嵌套块级元素)



# rem+媒体查询 布局

## rem和px和em的区别

1. px是绝对长度单位
2. em是相对长度单位 相对于自身的fontsize
   1. 谷歌浏览器默认字体是16px
   2. 谷歌浏览器默认最小字体是12px
3. rem 是相对长度单位  相对于html标签的fontsize

## 实现屏幕适配的步骤

1. 使用rem+媒体查询还原设计稿
2. 使用rem+媒体查询去做屏幕适配

## 适配的注意事项

1. 基础值 和设计稿等宽的媒体查询里面的html标签的fontsize  为100px
2. 写100px 是为了方便计算
3. 公式: `fontsize=基础值*要适配的屏幕/设计稿的宽度`
4. 不建议使用js来代替媒体查询的功能
5. 任何宽度的设计稿都可以用这套解决方案
6. pc端的滚动条占宽度 移动端的滚动条不占宽度

## 在线工具

[标你妹](http://www.biaonimeia.com/project)

[px转rem工具](http://mxd.tencent.com/wp-content/uploads/2014/11/rem.html)

# 开发技巧

## less和souce map

### souce map

存放了less文件和css文件的映射关系

### 作用

可以从页面调试工具里面 直接映射会对应的less文件

### 步骤:

1. 使用工具创建souce map (考拉 vs code中插件 easyless)

   1. 考拉

   2. easyless 插件

      1. 需要在vs code 的设置中 加入以下代码 就可以了 

         ```
         "less.compile": {
                 "sourceMap": true  // true => generate source maps (.css.map files)
             },
         ```

   3. 需要在谷歌浏览器中开启

      ​

      ​