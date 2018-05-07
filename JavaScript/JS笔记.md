# JavaScript

## 一、 JS实现

完整的JS实现由以下三部分组成：

- ECMAScript
- DOM
- BOM

### 1.1 ECMAScript:定义了JS的核心语言功能

#### ECMAScript的版本(ES5/6)和兼容性

ES的兼容性：不同浏览器(JS运行环境)各个版本的对ES标准的实现情况。

### 1.2 DOM标准：文档对象模型

文档对象模型（DOM，Document Object Model）是针对XML 但经过扩展用于HTML 的应用程序编程接口（API）。DOM把整个页面映射为一个多层节点结构。

#### DOM级别

DOM1:DOM核心（DOM Core）和DOM HTML.DOM 核心规定的是如何映射基于XML 的文档结构，以便简化对文档中任意部分的访问和操作。DOM HTML 模块则在DOM 核心的基础上加以扩展，添加了针对HTML 的对象和方法。

DOM2:DOM2 级在原来DOM 的基础上又扩充了（DHTML 一直都支持的）鼠标和用户界面事件、范围、遍历（迭代DOM文档的方法）等细分模块，而且通过对象接口增加了对CSS（Cascading Style Sheets，层叠样式表）的支持。以下是DOM2想入的新模块

- DOM视图:定义了跟踪不同文档（例如，应用CSS 之前和之后的文档）视图的接口；
- DOM事件
- DOM遍历和范围

DOM3:xxx

注：和ES标准一样，DOM标准也受浏览器实现的影响。

### 1.3 BOM

Internet Explorer 3 和Netscape Navigator 3 有一个共同的特色，那就是支持可以访问和操作浏览器窗口的浏览器对象模型（BOM，Browser Object Model）。开发人员使用BOM 可以控制浏览器显示的页面以外的部分。而BOM 真正与众不同的地方（也是经常会导致问题的地方），还是它作为JavaScript 实现的一部分但却没有相关的标准。这个问题在HTML5 中得到了解决，HTML5 致力于把很多BOM 功能写入正式规范。HTML5 发布后，很多关于BOM 的困惑烟消云散。

## 严格模式

```javascript
use strict;
```

## 二、 基本概念

### 2.1 数据类型

- undefined
- boolean
- string
- number
- object:Object 本质上是由一组无序的名值对组成的

#### typeof:类型检测

#### undefined:未初始化的变量默认值

undefined 值是派生自null, undefined == null 结果为true

#### null:从逻辑角度来看表示一个空对象指针

#### boolean：逻辑值true和false

可以使用Boolean()函数将其他类型转换成boolean类型的值

#### number类型：整数和浮点数

1. 数值范围

    由于内存的限制，ECMAScript 并不能保存世界上所有的数值。ECMAScript 能够表示的最小数值保存在Number.MIN_VALUE 中——在大多   数浏览器中，这个值是5e-324；能够表示的最大数值保存在Number.MAX_VALUE 中——在大多数浏览器中，这个值是    1.7976931348623157e+308。如果某次计算的结果得到了一个超出JavaScript 数值范围的值，那么这个数值将被自动转换成特殊的  Infinity 值。具体来说，如果这个数值是负数，则会被转换成-Infinity（负无穷），如果这个数值是正数，则会被转换成Infinity  （正无穷）。

2. NaN：Not a number
    这个数值用于表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误了）。

    NaN 本身有两个非同寻常的特点:
    - 任何涉及NaN 的操作（例如NaN/10）都会返回NaN
    - NaN 与任何值都不相等，包括NaN 本身

    针对NaN 的这两个特点，ECMAScript 定义了isNaN()函数。这个函数接受一个参数，该参数可以是任何类型，而函数会帮我们确定这个参数是否“不是数值”。isNaN()在接收到一个值之后，会尝试将这个值转换为数值。

3. 数值转换

- Number()
- parseInt()
- parseFloat()

#### String类型