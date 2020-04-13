---
title: js知识点常记
date: 2017-5-13 13:24
tags: js
categories: 前端
summary_img: http://p56w6hcyq.bkt.clouddn.com/js2.jpg
---
## 1.hasOwnProperty相关

为了判断一个对象是否包含自定义属性而不是原型链上的属性，我们需要使用继承自 Object.prototype 的 hasOwnProperty方法。
hasOwnProperty 是 JavaScript 中唯一一个处理属性但是不查找原型链的函数。

<!--more-->

```javascript
// 修改Object.prototype
Object.prototype.bar = 1; 
var foo = {goo: undefined};

foo.bar; // 1
'bar' in foo; // true

foo.hasOwnProperty('bar'); // false
foo.hasOwnProperty('goo'); // true
```



> 注意: 通过判断一个属性是否 undefined 是不够的。 因为一个属性可能确实存在，只不过它的值被设置为 undefined。

### hasOwnProperty 作为属性

JavaScript 不会保护 hasOwnProperty 被非法占用，因此如果一个对象碰巧存在这个属性， 就需要使用外部的 hasOwnProperty 函数来获取正确的结果。

```javascript
var foo = {
    hasOwnProperty: function() {
        return false;
    },
    bar: 'Here be dragons'
};

foo.hasOwnProperty('bar'); // 总是返回 false

// 使用其它对象的 hasOwnProperty，并将其上下文设置为foo
({}).hasOwnProperty.call(foo, 'bar'); // true
```



当检查对象上某个属性是否存在时，hasOwnProperty 是唯一可用的方法。 同时在使用 for in loop遍历对象时，推荐总是使用 hasOwnProperty 方法， 这将会避免原型对象扩展带来的干扰。

### for in 循环

和 in 操作符一样，for in 循环同样在查找对象属性时遍历原型链上的所有属性。

```javascript
// 修改 Object.prototype
Object.prototype.bar = 1;

var foo = {moo: 2};
for(var i in foo) {
    console.log(i); // 输出两个属性：bar 和 moo
}
```



> 注意: 由于 for in 总是要遍历整个原型链，因此如果一个对象的继承层次太深的话会影响性能。

由于不可能改变 for in 自身的行为，因此有必要过滤出那些不希望出现在循环体中的属性， 这可以通过 Object.prototype 原型上的 hasOwnProperty 函数来完成。

### 使用 hasOwnProperty 过滤

```javascript
// foo 变量是上例中的
for(var i in foo) {
    if (foo.hasOwnProperty(i)) {
        console.log(i);
    }
}
```



> 推荐总是使用 hasOwnProperty。不要对代码运行的环境做任何假设，不要假设原生对象是否已经被扩展了。

## 2.命名函数的赋值表达式

另外一个特殊的情况是将命名函数赋值给一个变量。

```javascript
var foo = function bar() {
    bar(); // 正常运行
}
bar(); // 出错：ReferenceError
```



bar 函数声明外是不可见的，这是因为我们已经把函数赋值给了 foo； 然而在 bar 内部依然可见。这是由于 JavaScript 的命名处理所致， 函数名在函数内总是可见的。

> 注意:在IE8及IE8以下版本浏览器bar在外部也是可见的，是因为浏览器对命名函数赋值表达式进行了错误的解析， 解析成两个函数 foo 和 bar

## 3.方法的赋值表达式

另一个看起来奇怪的地方是函数别名，也就是将一个方法赋值给一个变量。

```javascript
var test = someObject.methodTest;
test();
```



上例中，test 就像一个普通的函数被调用；因此，函数内的 this 将不再被指向到 someObject 对象。而是指向了window。

## 4.循环中的闭包

一个常见的错误出现在循环中使用闭包，假设我们需要在每次循环中调用循环序号

```javascript
for(var i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);  
    }, 1000);
}
```



上面的代码不会输出数字 `0`到 `9`，而是会输出数字`10` 十次。

当 console.log 被调用的时候，匿名函数保持对外部变量`i`的引用，此时 `for`循环已经结束，`i`的值被修改成了`10`.

为了得到想要的结果，需要在每次循环中创建变量 `i`的拷贝。

