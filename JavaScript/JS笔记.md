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

严格模式为这门语言中容易出错的地方施加了限制。

```javascript
use strict;
```

## 二、 基本概念

### 2.1 基本数据类型

按照ECMA-262 的定义，JavaScript 的变量与其他语言的变量有很大区别。JavaScript 变量松散类型的本质，决定了它只是在特定时间用于保存特定值的一个名字而已。由于不存在定义某个变量必须要保存何种数据类型值的规则，变量的值及其数据类型可以在脚本的生命周期内改变。

- Undefined：未初始化的变量和函数默认返回值。派生至Null
- Null:仅用于表示对象为空。
- Boolean
- String
- Number
- Object:Object 本质上是由一组无序的名值对组成的

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

ECMAScript 中的字符串是不可变的

将其他类型的值转换为String使用toString()方法

#### Object类型：ECMAScript 中的对象其实就是一组数据（属性）和功能（函数）的集合

理解一个重要的思想:即在 ECMAScript 中， (就像 Java 中的 java.lang.Object 对象一样)Object 类型是所有它的实例的基类。

Object的每个实例都具有的属性和方法：

- constructor:保存着用于创建当前对象的函数。
- hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中(而不是在实例 的原型中)是否存在
- isPrototypeOf(object):用于检查传入的对象是否是传入对象的原型
- propertyIsEnumerable(propertyName)
- toLocaleString()
- toString()
- valueOf

### 2.2 操作符

在所有运算中，如果对非数值型数据进行数值转换(有些运算会隐式的先转换，再计算)，调用其Number()方法；进行字符运算调用toString();执行条件语句时如果结果不为Boolean类型会将结果调用Boolean()方法进行转换

#### 位操作符: NaN 和 Infinity 值应用位操作时，这两个值都会被当成 0 来处理

#### 逻辑操作符

1. !

    注意：任何非0的数值的结果都为true,包括undefined,NaN

2. &&

    - 如果第一个操作数是对象，则返回第二个操作数
    - 如果有一个操作数是null,返回null

3. ||

    - 如果第一个操作数是对象，则返回第一个操作数
    - 如果两个操作数都是null，返回null，否则返回非null的那一个操作数。undefined和NaN同理

### 数学运算

### 关系运算

### 相等运算

#### 等于或不等于：强制类型转换

#### 全等或不全等：不类型转换

### 2.3 语句

#### for-in：遍历（枚举）对象属性

如果表示要迭代的对象的变量值为 null 或 undefined，for-in 语句会抛出错误。 ECMAScript 5 更正了这一行为;对这种情况不再抛出错误，而只是不执行循环体。为了保证最大限度的兼容性，建议在使用 for-in 循环之前，先检测确认该对象的值不是 null 或 undefined。

### 2.4 函数

函数对任何语言来说都是一个核心的概念。通过函数可以封装任意多条语句，而且可以在任何地方、任何时候调用执行。

#### 参数：值传递

ECMAScript 中的参数在内部是用一个数组来表示的，函数接收到的始终都是这个数组，而不关心数组中包含哪些参数以及参数的个数。在函数体内可以通过arguments 对象来访问这个参数数组，从而获取传递给函数的每一个参数。

这也就意味着函数的签名仅仅只有函数名，解析器不会验证参数。这个特点也确定了函数不能重载（只能通过判断传入的参数数量来模拟）。

arguments中保存的值与对应命令参数的值保持同步，但它们的内存空间是独立的。

## 三、 变量作用域和内存问题

按照ECMA-262 的定义，JavaScript 的变量与其他语言的变量有很大区别。JavaScript 变量松散类型的本质，决定了它只是在特定时间用于保存特定值的一个名字而已。由于不存在定义某个变量必须要保存何种数据类型值的规则，变量的值及其数据类型可以在脚本的生命周期内改变。

### 3.1 基本类型和引用类型

ECMAScript 变量可能包含两种不同数据类型的值：基本类型值和引用类型值。基本类型值指的是简单的数据段，而引用类型值指那些可能由多个值构成的对象。

5种基本数据类型：Undefined、Null、Boolean、Number 和String。这5 种基本数据类型是按值访问的，因为可以操作保存在变量中的实际的值。

引用类型的值是保存在内存中的对象。与其他语言不同，JavaScript 不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间。在操作对象时，实际上是在操作对象的引用而不是实际的对象。为此，引用类型的值是按引用访问的。

#### 动态添加属性

对于引用类型的值，我们可以动态为其添加属性和方法，也可以改变和删除其属性和方法。

#### 复制变量值

基本类型变量和引用类型变量复制都是将原值复制一份到新分配的内存空间(即原值的副本)。

当从一个变量向另一个变量复制值时，会将存储在变量中的值复制一份放到为新变量分配的空间中。需要注意的是，复制引用类型时，这个值的副本实际上是一个指针，而这个指针指向存储在堆中的**同一个对象**。所以操作任意一个指针副本时，改动的都是同一个对象。

#### 参数传递：按值传递

#### 引用类型检测：instanceof

### 3.2 执行环境及作用域

**执行环境（作用域）**（execution context，为简单起见，有时也称为“环境”）是JavaScript 中最为重要的一个概念。执行环境定义了变量的生命周期，以及哪一部分代码可以访问其中的变量。

**环境变量对象**:每个执行环境都有一个与之关联的变量对象（variable object），**环境中定义的所有变量和函数都保存在这个对象中**。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。

**全局执行环境**是最外围的一个执行环境。根据ECMAScript 实现所在的宿主环境不同，表示执行环境的对象也不一样。在Web 浏览器中，全局执行环境被认为是window 对象，因此所有全局变量和函数都是作为window 对象的属性和方法创建的。某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁（全局执行环境直到应用程序退出——例如关闭网页或浏览器——时才会被销毁）。

**函数执行环境**：**每个函数都有自己的执行环境**。当执行流进入一个函数时，函数的环境就会被推入一个环境栈中。而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。ECMAScript 程序中的执行流正是由这个方便的机制控制着。

**作用域链**：当代码在一个环境中执行时，会创建变量对象的一个作用域链（scope chain）。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端，始终都是当前执行的代码所在环境的变量对象。如果这个环境是函数，则将其活动对象（activation object）作为变量对象。活动对象在最开始时只包含一个变量，即**arguments 对象**（这个对象在全局环境中是不存在的）。作用域链中的下一个变量对象来自**包含（外部）环境**，而再下一个变量对象则来自下一个包含环境。这样，一直延续到全局执行环境；全局执行环境的变量对象始终都是作用域链中的最后一个对象。

**标识符解析**是沿着作用域链一级一级地搜索标识符的过程。搜索过程始终从作用域链的前端开始，然后逐级地向后回溯，直至找到标识符为止（如果找不到标识符，通常会导致错误发生）。也就是从局部到外部到全局的搜索过程。

