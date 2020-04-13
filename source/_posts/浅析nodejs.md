---
title: 浅析node
date: 2018-2-13 10:54
tags: node
categories: node
summary_img: http://p56w6hcyq.bkt.clouddn.com/node.jpg
---
学习Node.js时候的建议

1. 前端和后端的知识体系不同！不要使用前端的思维方式去学习后端开发！

2. 学习Node.js阶段，把自己当作后端开发人员！

3. 课堂上对重点的知识做笔记，利用一切时间练习课堂代码；晚上抽半个小时梳理总结今天所学知识点；整理今天的笔记！

4. 每天吃饭睡觉走大街上，都要在脑海中闪现今天学习的知识点【×××知识点是什么，怎么用】

   <!--more-->


什么是前端和后端

1. 前端主要工作：写页面（HTML）、美化页面（CSS）、调用后台提供的API接口去请求或提交数据（JS）；Ajax （XHR、Jquery  .ajax  .get  $.post），Jquery更多的是进行DOM方面的操作！H5C3，高级、Angular（单页面应用程序）

- 前端主要在浏览器端进行开发；前端主要和页面打交道，用户看到的基本上就是我们前端写出来的（前端就是颜值）

1. 后端主要工作：主要进行业务逻辑的操作、比如数据的增删改查、操作数据库、对外暴露API接口（后台是骨骼、灵魂）
2. 前后端协作流程：前端写页面，前端调用后台的接口；后台接受前端发过来的请求，然后进行相关的业务处理，把处理的结果返回给前端（提供API接口）

Javascript 的起源

1. 诞生：JS的诞生和一个公司有关，有一个网景公司；当时网速只有20~30KB（电话线），当时，就是为了进行客户端验证，为了减少不必要的网络请求，提高网络效率，网景公司决定研究一门语言，来解决这个问题；JS作者在10之内，就把这门语言写出来了，叫做LiveScript，为了搭上Java这般顺风车，就把LiveScript改名为Javascript；
2. 浏览器中的一战：微软发现浏览器市场很火，然后就自己开发了一款浏览器【IE】；为了推广自己的IE浏览器，把IE捆绑到了Windows操作系统中；JScript

- 一战胜利的果实：ECMAScript标准的确立；就是一个语言规范；只规定了如何进行分支判断、如何定义变量、如何定义方法.....

1. 短暂的和平期：IE6【微软发现自己已经天下无敌了，然后就把IE6的开发团队给解散了！】在和平期间，JS这门语言主要做什么：表单验证、简单的特效、狗皮膏药（当时被称为脚本语言）
2. 二战：【主角：谷歌、IE、火（浴火重生）狐】谷歌在2008年，借助于AJax，开始火起来了！一方面提升渲染引擎的效率、另一方面，提升JS解析引擎的效率，最终，二战以谷歌的胜利结束；谷歌有了一款世界上效率最快的JS解析引擎，叫做chrome V8引擎；

Node.js 的起源

nodejs的历史由来

- 作者，之前主要是做高性能服务器维护的；高性能的服务器有哪些必要的条件；必须要是异步非阻塞的、基于事件驱动的；
- 作者在分析了上面两条基本条件之后，就开始研发高性能服务器！
- C,C++,Java,C#,Javascript
- 对于程序员来说，如果同时提供了同步和异步两种编程方式，程序员肯定会选择同步；
- 作者选择Javascript最主要的原因，就是这门语言是单线程的
- 多线程：程序员能主动开启子线程的语言，就叫做多线程的语言；Thread td = new Thread();
- 作者最终，选择的语言是Javascript、解析引擎是V8；
- 刚开始，作者写出来的这个东西叫做web.js;后来，随着项目扩大和功能的完善，作者发现这款产品，不仅能做高性能的服务器，还能做许多事情，比如可以用这个东西去做前端包管理；于是就改名叫做Node.js;
- 像前端需要好用的工具，都是使用node.js开发出来的！

ECMAScript、浏览器中的Javascript、Node中的Javascript

- ECMAScript：语言规范；不能使用ECMAScript进行实际的编程，因为它只是一个语言标准而已；
- 浏览器中的Javascript：是ECMAScript这个规范的具体实现；我们可以使用浏览器中的JS进行实际的编程！

- 浏览器中的Javascript组成部分：DOM + BOM + ECMAScript；其中，DOM和BOM和规范无关，是浏览器根据自己的需要，后期扩展的；

- Node中的Javascript：是ECMAScript这个规范的具体实现；也能进行实际的编程！

- Node中的Javascript组成部分：ECMAScript + 核心API + 其他第三方API，由于Node不需要操作浏览器对象和文档对象，所以把BOM和DOM给剔除了！核心API中，提供了 操作 文件的API 和 操作网络的 API等。。。。

什么是Node.js

- Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

- 我们使用JS写的Node代码，说白了，只是单纯的字符串而已；
- 如果想要执行这些写好的代码，必须要有一个解析执行环境，这个环境就是chrome 的 V8 引擎；

- Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。

- 事件驱动：当触发某个事件的时候，执行事件中指定的代码！
- 非阻塞式 I/O 的模型：采用非阻塞的操作，能够提高处理的效率！

- Node.js 的包管理器 npm，是全球最大的开源库生态系统。

- 先使用npm init -y初始化一下包管理文件package.json，将来所有安装的包，都会记录到这个文件中
- 使用npm install 包名 --save/--save-dev去安装包；其中，install可以简写成i;
- --save表示把包安装到部署依赖中（在开发和部署上线都需要使用的包）； --save-dev表示安装到开发依赖（只在项目开发阶段需要用到的包）；
- --save可以简写成-S；--save-dev可以简写成-D;
- npm uninstall 包名 --save/--save-dev或者npm remove 包名 --save/--save-dev
- npm i webpack -g,其中，-g表示全局安装某些包，通过-g安装的包都在C:\Users\用户名\AppData\Roaming\npm下面

