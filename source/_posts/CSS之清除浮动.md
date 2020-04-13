---
title: CSS之清除浮动
date: 2017-4-22 20:06
tags: CSS
categories: 前端
summary_img: http://p4z3kz4fz.bkt.clouddn.com/boxmodel%20%281%29.png
---
### **1.什么是浮动**

**首先我们需要知道定位** 
元素在页面中的位置就是定位，解决问题之前我们先来了解下几种定位方式 
**1、普通流定位 static（默认方式）** 
普通流定位，又称为文档流定位，是页面元素的默认定位方式 
页面中的块级元素：按照从上到下的方式逐个排列 
页面中的行内元素：按照从左到右的方式逐个排列 

<!--more-->

但是如何让**多个块级元素在一行内显示?** 
这里就引出了浮动定位 
**2、浮动定位 float** 
float属性 取值为 left/right 
这个属性原本不是用来布局的，而是用来做文字环绕的，但是后来人们发现做布局也不错，就一直这么用了，甚至有些时候都忘了用他做文字环绕 
**3、相对定位 relative** 
元素会相对于它原来的位置偏移某个距离，改变元素位置后，元素原本的空间依然会被保留 
**语法** 
属性：position 
取值：relative 
配合着 偏移属性(top/right/bottom/left)实现位置的改变

**4、绝对定位 absolute** 
如果元素被设置为绝对定位的话，将具备以下几个特征 
1、脱离文档流-不占据页面空间 
2、通过偏移属性固定元素位置 
3、相对于 最近的已定位的**祖先元素**实现位置固定 
4、如果没有已定位**祖先元素**，那么就相对于最初的包含块(body,html)去实现位置的固定 
**语法** 
属性：position 
取值：absolute 
配合着 偏移属性(top/right/bottom/left)实现位置的固定

**5、固定定位 fixed** 
将元素固定在页面的某个位置处，不会随着滚动条而发生位置移动 
**语法** 
属性：position 
取值：fixed 
配合着 偏移属性(top/right/bottom/left)实现位置的固定

### **2.浮动的效果**

- **浮动 之后会怎么样？** 
  1、浮动定位元素会被排除在文档流之外-脱离文档流(不占据页面空间),其余的元素要上前补位 
  2、浮动元素会停靠在父元素的左边或右边，或停靠在其他已浮动元素的边缘上(元素只能在当前所在行浮动) 
  3、浮动元素依然位于父元素之内 
  4、浮动元素处理的问题-解决多个块级元素在一行内显示的问题 
  **注意** 
  1、一行内，显示不下所有的已浮动元素时，最后一个将换行 
  2、元素一旦浮动起来之后，那么宽度将变成自适应(宽度由内容决定) 
  3、元素一旦浮动起来之后，那么就将变成块级元素,尤其对行内元素，影响最大 
  块级元素：允许修改尺寸 
  行内元素：不允许修改尺寸 
  4、文本，行内元素，行内块元素时采用环绕的方式来排列的，是不会被浮动元素压在底下的，会巧妙的避开浮动元素
- **浮动 之后会有什么样的影响？** 
  由于浮动元素会脱离文档流，所以导致不占据页面空间，所以会对父元素高度带来一定影响。如果一个元素中包含的元素全部是浮动元素，那么该元素高度将变成0（高度塌陷）

### **3.如何清除浮动**

#### **解决方案 及 原理分析**

##### **方案1**

直接设置父元素的高度 
优势：极其简单 
弊端：必须要知道父元素高度是多少

##### **方案2**

在父元素中，追加空子元素，并设置其clear属性为both 
clear是css中专用于清除浮动的属性 
作用：清除当前元素前面的元素浮动所带来的影响 
取值： 
1、none 
默认值，不做任何清除浮动的操作 
2、left 
清除前面元素左浮动带来的影响 
3、right 
清除前面元素右浮动带来的影响 
4、both 
清除前面元素所有浮动带来的影响 
优势：代码量少 容易掌握 简单易懂 
弊端：会添加许多无意义的空标签，有违结构与表现的分离，不便于后期的维护

##### **方案3**

设置父元素浮动 
优势：简单，代码量少，没有结构和语义化问题 
弊端：对后续元素会有影响

##### **方案4**

为父元素设置overflow属性 
取值：hidden 或 auto 
优势：简单，代码量少 
弊端：如果有内容要溢出显示(弹出菜单)，也会被一同隐藏

##### **方案5**

父元素设置display:table 
优势：不影响结构与表现的分离，语义化正确，代码量少 
弊端：盒模型属性已经改变，会造成其他问题

##### **方案6**

使用内容生成的方式清除浮动

```css
.clearfix:after {
   content:""; 
   display: block; 
   clear:both; 
}12345
```

:after 选择器向选定的元素之后插入内容 
`content:"";` 生成内容为空 
`display: block;` 生成的元素以块级元素显示, 
`clear:both;` 清除前面元素浮动带来的影响 
相对于空标签闭合浮动的方法 
优势：不破坏文档结构，没有副作用 
弊端：代码量多

##### **方案7**

```css
.cf:before,.cf:after {
   content:"";
   display:table;
}
.cf:after { clear:both; }12345
```