```javascript
var color = "blue";

function changeColor(){
    var anotherColor = "red";
    function swapColors(){
        var tempColor = anotherColor;
        anotherColor = color;
        color = tempColor;
        // 这里可以访问color、anotherColor 和tempColor
    }
    // 这里可以访问color 和anotherColor，但不能访问tempColor
    swapColors();
}
// 这里只能访问color
changeColor();
```

以上代码共涉及3 个执行环境：全局环境、changeColor()的局部环境和swapColors()的局部环境。全局环境中有一个变量color 和一个函数changeColor()。changeColor()的局部环境中有一个名为anotherColor 的变量和一个名为swapColors()的函数，但它也可以访问全局环境中的变量color。swapColors()的局部环境中有一个变量tempColor，该变量只能在这个环境中访问到。无论全局环境还是changeColor()的局部环境都无权访问tempColor。然而，在swapColors()内部则可以访问其他两个环境中的所有变量，因为那两个环境是它的父执行环境。

#### 延长作用域块

- try-catch 语句的catch块：对catch语句来说，会创建一个新的变量对象，其中包含的是被抛出的错误对象的声明。
- with

#### JS没有块级作用域

1. 声明变量

    使用var 声明的变量会自动被添加到**最接近的环境中**。在函数内部，最接近的环境就是函数的局部环境；在with 语句中，最接近的环境是函数环境。如果初始化变量时没有使用var 声明，该变量会自动被添加到全局环境。

2. 搜索标识符

    当在某个环境中为了读取或写入而引用一个标识符时，必须通过搜索来确定该标识符实际代表什么。搜索过程从作用域链的前端开始，向上逐级查询与给定名字匹配的标识符。如果在局部环境中找到了该标识符，搜索过程停止，变量就绪。如果在局部环境中没有找到该变量名则继续沿作用域链向上搜索。搜索过程将一直追溯到全局环境的变量对象。如果在全局环境中也没有找到这个标识符，则意味着该变量尚未声明。

### 3.3 垃圾回收

JavaScript 具有自动垃圾收集机制，也就是说，执行环境会负责管理代码执行过程中使用的内存。这种垃圾收集机制的原理其实很单：找出那些不再继续使用的变量，然后释放其占用的内存。为此，垃圾收集器会按照固定的时间间隔（或代码执行中预定的收集时间），周期性地执行这一操作。

垃圾回收策略：标记清除和引用计数

#### 标记清除：mark-and-sweep

#### 引用计数：reference counting

Netscape Navigator 3.0 是最早使用引用计数策略的浏览器，但很快它就遇到了一个严重的问题：循环引用。

**循环引用**指的是对象A 中包含一个指向对象B 的指针，而对象B 中也包含一个指向对象A 的引用。这样这两个对象的引用计数始终是2，永远不会回收。

#### 性能问题

垃圾收集器是周期性运行的，而且如果为变量分配的内存数量很可观，那么回收工作量也是相当大的。在这种情况下，确定**垃圾收集的时间间隔**是一个非常重要的问题。

#### 管理内存

使用具备垃圾收集机制的语言编写程序，开发人员一般不必操心内存管理的问题。但是，JavaScript在进行内存管理及垃圾收集时面临的问题还是有点与众不同。其中最主要的一个问题，就是分配给Web浏览器的可用内存数量通常要比分配给桌面应用程序的少。这样做的目的主要是出于安全方面的考虑，目的是防止运行JavaScript 的网页耗尽全部系统内存而导致系统崩溃。内存限制问题不仅会影响给变量分配内存，同时还会影响调用栈以及在一个线程中能够同时执行的语句数量。

因此，确保占用最少的内存可以让页面获得更好的性能。而优化内存占用的最佳方式，就是为执行中的代码只保存必要的数据。一旦数据不再有用，最好通过将其值设置为null 来标记其引用可以释放——这个做法叫做**解除引用（dereferencing）**。这一做法适用于大多数全局变量和全局对象的属性。局部变量会在它们离开执行环境时自动被解除引用。

## 四、 引用类型

引用类型的值（对象）是某个特定引用类型的一个实例。在ECMAScript 中，引用类型是一种**数据结构**，用于将数据和功能组织在一起。它也常被称为类，但这种称呼并不妥当。尽管ECMAScript从技术上讲是一门面向对象的语言，但它不具备传统的面向对象语言所支持的类和接口等基本结构。引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

新对象是使用new 操作符后跟一个构造函数来创建的。**构造函数**本身就是一个函数，只不过该函数是出于创建新对象的目的而定义的

### 4.1 Object类型

```javascript
// 使用构造函数
var person = new Object();
person.name = "zyy";
persion.age = "18";

/**
*
* 对象字面量:简化创建包含大量属性的对象的过程.
* 就是花括号里边包含 key:value对(属性名:属性值)，多个属性用逗号分隔
*
* **使用字面量创建Object实现不会调用构造方法**
*/

var person = {
    name: "zyy",
    age: 18
}
```

tip:一般来讲，命名参数虽然容易处理，但在有多个可选参数的情况下就会显示不够灵活。最好的做法是对那些必需值使用命名参数，而使用对象字面量来封装多个可选参数。

#### 访问对象中的属性

```javascript
// 1. 使用点号
person.name

// 2. 使用[]，当需要**使用变量来访问对象属性**时使用这种方法，否则用点号
person["name"]
```

### 4.2 Array类型

除了Object 之外，Array 类型恐怕是ECMAScript 中最常用的类型了。而且，ECMAScript 中的数组与其他多数语言中的数组有着相当大的区别。虽然ECMAScript 数组与其他语言中的数组都是数据的有序列表，但与其他语言不同的是，ECMAScript 数组的**每一项可以保存任何类型的数据**。也就是说，可以用数组的第一个位置来保存字符串，用第二位置来保存数值，用第三个位置来保存对象，以此类推。而且，ECMAScript 数组的大小是**可以动态调整**的，即可以随着数据的添加自动增长以容纳新增数据。

#### 创建Array实例

```javascript
// 1. 构造函数
var arr = new Array(params);
//创建数据可以省略new
var arr = Array(params);

// 2. 字面量：和Object一样，使用字面量创建Array实例不会调用其构造方法
var arr = [1,2];
var arr = [];
```

#### 访问数组元素（索引）和动态性

数组索引：0 ~ length-1。

由于数组的动态性，可以在运行时手动**改变数组的length属性**和通过给**超出数组索引范围的项赋值**来改变数组长度。

#### 判断对象是否为数组:Array.isArray()

自从ECMAScript 3 做出规定以后，就出现了确定某个对象是不是数组的经典问题。对于一个网页，或者一个全局作用域而言，使用instanceof 操作符就能得到满意的结果。

instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的Array 构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。

为了解决这个问题，ECMAScript 5 新增了Array.isArray()方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的

#### 转换其他类型

- toString()
- toLocalString()
- toValueOf()
- join()

join():数组继承的toLocaleString()、toString()和valueOf()方法，在默认情况下都会以**逗号分隔的字符串**的形式返回数组项。而如果使用join()方法，则可以使用不同的分隔符来构建这个字符串。

如果数组中的某一项的值是null 或者undefined，那么该值在join()、toLocaleString()、toString()和valueOf()方法返回的结果中以空字符串表示。

#### 栈方法：将数组视为一个栈使用

- push()
- pop()

#### 队列方法

- shift()
- unshift()

#### 数组排序

- reverse()
- sort()，此方法还可以转递一个用于排序的函数

这两个方法的返回值都是排序之后的数组。

#### 操作方法

- concat()
- slice()
- splice()：向数组中插入项。利用该方法可以实现删除、插入、替换数组中的项。

#### 查找项的位置

- indexOf()
- lastIndexOf()

这两个方法在查找的时候都是进行全等判断，如找到返回所在位置，未找到返回-1。

#### 数组迭代

ECMAScript 5 为数组定义了5 个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象——影响this 的值。这个函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响方法的返回值。

- every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true。
- filter()：对数组中的每一项运行给定函数，返回该函数会返回true 的项组成的数组。
- forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。
- map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
- some()：对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true。

#### 并归（合并）操作

ECMAScript 5 还新增了两个归并数组的方法：reduce()和reduceRight()。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。其中，reduce()方法从数组的第一项开始，逐个遍历到最后。而reduceRight()则从数组的最后一项开始，向前遍历到第一项。

- reduce()
- reduceRight()

这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为归并基础的初始值。

并归调用的函数接收4 个参数：前一个值（第一次调用时该值为数组第一项)，此后这个值为前一次并归操作函数的返回值）、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代**发生在数组的第二项**上，**因此第一个参数是数组的第一项**，第二个参数就是数组的第二项。

### 4.3 Date类型

```javascript
// 创建对象，用无参构造创建的Date对象获取的时间是当前时间。
var date = new Date();

// 带日期字符串参数,内部也是调用Date.parese()来解析该字符串
var someDate = new Date("May 25, 2004");
```

- Date.parse()
- Date.UTC()
- Data.now()  //es5

#### 从Object继承的方法

#### 日期格式化方法

- toDateString()——以特定于实现的格式显示星期几、月、日和年；
- toTimeString()——以特定于实现的格式显示时、分、秒和时区；
- toLocaleDateString()——以特定于地区的格式显示星期几、月、日和年；
- toLocaleTimeString()——以特定于实现的格式显示时、分、秒；
- toUTCString()——以特定于实现的格式完整的UTC 日期。

与toLocaleString()和toString()方法一样，以上这些字符串格式方法的输出也是因浏览器
而异的，因此没有哪一个方法能够用来在用户界面中显示一致的日期信息。

#### 日期/时间组件方法:获取日期中特定部分的值

### 4.4 RegExp类型

```javascript
//字面量
var expression = / pattern / flags ;

//构造函数，与字面的区别是，由于构造函数的参数是字符串，匹配的字符包括元字符时要进行双重转义
var exp = new RegExp(patternStr,flagStr);

// 例如,以下两个实例等价
var exp1 = /\[bc\]at/i
var exp2 = new RegExp("\\[bc\\]at", "i");
```

其中的模式（pattern）部分可以是任何简单或复杂的正则表达式，可以包含字符类、限定符、分组、
向前查找以及反向引用。每个正则表达式都可带有一或多个标志（flags），用以标明正则表达式的行为。
正则表达式的匹配模式支持下列3 个标志。

- g：表示全局（global）模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止；
- i：表示不区分大小写（case-insensitive）模式，即在确定匹配项时忽略模式与字符串的大小写；
- m：表示多行（multiline）模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。

#### 实例属性

通过这些属性可以获知一个正则表达式的各方面信息，但却没有多大用处，因为这些信息全都包含在模式声明中。

- global：布尔值，表示是否设置了g 标志。
- ignoreCase：布尔值，表示是否设置了i 标志。
- lastIndex：整数，表示开始搜索下一个匹配项的字符位置，从0 算起。
- multiline：布尔值，表示是否设置了m 标志。
- source：正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。

#### 实例方法

1. exec():专门为捕获组而设计的方法
    对于exec()方法而言，即使在模式中设置了全局标志（g），它每次也只会返回一个匹配项。在不
设置全局标志的情况下，在同一个字符串上多次调用exec()将始终返回第一个匹配项的信息。而在设
置全局标志的情况下，每次调用exec()则都会在字符串中继续查找新匹配项

2. test()

RegExp 实例继承的toLocaleString()和toString()方法都会返回正则表达式的字面量。

#### RegExp构造函数属性:其他语言被看成静态属性(也就是通过类弄名称直接调用，不用实例化)

长属性名 | 别名 | 功能
------- | ------- | -------
RegExp.input | RegExp["$_"] | 最近一次要匹配的字符串。Opera未实现此属性
RegExp.lastMatch | RegExp["$&"] | 最近一次的匹配项。Opera未实现此属性
RegExp.lastParen | RegExp["$+"] | 最近一次匹配的捕获组。Opera未实现此属性
RegExp.leftContext | RegExp["$`"] | input字符串中lastMatch之前的文本
RegExp.multiline | RegExp["$*"] | 布尔值，表示是否所有表达式都使用多行模式。IE和Opera未实现此属性
RegExp.rightContext | RegExp["$'"] | Input字符串中lastMatch之后的文本

上面的几个属性之外，还有9 个用于存储捕获组的构造函数属性。$1 至 $9

### 4.5 Function类型

说起来ECMAScript 中什么最有意思，莫过于函数了——而有意思的根源，则在于**函数实际上是对象**。每个函数都是Function 类型的实例，而且都与其他引用类型一样具有属性和方法。由于函数是对象，因此**函数名实际上也是一个指向函数对象的指针**，不会与某个函数绑定。

```javascript
//函数的定义方式
// 1. 函数声明
function sum (num1, num2) {
    return num1 + num2;
}

// 2. 表达式
var sum = function(sum1, sum2) {
    return num1 + num2;
}

/*
  3. 构造函数
  从技术角度讲，这是一个函数表达式。但是，我们不推荐读者使用这种方法定义函数，因为这种语法会导致解析两次代码（第一次是解析常规ECMAScript 代码，第二次是解析传入构造函数中的字符串），从而影响性能。不过，这种语法对于理解“函数是对象，函数名是指针”的概念倒是非常直观的。
*/
var sum = new Function("num1", "num2", "return num1 + num2");

```

