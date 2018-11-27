# JAVA 8实战笔记

## 目录

- [JAVA 8实战笔记](#java-8%E5%AE%9E%E6%88%98%E7%AC%94%E8%AE%B0)
    - [目录](#%E7%9B%AE%E5%BD%95)
    - [一、 lambda表达式:java中对函数式编程的支持](#%E4%B8%80-lambda%E8%A1%A8%E8%BE%BE%E5%BC%8Fjava%E4%B8%AD%E5%AF%B9%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B%E7%9A%84%E6%94%AF%E6%8C%81)
        - [1. 基本概念](#1-%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)
            - [1.1 什么是函数式编程](#11-%E4%BB%80%E4%B9%88%E6%98%AF%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B)
            - [1.2 lambda表达式是什么？](#12-lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%98%AF%E4%BB%80%E4%B9%88)
            - [1.3 在java如何表示](#13-%E5%9C%A8java%E5%A6%82%E4%BD%95%E8%A1%A8%E7%A4%BA)
        - [2. 函数式接口：只有一个抽象方法的接口](#2-%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3%E5%8F%AA%E6%9C%89%E4%B8%80%E4%B8%AA%E6%8A%BD%E8%B1%A1%E6%96%B9%E6%B3%95%E7%9A%84%E6%8E%A5%E5%8F%A3)
        - [3. lambda表达式](#3-lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F)
            - [3.1 类型检查、类型推断以及限制](#31-%E7%B1%BB%E5%9E%8B%E6%A3%80%E6%9F%A5%E7%B1%BB%E5%9E%8B%E6%8E%A8%E6%96%AD%E4%BB%A5%E5%8F%8A%E9%99%90%E5%88%B6)
            - [3.2 方法引用：lambda表达式的语法糖,即直接引用现有方法](#32-%E6%96%B9%E6%B3%95%E5%BC%95%E7%94%A8lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F%E7%9A%84%E8%AF%AD%E6%B3%95%E7%B3%96%E5%8D%B3%E7%9B%B4%E6%8E%A5%E5%BC%95%E7%94%A8%E7%8E%B0%E6%9C%89%E6%96%B9%E6%B3%95)
            - [3.3 构造函数引用](#33-%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%E5%BC%95%E7%94%A8)
            - [3.4 复合表达式(利用默认方法实现)](#34-%E5%A4%8D%E5%90%88%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%88%A9%E7%94%A8%E9%BB%98%E8%AE%A4%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)
    - [二、默认方法](#%E4%BA%8C%E9%BB%98%E8%AE%A4%E6%96%B9%E6%B3%95)
    - [三、流：函数式数据处理](#%E4%B8%89%E6%B5%81%E5%87%BD%E6%95%B0%E5%BC%8F%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86)
        - [1. 流的基本概念](#1-%E6%B5%81%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)
            - [1.1 流是什么](#11-%E6%B5%81%E6%98%AF%E4%BB%80%E4%B9%88)
        - [2. 流与集合](#2-%E6%B5%81%E4%B8%8E%E9%9B%86%E5%90%88)
            - [1. 只能遍历(消费)一次](#1-%E5%8F%AA%E8%83%BD%E9%81%8D%E5%8E%86%E6%B6%88%E8%B4%B9%E4%B8%80%E6%AC%A1)
            - [2. 外部迭代与内部迭代](#2-%E5%A4%96%E9%83%A8%E8%BF%AD%E4%BB%A3%E4%B8%8E%E5%86%85%E9%83%A8%E8%BF%AD%E4%BB%A3)
        - [3. 流的操作（StreamOps:intermediate和terminal）](#3-%E6%B5%81%E7%9A%84%E6%93%8D%E4%BD%9Cstreamopsintermediate%E5%92%8Cterminal)
            - [1. intermediate操作](#1-intermediate%E6%93%8D%E4%BD%9C)
            - [2. terminal操作](#2-terminal%E6%93%8D%E4%BD%9C)
            - [3. 使用流](#3-%E4%BD%BF%E7%94%A8%E6%B5%81)
        - [4. 使用流 （详见api doc）](#4-%E4%BD%BF%E7%94%A8%E6%B5%81-%E8%AF%A6%E8%A7%81api-doc)
            - [4.1 筛选和切片](#41-%E7%AD%9B%E9%80%89%E5%92%8C%E5%88%87%E7%89%87)
            - [2. 映射](#2-%E6%98%A0%E5%B0%84)
                - [4.2.1 flatMap:流的扁平化映射(重要)](#421-flatmap%E6%B5%81%E7%9A%84%E6%89%81%E5%B9%B3%E5%8C%96%E6%98%A0%E5%B0%84%E9%87%8D%E8%A6%81)
            - [4.3 查找和匹配(短路)](#43-%E6%9F%A5%E6%89%BE%E5%92%8C%E5%8C%B9%E9%85%8D%E7%9F%AD%E8%B7%AF)
            - [5. reduce(归约)](#5-reduce%E5%BD%92%E7%BA%A6)
                - [5.1 元素求和](#51-%E5%85%83%E7%B4%A0%E6%B1%82%E5%92%8C)
                - [5.2 归约方法的优势与并行化](#52-%E5%BD%92%E7%BA%A6%E6%96%B9%E6%B3%95%E7%9A%84%E4%BC%98%E5%8A%BF%E4%B8%8E%E5%B9%B6%E8%A1%8C%E5%8C%96)
            - [5.3 有状态和无状态](#53-%E6%9C%89%E7%8A%B6%E6%80%81%E5%92%8C%E6%97%A0%E7%8A%B6%E6%80%81)
            - [6. 数值流](#6-%E6%95%B0%E5%80%BC%E6%B5%81)
                - [6.1 映射到数值流](#61-%E6%98%A0%E5%B0%84%E5%88%B0%E6%95%B0%E5%80%BC%E6%B5%81)
                - [6.2 转换回对象流](#62-%E8%BD%AC%E6%8D%A2%E5%9B%9E%E5%AF%B9%E8%B1%A1%E6%B5%81)
                - [6.3 默认值OptionalInt](#63-%E9%BB%98%E8%AE%A4%E5%80%BCoptionalint)
                - [6.4 生成数值范围的流](#64-%E7%94%9F%E6%88%90%E6%95%B0%E5%80%BC%E8%8C%83%E5%9B%B4%E7%9A%84%E6%B5%81)
            - [7. 多数据源构建流](#7-%E5%A4%9A%E6%95%B0%E6%8D%AE%E6%BA%90%E6%9E%84%E5%BB%BA%E6%B5%81)
                - [7.1 由值创建流：stream.of()](#71-%E7%94%B1%E5%80%BC%E5%88%9B%E5%BB%BA%E6%B5%81streamof)
                - [7.2 由数组创建流:Arrays.stream()](#72-%E7%94%B1%E6%95%B0%E7%BB%84%E5%88%9B%E5%BB%BA%E6%B5%81arraysstream)
                - [7.3 由文件生成流](#73-%E7%94%B1%E6%96%87%E4%BB%B6%E7%94%9F%E6%88%90%E6%B5%81)
                - [7.4 由函数生成流：创建无界流](#74-%E7%94%B1%E5%87%BD%E6%95%B0%E7%94%9F%E6%88%90%E6%B5%81%E5%88%9B%E5%BB%BA%E6%97%A0%E7%95%8C%E6%B5%81)

1. 主要内容
   - lambda表达式
   - 默认方法
   - 新的集合处理api：流
   - 新日期api: java.time

## 一、 lambda表达式:java中对函数式编程的支持

### 1. 基本概念

#### 1.1 什么是函数式编程

函数式编程（英语：functional programming）或称函数程序设计，又称泛函编程，是一种编程典范，它将**计算机运算**视为数学上的函数计算，并且避免使用程序状态以及易变对象。函数编程语言最重要的基础是**λ演算**（lambda calculus）。而且λ演算的函数可以接受函数当作输入（引数）和输出（传出值）。

#### 1.2 lambda表达式是什么？

其实就是不同程序语言对λ演算的实现。

#### 1.3 在java如何表示

java中的lambda表达式：其思想就是行为参数化（函数化），本质上是匿名函数的语言糖。

eg: () -> {}

### 2. 函数式接口：只有一个抽象方法的接口

1. 作用：函数描述符，声明该lambda表达式的输入(参数)/输出(返回值),即lambda表达式的方法签名。如 () -> Void,(Apple,Apple) -> int
2. @FunctionalInterface：编译时注解，告诉编译器以函数式接口的标准检查。
3. 为什么函数式接口只能有一个未实现的抽象方法：因为使用lambda表达式实际上还是传递的匿名对象，如果有两个抽象方法，java中要求该它的子类对象必须实现所有的方法，这样就不能写成现在的形式，故做了这样的规定。

### 3. lambda表达式

#### 3.1 类型检查、类型推断以及限制

1. 类型检查

    Lambda的类型是从使用Lambda的上下文推断出来的。上下文（比如，接受它传递的方法的
    参数，或接受它的值的局部变量）中Lambda表达式需要的类型称为目标类型。

    ```java
    // 接口声明
    filter(inventory, Predicate<Apple> p);

    //调用
    List<Apple> heavierThan150g =
    filter(inventory, (Apple a) -> a.getWeight() > 150);
    ```

    类型检查的过程：

    - 首先，你要找出filter方法的声明。
    - 第二，要求它是Predicate\<Apple>（目标类型）对象的第二个正式参数。
    - 第三，Predicate\<Apple>是一个函数式接口，定义了一个叫作test的抽象方法。
    - 第四，test方法描述了一个函数描述符，它可以接受一个Apple，并返回一个boolean。
    - 最后，filter的任何实际参数都必须匹配这个要求。即函数表达式必须是(Apple) -> boolean

2. 类型推断

    Java编译器会从上下文（目标类型）推断出用什么函数式接
    口来配合Lambda表达式，这意味着它也可以推断出适合Lambda的签名，因为函数描述符可以通
    过目标类型来得到。这样做的好处在于，编译器可以了解Lambda表达式的参数类型，这样就可
    以在Lambda语法中省去标注参数类型。换句话说，Java编译器会像下面这样推断Lambda的参数
    类型：

    ```java
    // 没有类型推断
    Comparator<Apple> c =
    (Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());

    // 使用类型推断
    Comparator<Apple> c =
    (a1, a2) -> a1.getWeight().compareTo(a2.getWeight());
    ```

3. 在lambda中使用局部变量的限制（和匿名内部类使用外部类的局部变量的限制一样）

    对局部变量的限制
    你可能会问自己，为什么局部变量有这些限制。第一，实例变量和局部变量背后的实现有一
    个关键不同。实例变量都存储在堆中，而局部变量则保存在栈上（不同的线程不共享栈空间）。如果Lambda可以直接访问局
    部变量，而且Lambda是在一个线程中使用的，则使用Lambda的线程，可能会在分配该变量的线
    程将这个变量收回之后，去访问该变量。因此，Java在访问自由局部变量时，实际上是在访问它
    的副本，而不是访问原始变量。如果局部变量仅仅赋值一次那就没有什么区别了——因此就有了
    这个限制。
    第二，这一限制不鼓励你使用改变外部变量的典型命令式编程模式（我们会在以后的各章中
    解释，这种模式会阻碍很容易做到的并行处理）。

>闭包
你可能已经听说过闭包（closure，不要和Clojure编程语言混淆）这个词，你可能会想
Lambda是否满足闭包的定义。用科学的说法来说，闭包就是一个函数的实例，且它可以无限
制地访问那个函数的非本地变量。例如，闭包可以作为参数传递给另一个函数。它也可以访
问和修改其作用域之外的变量。现在，Java 8的Lambda和匿名类可以做类似于闭包的事情：
它们可以作为参数传递给方法，并且可以访问其作用域之外的变量。但有一个限制：它们不
能修改定义Lambda的方法的局部变量的内容。这些变量必须是隐式最终的。可以认为Lambda
是对值封闭，而不是对变量封闭。如前所述，这种限制存在的原因在于局部变量保存在栈上，
并且隐式表示它们仅限于其所在线程。如果允许捕获可改变的局部变量，就会引发造成线程
不安全的新的可能性，而这是我们不想看到的（实例变量可以，因为它们保存在堆中，而堆
是在线程之间共享的）。

#### 3.2 方法引用：lambda表达式的语法糖,即直接引用现有方法

方法引用可以被看作仅仅调用特定方法的Lambda的一种快捷
写法。它的基本思想是，如果一个Lambda代表的只是“直接调用这个方法”，那最好还是用名称
来调用它，而不是去描述如何调用它。事实上，方法引用就是让你根据已有的方法实现来创建
Lambda表达式。但是，显式地指明方法的名称，你的代码的可读性会更好

使用方式 **类名::方法名**

1. 构建方法引用

    - (1)指向静态方法的方法引用（例如Integer的parseInt方法，写作Integer::parseInt）。
    你的第一个
    方法引用！
    - (2)指向任意类型实例方法的方法引用（ 例如String 的length 方法， 写作
    String::length）。
    - (3)指向现有对象的实例方法的方法引用（假设你有一个局部变量expensiveTransaction
    用于存放Transaction类型的对象，它支持实例方法getValue，那么你就可以写expensive
    Transaction::getValue）。

```java
//(1) 调用某个类的静态方法
(args) -> ClassName.staticMethod(args)
等价于 ClassName::staticMethod

//(2) 调用某个类(arg0)的成员方法
(arg0,arg1) -> arg0.invoke(arg1)
等价于 arg0::invoke  

//(3) 调用对象实例的方法
(arg1) -> arg1.invoke()
等价于 arg1::invoke
```

#### 3.3 构造函数引用

```java
Supplier<MyClass> supplier = MyClass::new
等价于
Supplier<MyClass> supplier = () -> new MyClass();
```

#### 3.4 复合表达式(利用默认方法实现)

1. 比较器复合
2. Predicate复合
3. 函数复合:即Function接口复合

总结：

- Lambda表达式可以理解为一种匿名函数：它没有名称，但有参数列表、函数主体、返回类型，可能还有一个可以抛出的异常的列表。
- 函数式接口就是仅仅声明了一个抽象方法的接口。
- 只有在接受函数式接口的地方才可以使用Lambda表达式。
- Lambda表达式允许你直接内联（就像直接new 一个匿名类），为函数式接口的抽象方法提供实现，并且将整个表达式作为函数式接口的一个实例。
- Java 8自带一些常用的函数式接口，放在java.util.function包里，包括Predicate\<T>、Function\<T,R>、Supplier\<T>、Consumer\<T>和BinaryOperator\<T>。为了避免装箱操作，对Predicate\<T>和Function<T, R>等通用函数式接口的原始类型特化：IntPredicate、IntToLongFunction等。
- 关于复合表达式：Comparator、Predicate和Function等函数式接口都有几个可以用来结合Lambda表达式的默认方法。

## 二、默认方法

1. 默认方法的含义及其作用

## 三、流：函数式数据处理

### 1. 流的基本概念

#### 1.1 流是什么

Java 8中的集合支持一个新的
stream方法，它会返回一个流（接口定义在java.util.stream.Stream里）。你在后面会看到，
还有很多其他的方法可以得到流，比如利用数值范围或从I/O资源生成流元素。
那么，流到底是什么呢？简短的定义就是“从支持数据处理操作的源生成的元素序列”

- 元素序列——就像集合一样，流也提供了一个接口，可以访问特定元素类型的一组有序值。因为集合是数据结构，所以它的主要目的是以特定的时间/空间复杂度存储和访问元素（如ArrayList 与 LinkedList）。但流的目的在于表达计算（即对数据集的操作），比如你前面见到的filter、sorted和map。集合讲的是数据，流讲的是计算。
- 源——流会使用一个提供数据的源，如集合、数组或输入/输出资源。 请注意，从有序集合生成流时会保留原有的顺序。由列表生成的流，其元素顺序与列表一致。
- 数据处理操作——流的数据处理功能支持类似于数据库的操作，以及函数式编程语言中的常用操作，如filter、map、reduce、find、match、sort等。流操作可以顺序执行，也可并行执行。

此外，流操作有两个重要的特点。

- 流水线——很多流操作本身会返回一个流，这样多个操作就可以链接起来，形成一个大的流水线。这让一些优化成为可能，如延迟和短路。流水线的操作可以看作对数据源进行数据库式查询。
- 内部迭代——与使用迭代器显式迭代的集合不同，流的迭代操作是在背后进行的

流允许你以声明性方式处理数据集合（通过查询语句来表达，而不
是临时编写一个实现）

特点：

- 声明性：简洁
- 可复合：灵活
- 可并行(**map-reduce**)：性能好

### 2. 流与集合

粗略地说，集合与流之间的差异就在于什么时候进行计算。集合是一个内存中的数据结构，
它包含数据结构中目前所有的值——集合中的每个元素都得先算出来才能添加到集合中。（你可
以往集合里加东西或者删东西，但是不管什么时候，集合中的每个元素都是放在内存里的，元素
都得先算出来才能成为集合的一部分。）
相比之下，流则是在概念上固定的数据结构（你不能添加或删除元素），其元素则是按需计
算的。

#### 1. 只能遍历(消费)一次

和迭代器类似，流只能遍历一次。遍历完之后，我们就说这个流已经被消费掉了。
你可以从原始数据源那里再获得一个新的流来重新遍历一遍，就像迭代器一样（这里假设它是集
合之类的可重复的源，如果是I/O通道就没戏了）

#### 2. 外部迭代与内部迭代

使用Collection接口需要用户去做迭代（比如用for-each），这称为外部迭代。 相反，
Streams库使用内部迭代——它帮你把迭代做了，还把得到的流值存在了某个地方，你只要给出
一个函数说要干什么就可以了。

```java
// for-each迭代
// 请注意，for-each还隐藏了迭代中的一些复杂性。for-each结构是一个语法糖，它背后的东西用Iterator对象表达出来更要丑陋得多。
List<String> names = new ArrayList
for (Dish dish :
        menu) {
    names.add(dish.getName());
}

//(2) 使用iterator
List<String> names = new ArrayList<>();
Iterator<String> iterator = menu.iterator();
while(iterator.hasNext()) {
Dish d = iterator.next();
names.add(d.getName());
}

//(3) 流：内部迭代
List<String> names = menu.stream()
                        .map(Dish::getName)
                        .collect(toList());
```

### 3. 流的操作（StreamOps:intermediate和terminal）

jdk doc说明:
>Stream operations are divided into intermediate and terminal operations, and are combined to form stream pipelines. A stream pipeline consists of a source (such as a Collection, an array, a generator function, or an I/O channel); followed by zero or more intermediate operations such as Stream.filter or Stream.map; and a terminal operation such as Stream.forEach or Stream.reduce.
>
>Intermediate operations return a new stream. They are always **lazy**; **executing an intermediate operation such as filter() does not actually perform any filtering, but instead creates a new stream that**, when traversed, contains the elements of the initial stream that match the given predicate. Traversal of the pipeline source does not begin until the terminal operation of the pipeline is executed.
>
>Terminal operations, such as Stream.forEach or IntStream.sum, may traverse the stream to produce a result or a side-effect. After the terminal operation is performed, the stream pipeline is considered consumed, and can no longer be used; if you need to traverse the same data source again, you must return to the data source to get a new stream. In almost all cases, terminal operations are eager, completing their traversal of the data source and processing of the pipeline before returning. Only the terminal operations **iterator()** and **spliterator()** are not; these are provided as an "escape hatch" to enable arbitrary client-controlled pipeline traversals in the event that the existing operations are not sufficient to the task.

#### 1. intermediate操作

诸如filter或sorted等中间操作会返回另一个流。这让多个操作可以连接起来形成一个查
询。重要的是，除非流水线上触发一个终端操作，否则中间操作不会执行任何处理——它们很懒。
这是因为中间操作一般都可以合并起来，在终端操作时一次性全部处理。

```java
List<String> names =
menu.stream()
.filter(d -> {  // filter
System.out.println("filtering" + d.getName());
return d.getCalories() > 300;
})
.map(d -> { //mapping
System.out.println("mapping" + d.getName());
return d.getName();
})
.limit(3)
.collect(toList());
System.out.println(names);

==//output:
filtering pork
mapping pork
filtering beef
mapping beef
filtering chicken
mapping chicken
[pork, beef, chicken]
```

你会发现，有好几种优化利用了流的延迟性质。第一，尽管很多菜的热量都高于300卡路里，
但只选出了前三个！这是因为limit操作和一种称为**短路**的技巧。第二，
尽管filter和map是两个独立的操作，但它们合并到同一次遍历中了（我们把这种技术叫作**循环合并**）。

#### 2. terminal操作

#### 3. 使用流

- 一个数据源（如集合）来执行一个查询；
- 任意个中间操作链(lazy)，和一个终端操作（迭代此时进行）组成pipeine。
- 当终端操作执行后，流被消耗掉。

### 4. 使用流 （详见api doc）

#### 4.1 筛选和切片

#### 2. 映射

##### 4.2.1 flatMap:流的扁平化映射(重要)

现在让我们回到提取菜名的例子。如果你要找出每道菜的名称有多长，怎么做？你可以像下
面这样，再链接上一个map：

```java
List<Integer> dishNameLengths = menu.stream()
.map(Dish::getName)
.map(String::length)
.collect(toList());
```

你已经看到如何使用map方法返回列表中每个单词的长度了。让我们拓展一下：对于一张单
词表， 如何返回一张列表， 列出里面各不相同的字符呢？ 例如， 给定单词列表
["Hello","World"]，你想要返回列表["H","e","l", "o","W","r","d"]。
你可能会认为这很容易，你可以把每个单词映射成一张字符表，然后调用distinct来过滤
重复的字符。第一个版本可能是这样的：

```java
words.stream() // Stream<String>
.map(word -> word.split("")) //将流的每个元素映射为 String[]
.distinct() //去重
.collect(toList()); //结果为 List<String[]>

/**
这个方法的问题在于，传递给map方法的Lambda为每个单词返回了一个String[]（String
列表）。因此， map 返回的流实际上是Stream<String[]> 类型的。你真正想要的是用
Stream<String>来表示一个字符流。
*/
```

1. 尝试map和Arrays.stream()

   ```java
    words.stream()
    .map(word -> word.split("")) // 将流的每个元素string 映射为 String[]
    .map(Arrays::stream) // 元素string[] 映射为 Stream<String>
    .distinct()
    .collect(toList()); // 结果 List<Stream<String>
   ```

2. 使用flatMap

    ```java
    List<String> uniqueCharacters =
        words.stream()
        .map(w -> w.split(""))
        .flatMap(Arrays::stream) // 将每一个string[] 映射为Stream<String>,并将这些流的内容放入一个统一的结果流.即将Stream<Stream<String>> -> Stream<String>
        .distinct()
        .collect(Collectors.toList()); // List<String>

    /**
    使用flatMap方法的效果是，各个数组并不是分别映射成一个流，而是映射成流的内容。所
    有使用map(Arrays::stream)时生成的单个流都被合并起来，即扁平化为一个流
    */
    ```

#### 4.3 查找和匹配(短路)

    如findAny(),matchAny()

#### 5. reduce(归约)

到目前为止，你见到过的终端操作都是返回一个boolean（allMatch之类的）、void
（forEach）或Optional对象（findAny等）。你也见过了使用collect来将流中的所有元素组
合成一个List。

reduce操作来表达更复杂的查询：当查询需要将流中的所有元素反复结合起来，计算为一个值，这个查询可以被归类为归约操作（将流归约成一个值）。用函数式编程语言的术语来说，这称为折叠（**fold**），因为你可以将这个操作看成把一张长长的纸（你的流）反复折叠成一个小方块，而这就是折叠操作的结果。

##### 5.1 元素求和

```java
int sum = numbers.stream().reduce(0, (a, b) -> a + b);
```

reduce还有一个重载的变体，它不接受初始值，但是会返回一个Optional对象：

```java
Optional<Integer> sum = numbers.stream().reduce((a, b) -> (a + b));
```

为什么它返回一个Optional\<Integer>呢？考虑流中没有任何元素的情况。reduce操作无
法返回其和，因为它没有初始值。这就是为什么结果被包裹在一个Optional对象里，以表明和
可能不存在

##### 5.2 归约方法的优势与并行化

相比于前面写的逐步迭代求和，使用reduce的好处在于，这里的迭代被内部迭代抽象掉
了，这让内部实现得以选择并行执行reduce操作。而迭代式求和例子要更新共享变量sum，
这不是那么容易并行化的。如果你加入了同步，很可能会发现线程竞争抵消了并行本应带来的
性能提升！这种计算的并行化需要另一种办法：将输入分块，分块求和，最后再合并起来。但
这样的话代码看起来就完全不一样了。你在第7章会看到使用分支/合并框架来做是什么样子。
但现在重要的是要认识到，可变的累加器模式对于并行化来说是死路一条。你需要一种新的模
式，这正是reduce所提供的。使用流来对所有的元素并行求和时，你的
代码几乎不用修改：stream()换成了parallelStream()。
int sum = numbers.parallelStream().reduce(0, Integer::sum);
但要并行执行这段代码也要付一定代价：传递给reduce的Lambda
不能更改状态（如实例变量），而且操作必须满足**结合律**才可以按任意顺序执行。

#### 5.3 有状态和无状态

你已经看到了很多的流操作。乍一看流操作简直是灵丹妙药，而且只要在从集合生成流的
时候把Stream换成parallelStream就可以实现并行。
当然，对于许多应用来说确实是这样，就像前面的那些例子。你可以把一张菜单变成流，
用filter选出某一类的菜肴，然后对得到的流做map来对卡路里求和，最后reduce得到菜单
的总热量。这个流计算甚至可以并行进行。但这些操作的特性并不相同。它们需要操作的内部
状态还是有些问题的。
诸如map或filter等操作会从输入流中获取每一个元素，并在输出流中得到0或1个结果。
这些操作一般都是无状态的：它们没有内部状态（假设用户提供的Lambda或方法引用没有内
部可变状态）。
但诸如reduce、sum、max等操作需要内部状态来累积结果。在上面的情况下，内部状态
很小。在我们的例子里就是一个int或double。不管流中有多少元素要处理，内部状态都是有界的。

相反，诸如sort或distinct等操作一开始都和filter和map差不多——都是接受一个
流，再生成一个流（中间操作），但有一个关键的区别。从流中排序和删除重复项时都需要知
道先前的历史。例如，排序要求所有元素都放入缓冲区后才能给输出流加入一个项目，这一操
作的存储要求是无界的。要是流比较大或是无限的，就可能会有问题（把质数流倒序会做什么
呢？它应当返回最大的质数，但数学告诉我们它不存在）。我们把这些操作叫作有状态操作。

简单来说filter和map等操作是无状态的，它们并不存储任何状态。reduce等操作要存储状态才
能计算出一个值。sorted和distinct等操作也要存储状态，因为它们需要把流中的所
有元素缓存起来才能返回一个新的流。这种操作称为有状态操作。

#### 6. 数值流

Java 8引入了三个原始类型特化流接口来解决这个问题：IntStream、DoubleStream和
LongStream，分别将流中的元素特化为int、long和double，从而避免了暗含的装箱成本。每
个接口都带来了进行常用数值归约的新方法，比如对数值流求和的sum，找到最大元素的max。
此外还有在必要时再把它们转换回对象流的方法。要记住的是，这些特化的原因并不在于流的复
杂性，而是装箱造成的复杂性——即类似int和Integer之间的效率差异。

##### 6.1 映射到数值流

##### 6.2 转换回对象流

##### 6.3 默认值OptionalInt

求和的那个例子很容易，因为它有一个默认值：0。但是，如果你要计算IntStream中的最
大元素，就得换个法子了，因为0是错误的结果。如何区分没有元素的流和最大值真的是0的流呢？
前面我们介绍了Optional类，这是一个可以表示值存在或不存在的容器。Optional可以用
Integer、String等参考类型来参数化。对于三种原始流特化，也分别有一个Optional原始类
型特化版本：OptionalInt、OptionalDouble和OptionalLong。

##### 6.4 生成数值范围的流

Java 8引入了两个可以用于IntStream和LongStream的静态方法，帮助生成这种范围：
range和rangeClosed。

#### 7. 多数据源构建流

##### 7.1 由值创建流：stream.of()

##### 7.2 由数组创建流:Arrays.stream()

##### 7.3 由文件生成流

Java中用于处理文件等I/O操作的NIO API（非阻塞 I/O）已更新，以便利用Stream API。
java.nio.file.Files中的很多静态方法都会返回一个流。

##### 7.4 由函数生成流：创建无界流

Stream API提供了两个静态方法来从函数生成流：Stream.iterate（有序）和Stream.generate（无序,有状态）。