为了避免引用错误，为了正确的获得循环序号，最好使用 匿名包装器（注：其实就是我们通常说的自执行匿名函数）。

```javascript
for(var i = 0; i < 10; i++) {
    (function(e) {
        setTimeout(function() {
            console.log(e);  
        }, 1000);
    })(i);
}
```



外部的匿名函数会立即执行，并把 i 作为它的参数，此时函数内 e 变量就拥有了 i 的一个拷贝。

当传递给 setTimeout 的匿名函数执行时，它就拥有了对 e 的引用，而这个值是不会被循环改变的。

有另一个方法完成同样的工作，那就是从匿名包装器中返回一个函数。这和上面的代码效果一样。

```javascript
for(var i = 0; i < 10; i++) {
    setTimeout((function(e) {
        return function() {
            console.log(e);
        }
    })(i), 1000)
}
```



## 5.对象使用和属性

JavaScript 中所有变量都可以当作对象使用，除了两个例外 `null` 和 `undefined`。

```javascript
false.toString(); // 'false'
[1, 2, 3].toString(); // '1,2,3'

function Foo(){}
Foo.bar = 1;
Foo.bar; // 1
```



一个常见的误解是数字的字面值（literal）不能当作对象使用。这是因为 JavaScript 解析器的一个错误， 它试图将点操作符解析为浮点数字面值的一部分。

```javascript
2.toString(); // 出错：SyntaxError
```



有很多变通方法可以让数字的字面值看起来像对象。

```javascript
2..toString(); // 第二个点号可以正常解析
2 .toString(); // 注意点号前面的空格
(2).toString(); // 2先被计算
```



删除属性的唯一方法是使用 `delete` 操作符；设置属性为 `undefined` 或者 `null` 并不能真正的删除属性， 而**仅仅**是移除了属性和值的关联。

```javascript
var obj = {
    bar: 1,
    foo: 2,
    baz: 3
};
obj.bar = undefined;
obj.foo = null;
delete obj.baz;

for(var i in obj) {
    if (obj.hasOwnProperty(i)) {
        console.log(i, '' + obj[i]);
    }
}
```



上面的输出结果有 `bar undefined` 和 `foo null` - 只有 `baz` 被真正的删除了，所以从输出结果中消失。

## 6.`arguments` 对象

JavaScript 中每个函数内都能访问一个特别变量 `arguments`。这个变量维护着所有传递到这个函数中的参数列表。

`arguments` 变量**不是**一个数组（`Array`）。 尽管在语法上它有数组相关的属性 `length`，但它不从 `Array.prototype`继承，实际上它是一个对象（`Object`）。

因此，无法对 `arguments` 变量使用标准的数组方法，比如 `push`, `pop` 或者 `slice`。 虽然使用 `for` 循环遍历也是可以的，但是为了更好的使用数组方法，最好把它转化为一个真正的数组。

### 转化为数组

下面的代码将会创建一个新的数组，包含所有 `arguments` 对象中的元素。

```
Array.prototype.slice.call(arguments);
```

`arguments` 对象为其内部属性以及函数形式参数创建 *getter* 和 *setter* 方法。

因此，改变形参的值会影响到 `arguments` 对象的值，反之亦然。

```javascript
function foo(a, b, c) {
    arguments[0] = 2;
    a; // 2                                                           

    b = 4;
    arguments[1]; // 4

    var d = c;
    d = 9;
    c; // 3
}
foo(1, 2, 3);
```



如下一个例子：

```javascript
function sidEffecting(ary) { 
  ary[0] = ary[2];
}
function bar(a,b,c) { 
  c = 10
  sidEffecting(arguments);
  return a + b + c;
}
bar(1,1,1)
```

这里所有的更改都将生效，a和c的值都为10，a+b+c的值将为21。

## 7.类型相关

### 测试为定义变量

```javascript
typeof foo !== 'undefined'
```



上面代码会检测 `foo` 是否已经定义；如果没有定义而直接使用会导致 `ReferenceError` 的异常。 这是 `typeof` 唯一有用的地方。当然也能判断出来基本类型。

### `Object.prototype.toString检测一个对象的类型`

为了检测一个对象的类型，强烈推荐使用 `Object.prototype.toString` 方法