- NPM 和 （Github、码云） 和 Git之间的关系

- NPM是包管理平台（里面托管了各种各样的包）
- Github、码云 代码托管平台（托管了各种各样的代码仓库）
- Git是用来对代码进行分支版本管理

补充：yarn

- yarn和npm的作用完全一样，都是用来管理项目中的第三方依赖包的！
- yarn是Facebook公司推出来的一套包管理工具！【后期咱们学习React，尤其是ReactNative的时候，默认就是用Yarn去装包的】
- yarn会缓存曾经安装过的包；但是npm也会缓存，但是效果不如yarn明显；
- yarn与npm的命令行小结

补充：如何设置npm和yarn的安装镜像：

什么是NPM淘宝镜像呢：由于每次安装包需要走国外的网络，速度很慢，所以，淘宝帮我们在国内创建了一个NPM包托管网站，能够提升使用NPM装包时候的速度！

1. 配置npm的国内淘宝镜像：

    npm config set registry https://registry.npm.taobao.org --global
    npm config set disturl https://npm.taobao.org/dist --global

2. 配置yarn的国内淘宝镜像：

    yarn config set registry https://registry.npm.taobao.org --global
    yarn config set disturl https://npm.taobao.org/dist --global

总结：Node.js 就是一个Javascript的服务端运行环境（依赖于Chrome 的V8引擎），为Javascript提供了服务器端编程的能力！

Node.js 可以做哪些事情

- 【★】Node可以作为前端的一个工具去使用，通过NPM安装好用的工具；Node可以开发一些前端的工具【i5ting_toc】
- 【★】Node能做服务器
- 【★】Node还可以操作数据库并对外提供数据接口
- Node能做即时聊天

【★★】为什么要学习Node.js

- 从企业角度分析：

- 企业对一专多能人才的需求：怎么才能最大限度的压榨员工；省钱
- 多高性能服务器的需求：怎么才能最大限度的压榨服务器；
- Node适合做快速的网络请求，但是不适合做大数据的业务逻辑的处理；

- 从自身角度分析：

- 挣钱；
- 对将来职业生涯有好处：学了Node之后，为我们构建了后端的知识体系，无论将来你会不会做后端的Node开发，但是，起码你已经构建了完整的前后端知识体系！
- 后面学到的任何新技术：Vue.js，React,React-Native都是基于Node的！包括后面要学的一个构建工具webpack！

在Node中执行相关的JS代码的两种方式

1. 直接在命令行中输入node，进入Node的REPL运行环境：

- R：Read：读取用户输入的字符串内容
- E：Evaluate：把用户输入的字符串，当作JS代码去解析执行
- P：Print：打印输出Evaluate解析的结果
- L：Loop：进入下一次循环

1. 将Node代码写入到一个js文件中，然后通过node 要执行的JS文件路径去运行Node代码

环境变量

为什么可以通过命令行形式，直接启动node或者notepad呢？？？

注意：每当修改了环境变量之后，需要重新启动命令窗口！

什么是环境变量

Path环境变量的作用：能够让我们通过命令行的形式快速启动一个应用程序；

用户变量和系统变量的区别、

用户变量：用户变量是属于每一个用户的，用户之间的用户变量是私有的，不共享的；

系统变量：系统变量是共享的，只能用户能够登录这台电脑，那么就能访问系统变量中的任何东西！【将来咋在配置环境变量的时候，推荐大家配置到系统变量中！】

配置环境变量的两种方式

1. 第一种方式：直接把路径添加到path环境变量中；
2. 第二种方式：先在环境变量中创建一个新变量，名字类似于：ZOOM_HOME这样，值是我们程序的根目录；然后，再把这个变量名，引用到 Path环境变量中，类似于：%ZOOM_HOME%

Path变量的查找规则

1. 先从当前的目录中查找有没有这个应用程序，如果有，则直接运行，如果没有，则去系统环境变量中，path环境变量下挨个查找对应的文件夹，如果在对应文件夹中能找到，则直接运行，如果找不到，最终报错！

【★★】使用fs模块来操作文件

1. fs.readFile
2. fs.writeFile
3. fs.appendFile

【★★★】fs模块中路径问题

箭头函数

Node中的使用http模块创建最基本的web服务器

之前有没有接触过Web服务器？？？

其实，PHPStudy中集成了一个叫做Apache的软件；这个软件就是一个服务器软件，能够托管一个网站；

其实在Node中，并没有类似于Apache这样软件；我们可以通过简单的几行代码，写出一个Web服务器！

【★★★】HTTP协议中的 请求 - 处理 - 响应 模型

【★★】step by step 构建HTTP服务器

升级1：根据不同的URL地址响应不同HTML消息

升级2：根据不同URL地址 - 响应不同的页面

升级3：在响应不同页面的同时响应静态资源（css、图片、js）

【★★★】【难点】升级4：根据不同URL地址 - 响应不同文件的改造

【★★】【难点】网页中资源请求路径问题

相关文章

- JavaScript——历史与简介
- 深入浅出Node.js（一）：什么是Node.js
- I/O事件概述
- 理解Node.js事件驱动编程
- Node.js 中文网
- Node.js 英文官网
- Node.js 菜鸟教程
- CNode：Node.js专业中文社区
- 深入浅出Node.js(朴灵)完整扫描版.pdf
- HTTP Keep-Alive是什么？如何工作？
- 浏览器User-agent String里的历史故事
- art-template API
- yarn与npm的命令行小结