#### 没有重载(深入理解)

将函数名想象为指针，也有助于理解为什么ECMAScript 中没有函数重载的概念。

```javascript
function addSomeNumber(num){
    return num + 100;
}
function addSomeNumber(num) {
    return num + 200;
}
var result = addSomeNumber(100);


//显然，这个例子中声明了两个同名函数，而结果则是后面的函数覆盖了前面的函数。以上代码实际上与下面的代码没有什么区别。
var addSomeNumber = function (num){
    return num + 100;
};
addSomeNumber = function (num) {
    return num + 200;
};
var result = addSomeNumber(100);

//通过观察重写之后的代码，很容易看清楚到底是怎么回事儿——在创建第二个函数时，实际上覆盖了引用第一个函数的变量addSomeNumber。
```

#### 函数声明与函数表达式的区别：函数声明提升

解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。

因为在代码开始执行之前，解析器就已经通过一个名为函数声明提升（function declaration hoisting）的过程，读取并将函数声明添加到执行环境中。对代码求值时，JavaScript引擎在第一遍会声明函数并将它们放到源代码树的顶部。所以，即使声明函数的代码在调用它的代码后面，JavaScript 引擎也能把函数声明提升到顶部。

```javascript
//函数声明定义，函数提升，可以执行。
alert(sum(10,10));
function sum(num1, num2){
    return num1 + num2;
}

// 表达式定义，按顺序执行，所以会报错
alert(sum(10,10));
var sum = function(num1, num2){
    return num1 + num2;
};
```

#### 函数内部属性

在函数内部，有两个特殊的对象：arguments 和this；

1. arguments.callee:指向拥有这个arguments 对象的函数的指针
2. this:指向当前函数的执行环境的环境变量对象的指针。
3. caller:指向调用当前函数的函数的引用。
4. 严格模式

    当函数在严格模式下运行时，访问arguments.callee 会导致错误。ECMAScript 5 还定义了arguments.caller 属性，但在严格模式下访问它也会导致错误，而在非严格模式下这个属性始终是undefined。定义这个属性是为了分清arguments.caller 和函数的caller 属性。以上变化都是为了加强这门语言的安全性，这样第三方代码就不能在相同的环境里窥视其他代码了。严格模式还有一个限制：不能为函数的caller 属性赋值，否则会导致错误。

```javascript
window.color = "red";
var o = {
    color: "blue"
};

function sayColor() {
    alert(this.color);
}
sayColor(); //"red"
o.sayColor = sayColor;  //将函数赋值给对象的属性，并通过对象调用，此时this引用的是该对象
o.sayColor(); //"blue"
```

#### 函数的属性和方法（作为对象而言）

1. length:表示函数希望接收的命名参数的个数(也就是函数声明时形参的个数)。
2. prototype：ECMAScript 中的引用类型而言，prototype 是保存它们所有实例方法的真正所在

    诸如toString()和valueOf()等方法实际上都保存在prototype 名下，只不过是通过各自对象的实例访问罢了。在创建自定义引用类型以及实现继承时，prototype 属性的作用是极为重要的）。在ECMAScript 5 中，prototype 属性是不可枚举的，因此使用for-in 无法发现。

3. apply()和call():。这两个方法的用途都是在特定的作用域中调用函数（实际上等于设置函数体内this 对象的值）

    apply()和call()的区别仅仅是传递的函数调用参数的方式不同。allply使用的是参数数组，而call是单独传递每一个参数。

    传递参数并非apply()和call()真正的用武之地；它们真正强大的地方是能够扩充函数赖以运行的作用域。

    ```javascript
    window.color = "red";
    var o = { color: "blue" };
    function sayColor(){
            alert(this.color);
    }
    sayColor(); //red
    sayColor.call(this); //red
    sayColor.call(window); //red
    sayColor.call(o); //blue
    ```

4. bind():ES5,创建函数的实例，其this（执行环境变量对象）的值会被绑定到传给bind()函数的值

    ```javascript
    window.color = "red";
    var o = { color: "blue" };
    function sayColor(){
        alert(this.color);
    }
    var objectSayColor = sayColor.bind(o);
    objectSayColor(); //blue
    ```

### 4.6 基本类型的包装类

1. 包装类型的由来

    为了便于操作基本类型值，ECMAScript 还提供了3 个特殊的引用类型：Boolean、Number 和String。这些类型与本章介绍的其他引用   类型相似，但同时也具有与各自的基本类型相应的特殊行为。实际上，**每当读取一个基本类型值的时候，后台就会创建一个对应的基本   包装类型的对象**，从而让我们能够调用一些方法来操作这些数据。

    ```javascript
    var s1 = "some text";
    var s2 = s1.substring(2);

    /*
    这个例子中的变量s1 包含一个字符串，字符串当然是基本类型值。而下一行调用了s1 的
    substring()方法，并将返回的结果保存在了s2 中。我们知道，基本类型值不是对象，因而从逻辑上
    讲它们不应该有方法（尽管如我们所愿，它们确实有方法）。其实，为了让我们实现这种直观的操作，
    后台已经自动完成了一系列的处理。当第二行代码访问s1 时，访问过程处于一种读取模式，也就是要
    从内存中读取这个字符串的值。而在读取模式中访问字符串时，后台都会自动完成下列处理。
    (1) 创建String 类型的一个实例；
    (2) 在实例上调用指定的方法；
    (3) 销毁这个实例。
    */

    var s1 = new String("some text");
    var s2 = s1.substring(2);
    s1 = null;
    ```

2. 包装类型和基本类型的区别

    引用类型与基本包装类型的主要区别就是对象的生存期。使用new 操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。这意味着我们不能在运行时为基本类 型值添加属性和方法。

    ```javascript
    var s1 = "some text";
    // 因为基本类型没有属性和方法，这里创建属性实际上是自动创建了它的包装类型来添加对象
    s1.color = "red";
    //但是由于自动创建的包装类型的对象，执行了添加属性操作之后，就销毁了。
    alert(s1.color); //undefined
    ```

    Object 构造函数也会像工厂方法一样，根据传入值的类型返回相应基本包装类型的实例。

    ```javascript
    var value = "25";
    var number = Number(value); //转型函数
    alert(typeof number); //"number"

    var obj = new Number(value); //构造函数
    alert(typeof obj); //"object"
    ```

#### String包装类型

1. 取出特定位置的字符

    - charAt()
    - charCodeAt()

2. 字符串操作：联结、取子串

    - concat()
    - slice()
    - substr()
    - subString()

3. 查找字符串中子串的位置

    - indexOf()
    - lastIndexOf()

4. trim()
5. 大小写转换
6. 字符串的正则匹配方法

    - match()
    - search()
    - replace()
    - split()