优势：不破坏文档结构，没有副作用 
弊端： 代码量多 
注意：display:table本身无法触发BFC，但是它会产生匿名框(anonymous boxes)，而匿名框中的display:table-cell可以触发BFC，简单说就是，触发块级格式化上下文的是匿名框，而不是display:table。所以通过display:table和display:table-cell创建的BFC效果是不一样的（后面会说到BFC）。

> CSS2.1 表格模型中的元素，可能不会全部包含在除HTML之外的文档语言中。这时，那些“丢失”的元素会被模拟出来，从而使得表格模型能够正常工作。所有的表格元素将会自动在自身周围生成所需的匿名table对象，使其符合table/inline-table、table-row、table- cell的三层嵌套关系。

##### **疑问**

为什么会margin边距重叠？ 
overflow:hidden, 语义应该是溢出:隐藏，按道理说，子元素浮动了，但依然是在父元素里的，而父元素高度塌陷，高度为0了，子元素应该算是溢出了，为什么没有隐藏，反而撑开了父元素的高度？ 
为什么display:table也能清除浮动，原理是什么？

##### **解释**

要解释这些疑问，我们就要提到Formatting context 
Formatting context是W3C CSS2.1规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。 
最常见的Formatting context有Block fomatting context(简称BFC)和Inline formatting context(简称IFC)。 
CSS2.1 中只有BFC和IFC, CSS3中还增加了GFC和FFC 
**这里主要说BFC** 
BFC(Block formatting context)直译为”块级格式化上下文”。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。 
block-level box，display属性为block, list-item, table的元素，会生成block-level box。并且参与block fomatting context。 
inline-level box， display属性为inline, inline-block, inline-table的元素，会生成inline-level box。并且参与inline formatting context。 
**BFC布局规则：** 
1、内部的Box会在垂直方向，按照从上到下的方式逐个排列。 
2、Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠 
3、每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。 
4、BFC的区域不会与float box重叠。 
5、BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。 
6、计算BFC的高度时，浮动元素的高度也参与计算 
**触发BFC的条件** 
1、根元素 
2、float （left，right） 
3、overflow 除了visible 以外的值（hidden，auto，scroll ） 
4、display (table-cell，table-caption，inline-block) 
5、position（absolute，fixed） 
**举例详解BFC**

```css
<style>
   .top{
    width:100px;
    height:100px;
    background:red;
    margin:50px;
   }
   .bottom{
    width:100px;
    height:100px;
    background:blue;
    margin:20px;
   }
</style>
<body>
    <div class="top">上</div>
    <div class="bottom">下</div>
</body>
```

​							<img src="http://img.blog.csdn.net/20170403151130868?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRkVfZGV2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="">

依据BFC布局规则第二条：

Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠 
注意：发生重叠后，外边距的高度等于两个发生重叠的外边距的高度中的较大者

```html
<style>
   .top{
    width:100px;
    height:100px;
    background:red;
    float:left;
   }
   .bottom{
    width:200px;
    height:200px;
    background:blue;
   }
</style>
<body>
    <div class="top"></div>
    <div class="bottom"></div>
</body>
```
​	                                                       <img src="http://img.blog.csdn.net/20170403152150431?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRkVfZGV2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="">
依据BFC布局规则第三条：

每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。 
我们可以看到，虽然有浮动的元素top，但是bottom的左边依然与包含块的左边相接触。

```css
width:100px;
height:100px;
background:red;
float:left;<style>
   .top{
    width:100px;
    height:100px;
    background:red;
    float:left;
   }
   .bottom{
    width:200px;
    height:200px;
    background:blue;
    overflow:hidden;
   }
</style>
<body>
    <div class="top"></div>
    <div class="bottom"></div>
</body>
```
​								<img src="http://img.blog.csdn.net/20170403153221135?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRkVfZGV2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="">

依据BFC布局规则第四条：

BFC的区域不会与float box重叠。 
看代码和效果图，可以看出，这次的代码比上面的代码多了一行overflow:hidden;用这行代码触发新的BFC后，由于这个新的BFC不会与浮动的top重叠，所以bottom的位置改变了

```css
<style>
   p{
    width:100px;
    height:100px;
    background:red;
    float:left;
   }
   div{
    width:200px;
    border:1px solid blue;
   }
</style>
<body>
    <div>
       <p></p>
    </div>
</body>width:100px;
height:100px;
background:red;
float:left;
```
​										<img src="http://img.blog.csdn.net/20170403154832675?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRkVfZGV2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="">
当div增加 overflow:hidden; 时 效果如下 

​										![这里写图片描述](http://img.blog.csdn.net/20170403155037444?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRkVfZGV2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 
依据BFC布局规则第六条：

计算BFC的高度时，浮动元素的高度也参与计算。 
到此我们应该是解决了上面的所有疑问了。

总结
清除浮动的方式有很多种，但是实现的原理主要是靠clear属性，和触发新的BFC，通过详细的解释与比较，最后两种内容生成的方式是比较推荐使用的，如果需要考虑margin重叠的问题，就用方案7，不考虑就用方案6。

文章转载自[CSDN](http://blog.csdn.net/FE_dev/article/details/68954481)