如下例子：

```javascript
Object.prototype.toString.call([])    // "[object Array]"
Object.prototype.toString.call({})    // "[object Object]"
Object.prototype.toString.call(2)    // "[object Number]"
```



### 类型转换

内置类型（比如 `Number` 和 `String`）的构造函数在被调用时，使用或者不使用 `new` 的结果完全不同。

```javascript
new Number(10) === 10;     // False, 对象与数字的比较
Number(10) === 10;         // True, 数字与数字的比较
new Number(10) + 0 === 10; // True, 由于隐式的类型转换
```



**转换为字符串**

```javascript
'' + 10 === '10'; // true
```



将一个值加上空字符串可以轻松转换为字符串类型。

**转换为数字**

```javascript
+'10' === 10; // true
```



使用**一元**的加号操作符，可以把字符串转换为数字。

**转换为布尔型**

通过使用 否 操作符两次，可以把一个值转换为布尔型。

```javascript
!!'foo';   // true
!!'';      // false
!!'0';     // true
!!'1';     // true
!!'-1'     // true
!!{};      // true
!!true;    // true
```



## 8.为什么不要使用 `eval`

`eval` 函数会在当前作用域中执行一段 JavaScript 代码字符串。

```javascript
var foo = 1;
function test() {
    var foo = 2;
    eval('foo = 3');
    return foo;
}
test(); // 3
foo; // 1
```



但是 `eval` 只在被**直接**调用并且调用函数就是 `eval` 本身时，才在当前作用域中执行。

```javascript
var foo = 1;
function test() {
    var foo = 2;
    var bar = eval;
    bar('foo = 3');
    return foo;
}
test(); // 2
foo; // 3
```



上面的代码等价于在全局作用域中调用 `eval`，和下面两种写法效果一样：

```javascript
// 写法一：直接调用全局作用域下的 foo 变量
var foo = 1;
function test() {
    var foo = 2;
    window.foo = 3;
    return foo;
}
test(); // 2
foo; // 3

// 写法二：使用 call 函数修改 eval 执行的上下文为全局作用域
var foo = 1;
function test() {
    var foo = 2;
    eval.call(window, 'foo = 3');
    return foo;
}
test(); // 2
foo; // 3
```



在**任何情况下**我们都应该避免使用 `eval` 函数。99.9% 使用 `eval` 的场景都有**不使用** `eval` 的解决方案。

`eval` 也存在安全问题，因为它会执行**任意**传给它的代码， 在代码字符串未知或者是来自一个不信任的源时，绝对不要使用 `eval` 函数。

## 9.定时器

### 手工清空定时器

```javascript
var id = setTimeout(foo, 1000);
clearTimeout(id);
```



### 清除所有定时器

由于没有内置的清除所有定时器的方法，可以采用一种暴力的方式来达到这一目的。

```javascript
// 清空"所有"的定时器
for(var i = 1; i < 1000; i++) {
    clearTimeout(i);
}
```



可能还有些定时器不会在上面代码中被清除（注**：**如果定时器调用时返回的 ID 值大于 1000）， 因此我们可以事先保存所有的定时器 ID，然后一把清除。

建议**不要**在调用定时器函数时，为了向回调函数传递参数而使用字符串的形式。

```javascript
function foo(a, b, c) {}

// 不要这样做
setTimeout('foo(1,2, 3)', 1000)

// 可以使用匿名函数完成相同功能
setTimeout(function() {
    foo(1, 2, 3);
}, 1000)
```



> **绝对不要**使用字符串作为 `setTimeout` 或者 `setInterval` 的第一个参数， 这么写的代码明显质量很差。当需要向回调函数传递参数时，可以创建一个*匿名函数*，在函数内执行真实的回调函数。
>
> 另外，应该避免使用 `setInterval`，因为它的定时执行不会被 JavaScript 阻塞。
>
>  后续逐渐添加

## 10，数组和字符串

- split() join() 的区别
  - 前者是切割成数组的形式，后者是将数组转换成字符串
- 数组方法pop() push() unshift() shift()
  - Push( )尾部添加
  - pop ( )尾部删除
  - Unshift( )头部添加
  - shift( )头部删除 并返回删除项