7. 其他方法

    - localCompare()
    - fromCharCode()

    String 构造函数本身还有一个静态方法：fromCharCode()。这个方法的任务是接收一或多个字符编码，然后将它们转换成一个字符串。 从本质上来看，这个方法与实例方法charCodeAt()执行的是相反的操作。

### 单体内置对象:Global/Math

ECMA-262 对内置对象的定义是：“由ECMAScript 实现提供的、不依赖于宿主环境的对象，这些对象在ECMAScript 程序执行之前就已经存在了。”意思就是说，开发人员**不必显式地实例化内置对象**，因为它们已经实例了。前面我们已经介绍了大多数内置对象，例如Object、Array 和String。ECMA-262 还定义了两个单体内置对象：Global 和Math。

#### Global对象

Global（全局）对象可以说是ECMAScript 中最特别的一个对象了，因为不管你从什么角度上看，这个对象都是不存在的。ECMAScript 中的Global 对象在某种意义上是作为一个终极的“兜底儿对象”来定义的。换句话说，不属于任何其他对象的属性和方法，最终都是它的属性和方法。**事实上，没有全局变量或全局函数；所有在全局作用域中定义的属性和函数，都是Global 对象的属性**。本书前面介绍过的那些函数，诸如isNaN()、isFinite()、parseInt()以及parseFloat()，实际上全都是Global对象的方法。

1. URI编码方法
2. eval()

3. Global对象的属性

    Global 对象还包含一些属性，例如特殊的值undefined、NaN 以及Infinity 都是Global 对象的属性。此外，所有原生引用类型的构造函数，像Object 和Function，也都是Global 对象的属性。

    ECMAScript 5 明确禁止给undefined、NaN 和Infinity 赋值，这样做即使在非严格模式下也会导致错误。

4. Window对象

ECMAScript 虽然没有指出如何直接访问Global 对象，**但Web 浏览器都是将这个全局对象作为window 对象的一部分加以实现的**。因此，在全局作用域中声明的所有变量和函数，就都成为了window对象的属性。

另一种取得Global 对象的方法是使用以下代码：

```javascript

/**
以下代码创建了一个立即调用的函数表达式，返回this 的值。如前所述，在没有给函数明确指定this 值的情况下（无论是通过将函数添加为对象的方法，还是通过调用call()或apply()），this值等于Global 对象。而像这样通过简单地返回this 来取得Global 对象，在任何执行环境下都是可行的。
*/
var global = function(){
return this;
}();
```

#### Math对象

## 六、 OOP

面向对象（Object-Oriented，OO）的语言有一个标志，那就是它们都有类的概念，而通过类可以创建任意多个具有相同属性和方法的对象。**ECMAScript 中没有类的概念**，因此它的对象也与基于类的语言中的对象有所不同。ECMA-262 把对象定义为：“**无序属性的集合，其属性可以包含基本值、对象或者函数**。”严格来讲，这就相当于说对象是一组没有特定顺序的值。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值。正因为这样（以及其他将要讨论的原因），我们可以把ECMAScript 的对象想象成散列表：无非就是一组名值对，其中值可以是数据或函数。每个对象都是基于一个引用类型创建的，这个引用类型可以是原生类型，也可以是开发人员定义的类型。

### 6.1 理解对象

#### 属性类型

ECMA-262 第5 版在定义只有内部才用的特性（attribute）时，描述了属性（property）的各种特征。ECMA-262 定义这些特性是为了实现JavaScript 引擎用的，因此在JavaScript 中不能直接访问它们。为了表示特性是内部值，该规范把它们放在了两对儿方括号中，例如[[Enumerable]]。

内部属性的类型分为：数据属性和访问器属性。

1. 数据属性

    数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有4 个描述其行为的特性。
    - [[Configurable]]
    - [[Enumerable]]
    - [[Writeable]]
    - [[Value]]

    要修改属性默认的特性，必须使用ECMAScript 5 的Object.defineProperty()方法。

2. 访问器属性

    访问器属性不包含数据值；它们包含一对儿getter 和setter 函数（不过，这两个函数都不是必需的）。在读取访问器属性时，会调用getter 函数，这个函数负责返回有效的值；在写入访问器属性时，会调用setter 函数并传入新值，这个函数负责决定如何处理数据。访问器属性有如下4 个特性。
    - [[Configurable]]
    - [[Enumerable]]
    - [[Get]]
    - [[Set]]

    访问器属性不能直接定义，必须使用Object.defineProperty()来定义。

    tip:
    - 在这个方法之前， 要创建访问器属性， 一般都使用两个非标准的方法：__defineGetter__()和__defineSetter__()。
    - 在不支持Object.defineProperty() 方法的浏览器中不能修改[[Configurable]] 和[[Enumerable]]。

#### 定义多个属性

    由于为对象定义多个属性的可能性很大，ECMAScript 5 又定义了一个Object.defineProperties()方法。利用这个方法可以通过描述符一次定义多个属性。

    ```javascript
    var book = {};
    Object.defineProperties(book, {
    _year: {
        value: 2004
    },
    edition: {
        value: 1
    },
    year: {
        get: function(){return this._year;
        },
        set: function(newValue){
            if (newValue > 2004) {
              this._year = newValue;
              this.edition += newValue - 2004;
         }
        }
    }
    });
    ```

#### 读取属性的特征

使用ECMAScript 5 的Object.getOwnPropertyDescriptor()方法，可以取得给定属性的描述符。这个方法接收两个参数：属性所在的对象和要读取其描述符的属性名称。返回值是一个对象，如果是访问器属性，这个对象的属性有configurable、enumerable、get 和set；如果是数据属性，这个对象的属性有configurable、enumerable、writable 和value。

### 6.2 创建对象

虽然Object 构造函数或对象字面量都可以用来创建单个对象，但这些方式有个明显的缺点：使用同一个接口创建很多对象，会产生大量的重复代码。为解决这个问题，人们开始使用工厂模式的一种变体。

#### 工厂模式

工厂模式是软件工程领域一种广为人知的设计模式，这种模式抽象了创建具体对象的过程，考虑到在ECMAScript 中无法创建类，开发人员就发明了一种函数，用函数来封装以特定接口创建对象的细节

```javascript
function createPerson(name, age, job) {
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function () {
        alert(this.name);
    };
    return o;
}
var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
```

工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）。

#### 构造函数模式

```javascript
function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function () {
        alert(this.name);
    };
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

在上面的例子中，Person()函数取代了createPerson()函数。我们注意到，Person()中的代码除了与createPerson()中相同的部分外，还存在以下不同之处：

- 没有显式地创建对象
- 直接将属性和方法赋给了this对象
- 没有return语句

此外，还应该注意到函数名Person 使用的是大写字母P。按照惯例，构造函数始终都应该以一个大写字母开头，而非构造函数则应该以一个小写字母开头。这个做法借鉴自其他OO 语言，主要是为了区别于ECMAScript 中的其他函数；因为构造函数本身也是函数，只不过可以用来创建对象而已。

要创建Person对象的新实例，必须使用new 操作符。以这种方式调用构造函数实际上会经历以下4个步骤：

- 创建一个新对象；
- 将构造函数的作用域赋值为新对象（因此this 就指向了这个新对象）；
- 执行构造函数中的代码（为这个新对象添加属性）；
- 返回新对象。

在前面例子的最后，person1 和person2 分别保存着Person 的一个不同的实例。这两个对象都有一个constructor（构造函数）属性，该属性指向Person

```javascript
alert(person1.constructor == Person); //true
alert(person2.constructor == Person); //true

/** 对象的constructor 属性最初是用来标识对象类型的。但是，提到检测对象类型，还是instanceof操作符要更可靠一些。我们在这个例子中创建的所有对象既是Object 的实例，同时也是Person的实例，这一点通过instanceof 操作符可以得到验证。
*/
alert(person1 instanceof Object); //true
alert(person1 instanceof Person); //true
alert(person2 instanceof Object); //true
alert(person2 instanceof Person); //true
```

创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型；而这正是构造函数模式胜过工厂模式的地方。

1. 将构造函数当函数使用

    构造函数与其他函数的唯一区别，就在于调用它们的方式不同。不过，构造函数毕竟也是函数，不存在定义构造函数的特殊语法。任何函数，只要通过new 操作符来调用，那它就可以作为构造函数；而任何函数，如果不通过new 操作符来调用，那它跟普通函数也不会有什么两样。

    ```javascript
    // 当作构造函数使用
    var person = new Person("Nicholas", 29, "Software Engineer");
    person.sayName(); //"Nicholas"
    // 作为普通函数调用，此时是在全局作用域中调用，此时this指向的就是window
    Person("Greg", 27, "Doctor"); // 添加到window
    window.sayName(); //"Greg"
    // 在另一个对象的作用域中调用
    var o = new Object();
    Person.call(o, "Kristen", 25, "Nurse");
    o.sayName(); //"Kristen"
    ```

2. 构造函数的问题

构造函数模式虽然好用，但也并非没有缺点。使用构造函数的主要问题，就是每个方法都要在每个实例上重新创建一遍。在前面的例子中，person1 和person2 都有一个名为sayName()的方法，但那两个方法不是同一个Function 的实例。不要忘了——ECMAScript 中的函数是对象，因此每定义一个函数，也就是实例化了一个对象。从逻辑角度讲，此时的构造函数也可以这样定义。

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = new Function("alert(this.name)"); // 与声明函数在逻辑上是等价的
}
```

从这个角度上来看构造函数，更容易明白每个Person 实例都包含一个不同的Function 实例（以显示name 属性）的本质。说明白些，以这种方式创建函数，**会导致不同的作用域链和标识符解析**，但创建Function 新实例的机制仍然是相同的。因此，不同实例上的同名函数是不相等的，以下代码可以证明这一点。

```javascript
alert(person1.sayName == person2.sayName); //false
```

然而，创建两个完成同样任务的Function 实例的确没有必要；况且有this 对象在，根本不用在执行代码前就把函数绑定到特定对象上面。因此，大可像下面这样，通过把函数定义转移到构造函数外部来解决这个问题。

```javascript
function Person(name, age, job){
this.name = name;
this.age = age;
this.job = job;
this.sayName = sayName;
}
function sayName(){
alert(this.name);
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

这样做确实解决了两个函数做同一件事的问题，可是新问题又来了：在全局作用域中定义的函数实际上只能被某个对象调用，这让全局作用域有点名不副实。而更让人无法接受的是：如果对象需要定义很多方法，那么就要定义很多个全局函数，于是我们这个自定义的引用类型就丝毫没有封装性可言了。好在，这些问题可以通过使用原型模式来解决。

#### 原型模式（重要）

我们创建的每个**函数**都有一个prototype（原型）属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的**所有实例共享的属性和方法**.如果按照字面意思来理解，那么prototype 就是通过调用构造函数而创建的那个对象实例的原型对象。使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法.

要理解原型模式的工作原理，必须先理解ECMAScript 中原型对象的性质。

1. 理解原型对象

    无论什么时候，只要创建了一个新函数，就会根据一组特定的规则为该函数创建一个prototype属性，这个属性指向**函数的原型对象**。在默认情况下，所有原型对象都会自动获得一个constructor（构造函数）属性，这个属性包含一个指向prototype 属性所在函数的指针。

    创建了自定义的构造函数之后，其原型对象默认只会取得constructor 属性；至于其他方法，则都是从Object 继承而来的。**当调用构造 函数创建一个新实例后，该实例的内部将包含一个指针（内部属性），指向构造函数的原型对象（该指针指向创建该实例时的构造函数的原型对象）**。ECMA-262 第5 版中管这个指针叫[ [Prototype]]。虽然在脚本中没有标准的方式访问[[Prototype]]，但Firefox、Safari 和Chrome 在每个对象上都支持一个属性 **__proto__**；而在其他实现中，这个属性对脚本则是完全不可见的。不过，要明确的真正重要的一点就是，**这个连接存在于实例与  构造函数的原型对象之间，而不是存在于实例与构造函数之间**。

    虽然在所有实现中都无法访问到[[Prototype]]，但可以通过isPrototypeOf()方法来确定对象之间是否存在这种关系。从本质上讲，如  果[[Prototype]]指向调用isPrototypeOf()方法的对象，那么这个方法就返回true

    ECMAScript 5 增加了一个新方法，叫Object.getPrototypeOf()，在所有支持的实现中，这个方法返回[[Prototype]]的值。然后通过该引用访问对象的构造方法的原型对象的属性和方法。

    **每当代码读取某个对象的某个属性时，都会执行一次搜索**，目标是具有给定名字的属性。搜索首先从对象实例本身开始。如果在实例中找到了具有给定名字的属性，则返回该属性的值；如果没有找到，则继续搜索指针指向的原型对象，在原型对象中查找具有给定名字的属性。如果在原型对象中找到了这个属性，则返回该属性的值。这就意味着当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性；换句话说，添加这个属性只会阻止我们访问原型中的那个属性(屏蔽掉)，但不会修改那个属性

    使用hasOwnProperty()方法可以检测一个属性是存在于实例中，还是存在于原型中。这个方法（不要忘了它是从Object 继承来的）只在给定属性存在于对象实例中时，才会返回true

2. 原型与in操作符

    有两种方式使用in 操作符：单独使用和在for-in。在单独使用时，in 操作符会在通过对象能够访问给定属性时返回true，无论该属性存在于实例中还是原型中。

    在使用for-in迭代时，返回的是所有能够通过对象访问的、可枚举的（enumerated）属性，其中既包括存在于实例中的属性，也包括存在于原型中的属性。

    要取得对象上所有可枚举的实例属性，可以使用ECMAScript 5 的Object.keys()方法。这个方法接收一个对象作为参数，返回一个包含所有可枚举属性的字符串数组。

    Object.getOwnPropertyNames()：获取该对象实例的所有属性，无论它是否可枚举。

3. 更简单的原型语法

    实例的原型对象每添加一个属性和方法就要敲一遍XXX.prototype。为减少不必要的输入，也为了从视觉上更好地封装原型的功能，更常见的做法是用一个包含所有属性和方法的对象字面量来重写整个原型对象。

    ```javascript
    function Person() {}
    Person.prototype = {
        name: "Nicholas",
        age: 29,
        job: "Software Engineer",
        sayName: function () {
            alert(this.name);
        }
    };
    ```

    我们将Person.prototype 设置为等于一个以对象字面量形式创建的新对象。最终结果和给原型对象一个一个单独添加这些属性和方法相同，**但有一点不同：constructor 属性不再指向Person 了**。前面曾经介绍过，每创建一个函数，就会同时创建它的prototype 对象，这个对象也会自动获得constructor 属性。而我们在这里使用的语法，**本质上完全重写了（覆盖）默认的prototype 对象**，因此constructor 属性也就变成了新对象的constructor 属性（指向Object 构造函数），不再指向Person 函数。此时，尽管instanceof操作符还能返回正确的结果，但通过constructor 已经无法确定对象的类型了。

    ```javascript
    var friend = new Person();
    friend instanceof Object; //true
    friend instanceof Person; //true
    friend.constructor == Person; //false
    friend.constructor == Object; //true
    ```

    如果constructor 的值真的很重要，可以像下面这样特意将它设置回适当的值。

    ```javascript
    function Person() {}
    Person.prototype = {
        constructor: Person,
        name: "Nicholas",
        age: 29,
        job: "Software Engineer",
        sayName: function () {
            alert(this.name);
        }
    };
    /* 注意，以这种方式重设constructor 属性会导致它的[[Enumerable]]特性被设置为true。默认
    情况下，原生的constructor 属性是不可枚举的，因此如果你使用兼容ECMAScript 5 的JavaScript 引
    擎，可以使用Object.defineProperty()来为原型对象定义该属性 */
    ```

4. 原型的动态性

    由于在原型中查找值的过程是一次搜索，因此我们对原型对象所做的任何修改都能够立即从实例上反映出来——即使是先创建了实例后修改原型也照样如此

    ```javascript
    var friend = new Person();
    Person.prototype.sayHi = function () {
        alert("hi");
    };
    friend.sayHi(); //"hi"（没有问题！）
    ```

    尽管可以随时为原型添加属性和方法，并且修改能够立即在所有对象实例中反映出来，但如果是重写整个原型对象，那么情况就不一样了。我们知道，**调用构造函数时会为实例添加一个指向最初原型的[[Prototype]]（调用构造函数时的构造函数prototype的）指针，而把原型修改为另外一个对象就等于切断了构造函数与最初原型之间的联系。请记住：实例中的指针仅指向(创建该实例时的)原型，而不指向构造函数**。

5. 原生对象的原型

    原型模式的重要性不仅体现在创建自定义类型方面，就连所有原生的引用类型，都是采用这种模式创建的。所有原生引用类型（Object、Array、String，等等）都在其构造函数的原型上定义了方法。例如，在Array.prototype 中可以找到sort()方法，而在String.prototype 中可以找到substring()方法。

    通过原生对象的原型，不仅可以取得所有默认方法的引用，而且也可以定义新方法。可以像修改自定义对象的原型一样修改原生对象的原型，因此可以随时添加方法。下面的代码就给基本包装类型String 添加了一个名为startsWith()的方法。

    ```javascript

    /* 这里新定义的startsWith()方法会在传入的文本位于一个字符串开始时返回true。既然方法被
    添加给了String.prototype，那么当前环境中的所有字符串就都可以调用它。由于msg 是字符串，
    而且后台会调用String 基本包装函数创建这个字符串，因此通过msg 就可以调用startsWith()方法。*/
    String.prototype.startsWith = function (text) {
    return this.indexOf(text) == 0;
    };
    var msg = "Hello world!";
    alert(msg.startsWith("Hello")); //true

    /* 尽管可以这样做，但我们不推荐在产品化的程序中修改原生对象的原型。如果因
    某个实现中缺少某个方法，就在原生对象的原型中添加这个方法，那么当在另一个支
    持该方法的实现中运行代码时，就可能会导致命名冲突。而且，这样做也可能会意外
    地重写原生方法。 */
    ```

6. 原型对象的问题

    原型模式也不是没有缺点。首先，它省略了为构造函数传递初始化参数这一环节，结果所有实例在默认情况下都将取得相同的属性值。虽然这会在某种程度上带来一些不方便，但还不是原型的最大问题。原型模式的最大问题是由其共享的本性所导致的。

    原型中所有属性是被很多实例共享的，这种共享对于函数非常合适。对于那些包含基本值的属性倒也说得过去，毕竟（如前面的例子所示），通过在实例上添加一个同名属性，可以隐藏原型中的对应属性。然而，**对于包含引用类型值的属性来说，问题就比较突了**。例如：

    ```javascript
    function Person() {}
    Person.prototype = {
        constructor: Person,
        name: "Nicholas",
        age: 29,
        job: "Software Engineer",
        friends: ["Shelby", "Court"],
        sayName: function () {
            alert(this.name);
        }
    };
    var person1 = new Person();
    var person2 = new Person();
    person1.friends.push("Van");
    alert(person1.friends); //"Shelby,Court,Van"
    alert(person2.friends); //"Shelby,Court,Van"
    alert(person1.friends === person2.friends); //true
    ```

    在此，Person.prototype 对象有一个名为friends 的属性，该属性包含一个字符串数组。然后，创建了Person 的两个实例。接着，修改了person1.friends 引用的数组，向数组中添加了一个字符串。由于friends 数组存在于Person.prototype 而非person1 中，所以刚刚提到的修改也会通过person2.friends（与person1.friends 指向同一个数组）反映出来。假如我们的初衷就是像这样在所有实例中共享一个数组，那么对这个结果我没有话可说。可是，**实例一般都是要有属于自己的独立属性的。而这个问题正是我们很少看到有人单独使用原型模式的原因所在。**

#### 结合构造函数模式和原型模式

创建自定义类型的最常见方式，就是组合使用构造函数模式与原型模式。构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。结果，每个实例都会有自己的一份实例属性的副本，但同时又共享着对方法的引用，最大限度地节省了内存。另外，这种混成模式还支持向构造函数传递参数；可谓是集两种模式之长。

```javascript
function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.friends = ["Shelby", "Court"];
}
Person.prototype = {
    constructor: Person,
    sayName: function () {
        alert(this.name);
    }
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
person1.friends.push("Van");
alert(person1.friends); //"Shelby,Count,Van"
alert(person2.friends); //"Shelby,Count"
alert(person1.friends === person2.friends); //false
alert(person1.sayName === person2.sayName); //true

/* 在这个例子中，实例属性都是在构造函数中定义的，而由所有实例共享的属性constructor 和方法sayName()则是在原型中定义的。*/
```

这种构造函数与原型混成的模式，是目前在ECMAScript 中使用最广泛、认同度最高的一种创建自定义类型的方法。可以说，这是用来定义引用类型的一种默认模式。

#### 动态原型模式

有其他OO 语言经验的开发人员在看到独立的构造函数和原型时，很可能会感到非常困惑。动态原型模式正是致力于解决这个问题的一个方案，**它把所有信息都封装在了构造函数中，而通过在构造函数中初始化原型（仅在必要的情况下），又保持了同时使用构造函数和原型的优点**。换句话说，**可以通过检查某个应该存在的方法是否有效，来决定是否需要初始化原型**。

```javascript
function Person(name, age, job) {
    //属性
    this.name = name;
    this.age = age;
    this.job = job;
    if (typeof this.sayName != "function") {
        Person.prototype.sayName = function () {
            alert(this.name);
        };
    }
}
var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName();
```

注意构造函数代码中加粗的部分。这里只在sayName()方法不存在的情况下，才会将它添加到原型中。这段代码只会在初次调用构造函数时才会执行。此后，原型已经完成初始化，不会再执行对应的prototype对象的修改代码。不过要记住，这里对原型所做的修改，能够立即在所有实例中得到反映。因此，这种方法确实可以说非常完美。其中，**if 语句检查的可以是初始化之后应该存在的任何属性或方法——不必用一大堆if 语句检查每个属性和每个方法；只要检查其中一个即可**。对于采用这种模式创建的对象，还可以使用instanceof 操作符确定它的类型。

#### 寄生构造函数模式

通常，在前述的几种模式都不适用的情况下，可以使用寄生（parasitic）构造函数模式。这种模式的基本思想是创建一个函数，该函数的作用仅仅是封装创建对象的代码，然后再返回新创建的对象；但从表面上看，这个函数又很像是典型的构造函数。eg:

```javascript
function Person(name, age, job) {
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function () {
        alert(this.name);
    };
    return o;
}
var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName(); //"Nicholas"
```

在这个例子中，Person 函数创建了一个新对象，并以相应的属性和方法初始化该对象，然后又返回了这个对象。**除了使用new 操作符并把使用的包装函数叫做构造函数之外，这个模式跟工厂模式其实是一模一样的**。**构造函数在不返回值的情况下，默认会返回新对象实例。而通过在构造函数的末尾添加一个return 语句，可以重写调用构造函数时返回的值**。

这个模式可以在特殊的情况下用来为对象创建构造函数。假设我们想创建一个具有额外方法的特殊数组。由于不能直接修改Array 构造函
数，因此可以使用这个模式。

```javascript
function SpecialArray() {
    //创建数组
    var values = new Array();
    //添加值
    values.push.apply(values, arguments);
    //添加方法
    values.toPipedString = function () {
        return this.join("|");
    };
    //返回数组
    return values;
}
var colors = new SpecialArray("red", "blue", "green");
alert(colors.toPipedString()); //"red|blue|green"
```

关于寄生构造函数模式，有一点需要说明：首先，返回的对象与构造函数或者与构造函数的原型属性之间没有关系；也就是说，构造函数返回的对象与在构造函数外部创建的对象没有什么不同。因此，不能依赖instanceof 操作符来确定对象类型。由于存在上述问题，我们建议在可以使用其他模式的情况下，不要使用这种模式。

#### 稳妥构造函数模式

**所谓稳妥对象，指的是没有公共属性，而且其方法也不引用this 的对象**。稳妥对象最适合在一些安全的环境中（这些环境中会禁止使用this 和new），或者在防止数据被其他应用程序（如Mashup程序）改动时使用。稳妥构造函数遵循与寄生构造函数类似的模式，但有两点不同：**一是新创建对象的实例方法不引用this；二是不使用new 操作符调用构造函数**。按照稳妥构造函数的要求，可以将前面的Person 构造函数重写如下。

```javascript
function Person(name, age, job) {
    //创建要返回的对象
    var o = new Object();
    //可以在这里定义私有变量和函数
    //添加方法
    o.sayName = function () {
        alert(name);
    };
    //返回对象
    return o;
}

var friend = Person("Nicholas", 29, "Software Engineer");
friend.sayName(); //"Nicholas"
```

这样，变量friend 中保存的是一个稳妥对象，而除了调用sayName()方法外，没有别的方式可以访问其数据成员。即使有其他代码会给这个对象添加方法或数据成员，但也不可能有别的办法访问传入到构造函数中的原始数据。稳妥构造函数模式提供的这种安全性，使得它非常适合在某些安全执行环境——例如，ADsafe（<www.adsafe.org>）和Caja（<http://code.google.com/p/google-caja/>）提供的环境——下使用。

tip:与寄生构造函数模式类似，使用稳妥构造函数模式创建的对象与构造函数之间也没有什么关系，因此instanceof 操作符对这种对象也没有意义。

### 6.3 继承

继承是OO 语言中的一个最为人津津乐道的概念。许多OO 语言都支持两种继承方式：接口继承和实现继承。接口继承只继承方法签名，而实现继承则继承实际的方法。如前所述，由于函数没有签名，在ECMAScript 中无法实现接口继承。ECMAScript 只支持实现继承，而且其实现继承主要是依靠原型链来实现的。

#### 原型链

ECMAScript 中描述了原型链的概念，并将原型链作为实现继承的主要方法。其基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法。

简单回顾一下构造函数、原型和实例的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。**那么，假如我们让原型对象等于另一个类型的实例，结果会怎么样呢？显然，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原型又是另一个类型的实例，那么上述关系依然成立，如此层层递进，就构成了实例与原型的链条。**这就是所谓原型链的基本概念。

实现原型链有一种基本模式，其代码大致如下：

```javascript
function SuperType() {
    this.property = true;
}
SuperType.prototype.getSuperValue = function () {
    return this.property;
};

function SubType() {
    this.subproperty = false;
}
//继承了SuperType
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function () {
    return this.subproperty;
};
var instance = new SubType();
alert(instance.getSuperValue()); //true
```