# Spring In Action

Sping是一个模块化框架，目的是简化Java EE应用程序开发(最初是用来替代更加重量级的企业级Java技术，尤其是EJB)。

本书涵盖了Spring框架的许多领域，既有核心框架，也有各种功能扩展，不少的同学曾经对我言及，感觉书中所讲述的内容深度不够，但是我个人认为，对于开源框架的学习，我们会有不同的掌握深度，从最初始的使用、配置，到设计原理，再到源码分析，一本书很难面面俱到深入介绍所有的内容，但是它却能够提供一个方向，让我们按图索骥深入学习更多的知识。

## 一、 Spring Core

## 1. Spring简介

在诞生之初，创建Spring的主要目的是用来替代更加重量级的企业级Java技术，尤其是EJB。相
对于EJB来说，Spring提供了更加轻量级和简单的编程模型。它增强了简单老式Java对象（Plain
Old Java object，POJO）的功能，使其具备了之前只有EJB和其他企业级Java规范才具有的功
能。

随着时间的推移，EJB以及Java 2企业版（Java 2 Enterprise Edition，J2EE）在不断演化。EJB自身也提供了面向简单POJO的编程模型。现在，EJB也采用了依赖注入（Dependency Injection，DI）和面向切面编程（Aspect-Oriented Programming，AOP）的理念，这毫无疑问是受到Spring成功的启发。

尽管J2EE（现在称之为JEE）能够赶上Spring的步伐，但Spring也没有停止前进。Spring继续在其他领域发展，而JEE则刚刚开始涉及这些领域，或者还完全没有开始在这些领域的创新。移动开发、社交API集成、NoSQL数据库、云计算以及大数据都是Spring正在涉足和创新的领域。Spring的前景依然会很美好。

### 1.1 简化Java EE开发

Spring是为了解决企业级应用开发的复杂性而创建的，使用Spring可以让简单的JavaBean实现之前只有EJB才能完成的事情。但Spring不仅仅局限于服务器端开发，任何Java应用都能在简单性、可测试性和松耦合等方面从Spring中获益。

为了降低Java开发的复杂性，Spring采取了以下4种关键策略：

- 基于POJO的轻量级和最小侵入性编程；
- 通过依赖注入和面向接口实现松耦合；
- 基于切面和惯例进行声明式编程；
- 通过切面和模板减少样板式代码。

#### 基于POJO

如果你从事Java编程有一段时间了，那么你或许会发现（可能你也实际使用过）很多框架通过强迫应用继承它们的类或实现它们的接口从而导致应用与框架绑死。

Spring竭力避免因自身的API而弄乱你的应用代码。Spring不会强迫你实现Spring规范的接口或继承Spring规范的类，相反，在基于Spring构建的应用中，它的类通常没有任何痕迹表明你使用了Spring。**最坏的场景是，一个类或许会使用Spring注解**，但它依旧是POJO。

```java
/*
可以看到，这是一个简单普通的Java类——POJO。没有任何地方表明它是一个Spring组件。Spring的非侵入编程模型意味着这个类在Spring应用和非Spring应用中都可以发挥同样的作用。
*/
package com.zyy.spring
public class HelloWorld  {
    public String sayHello() {
        return "Hello World";
    }
}
```

Spring赋予POJO魔力的方式之一就是通过DI来装配它们,使应用对象之间保持松耦合。

#### 依赖注入(Dependency Injection，DI)

注入：对象不由自己创建，由外部(第三方框架通过参数)传递进来。
装配：创建应用组件之间协作的行为通常称为装配（wiring）。

任何一个有实际意义的应用都会由两个或者更多的类组成，这些类相互之间进行协作来完成特定的业务逻辑。按照传统的做法，每个对象负责管理与自己相互协作的对象（即它所依赖的对象）的引用，这将会导致高度耦合和难以测试的代码。

耦合具有两面性（two-headed beast）。一方面，紧密耦的代码难以测试、难以复用、难以理解，并且典型地表现出“打地鼠”式的bug特性（修复一个bug将会出现一个或者更多新的bug）。另一方面，一定程度的耦合又是必须的——完全没有耦合的代什么也做不了。为了完成有实际意义的功能，不同的类必须以适当的方式进行交互。总言之，耦合是必须的，但应当被小心谨慎地管理。

通过DI，对象的依赖关系将由系统中负责协调各对象的第三方组件在创建对象的时候进行设定。对象无需自行创建或管理它们的依赖关系，依赖关系将被自动注入到需要它们的对象当中去。

![DI](/imgs/di.png)

Spring中通过DI装配的工作流程：

    1. 创建/获取上下文对象
    2. 获取bean对象(通过配置自动生成)
    3. 使用bean对象
    4. 释放上下文

Spring通过应用上下文（Application Context）装载bean的定义并把它们组装起来。Spring应用上下文全权负责对象的创建和组装。Spring自带了多种应用上下文的实现，它们之间主要的区别仅仅在于如何加载配置。

#### 应用切面（aspect-oriented programming，AOP）：基于切面进行声明式编程

DI能够让相互协作的软件组件保持松散耦合，**而AOP允许你把遍布应用各处的功能分离出来形成可重用的组件**。

面向切面编程往往被定义为促使软件系统实现**关注点**的分离一项技术。系统由许多不同的组件组成，每一个组件各负责一块特定功能。除了实现自身核心的功能之外，这些组件还经常承担着额外的职责。诸如日志、事务管理和安全这样的系统服务经常融入到自身具有核心业务逻辑的组件中去，**这些系统服务通常被称为横切关注点**，因为它们会跨越系统的多个组件。

如果将这些关注点分散到多个组件中去，你的代码将会带来双重的复杂性。

- 实现系统关注点功能的代码将会重复出现在多个组件中。这意味着如果你要改变这些关注点的逻辑，必须修改各个模块中的相关实现。即使你把这些关注点抽象为一个独立的模块，其他模块只是调用它的方法，但方法的调用还是会重复出现在各个模块中。
- 组件会因为那些与自身核心业务无关的代码而变得混乱。一个向地址簿增加地址条目的方法应该只关注如何添加地址，而不应该关注它是不是安全的或者是否需要支持事务。

下图展示了这种复杂性。左边的业务对象与系统级服务结合得过于紧密。每个对象不但要知道它需要记日志、进行安全控制和参与事务，还要亲自执行这些服务。在整个系统内，关注点（例如日志和安全）的调用经常散布到各个模块中，而这些关注点并不是模块的核心业务

![传统方式](/imgs/tranditional_constructor.png)

AOP能够使这些服务模块化，并以声明的方式将它们应用到它们需要影响的组件中去。所造成的结果就是这些组件会具有更高的内聚性并且会更加关注自身的业务，完全不需要了解涉及系统服务所带来复杂性。总之，AOP能够确保POJO的简单性。

我们可以把切面想象为覆盖在很多组件之上的一个外壳。应用是由那些实现各自业务功能的模块组成的。借助AOP，可以使用各种功能层去包裹核心业务层。这些层以声明的方式灵活地应用到系统中，你的核心应用甚至根本不知道它们的存在。这是一个非常强大的理念，可以将安全、事务和日志关注点与核心业务逻辑相分离。

![AOP](/imgs/aop.png)利用AOP，系统范围内的关注点覆盖在它们所影响组件之上.

相关概念：AspectJ

#### 使用模板消除样板式（boilerplate code)代码

### 1.2 容纳你的Bean

在基于Spring的应用中，你的应用对象生存于Spring容器（container）中。Spring容器负责创建对象，装配它们，配置它们并管理它们的整个生命周期。

容器是Spring框架的核心。Spring容器并不是只有一个。Spring自带了多个容器实现，可以归为两种不同的类型。**bean工厂**（由org.springframework. beans. factory.eanFactory接口定义）是最简单的容器，提供基本的DI支持。**应用上下文**（由org.springframework.context.ApplicationContext接口定义）基于BeanFactory构建，并提供应用框架级别的服务，例如从属性文件解析文本信息以及发布应用事件给感兴趣的事件监听者。

#### 使用ApplicationContext

- AnnotationConfigApplicationContext：从一个或多个基于Java的配置类中加载Spring应用上下文。
- AnnotationConfigWebApplicationContext：从一个或多个基于Java的配置类中加载Spring Web应用上下文。
- ClassPathXmlApplicationContext：从类路径下的一个或多个XML配置文件中加载上下文定义，把应用上下文的定义文件作为类资源。
- FileSystemXmlapplicationcontext：从文件系统下的一个或多个XML配置文件中加载上下文定义。
- XmlWebApplicationContext：从Web应用下的一个或多个XML配置文件中加载上下文定义。

#### bean的生命周期

![bean's lifycycle](/imgs/lifecycle_bean.png)bean在Spring容器中从创建到销毁经历了若干阶段，每一阶段都可以针对Spring如何管理bean进行个性化定制

1. Spring对bean进行实例化；
2. Spring将值和bean的引用注入到bean对应的属性中；
3. 如果bean实现了BeanNameAware接口，Spring将bean的ID传递给setBean-Name()方法；
4. 如果bean实现了BeanFactoryAware接口，Spring将调用setBeanFactory()方法，将BeanFactory容器实例传入；
5. 如果bean实现了ApplicationContextAware接口，Spring将调用setApplicationContext()方法，将bean所在的应用上下文的引用传入进来；
6. 如果bean实现了BeanPostProcessor接口，Spring将调用它们的post-ProcessBeforeInitialization()方法；
7. 如果bean实现了InitializingBean接口，Spring将调用它们的after-PropertiesSet()方法。类似地，如果bean使用init-method声明了初始化方法，该方法也会被调用；
8. 如果bean实现了BeanPostProcessor接口，Spring将调用它们的post-ProcessAfterInitialization()方法；
9. 此时，bean已经准备就绪，可以被应用程序使用了，它们将一直驻留在应用上下文中，直到该应用上下文被销毁；
10. 如果bean实现了DisposableBean接口，Spring将调用它的destroy()接口方法。同样，如果bean使用destroy-method声明了销毁方法，该方法也会被调用。

### 1.3 了解Spring体系(生态)

在Spring框架的范畴内，你会发现Spring简化Java开发的多种方式。但在Spring框架之外还存在一个构建在核心框架之上的庞大生态圈，它将Spring扩展到不同的领域，例如Web服务、REST、移动开发以及NoSQL。

#### SpringFramework

![Spring Framework](/imgs/Spring_framework.png)

总体而言，这些模块为开发企业级应用提供了所需的一切。但是你也不必将应用建立在整个Spring框架之上，你可以自由地选择适合自身应用需求的Spring模块；当Spring不能满足需求时，完全可以考虑其他选择。事实上，Spring甚至提供了与其他第三方框架和类库的集成点，这样你就不需要自己编写这样的代码了。

1. Spring核心容器

    容器是Spring框架最核心的部分，它管理着Spring应用中bean的创建、配置和管理。在该模块中，包括了Spring bean工厂，它为Spring提供了DI的功能。基于bean工厂，我们还会发现有多种Spring应用上下文的实现，每一种都提供了配置Spring的不同方式。除了bean工厂和应用上下文，该模块也提供了许多企业服务，例如E-mail、JNDI访问、EJB集成和调度。所有的Spring模块都构建于核心容器之上。当你配置应用时，其实你隐式地使用了这些类。

2. Spring的AOP模块

    在AOP模块中，Spring对面向切面编程提供了丰富的支持。这个模块是Spring应用系统中开发切面的基础。与DI一样，AOP可以帮助应用对象解耦。借助于AOP，可以将遍布系统的关注点（例如事务和安全）从它们所应用的对象中解耦出来。

3. 数据访问与集成

    使用JDBC编写代码通常会导致大量的样板式代码，例如获得数据库连接、创建语句、处理结果集到最后关闭数据库连接。Spring的JDBC和DAO（Data Access Object）模块抽象了这些样板式代码，使我们的数据库代码变得简单明了，还可以避免因为关闭数据库资源失败而引发的问题。该模块在多种数据库服务的错误信息之上构建了一个语义丰富的异常层，以后我们再也不需要解释那些隐晦专有的SQL错误信息了！

    对于那些更喜欢ORM（Object-Relational Mapping）工具而不愿意直接使用JDBC的开发者，Spring提供了ORM模块。Spring的ORM模块建立在对DAO的支持之上，并为多个ORM框架提供了一种构建DAO的简便方式。Spring没有尝试去创建自己的ORM解决方案，而是对许多流行的ORM框架进行了集成，包括Hibernate、Java Persisternce API、Java Data Object和iBATISSQL Maps。Spring的事务管理支持所有的ORM框架以及JDBC。

4. JMS

    本模块同样包含了在JMS（Java Message Service）之上构建的Spring抽象层，它会使用消息以异步的方式与其他应用集成。从Spring 3.0开始，本模块还包含对象到XML映射的特性，它最初是Spring Web Service项目的一部分。

    除此之外，本模块会使用Spring AOP模块为Spring应用中的对象提供事务管理服务。

5. Web与远程调用

    MVC（Model-View-Controller）模式是一种普遍被接受的构建Web应用的方法，它可以帮助用户将界面逻辑与应用逻辑分离。Java从来不缺少MVC框架，Apache的Struts、JSF、WebWork和Tapestry都是可选的最流行的MVC框架。

    虽然Spring能够与多种流行的MVC框架进行集成，但它的Web和远程调用模块自带了一个强大的MVC框架，有助于在Web层提升应用的松耦合水平

    除了面向用户的Web应用，该模块还提供了多种构建与其他应用交互的远程调用方案。Spring远程调用功能集成了RMI（Remote Method Invocation）、Hessian、Burlap、JAX-WS，同时Spring还自带了一个远程调用框架：HTTP invoker。Spring还提供了暴露和使用REST API的良好支持。

6. Instrumentation
    Spring的Instrumentation模块提供了为JVM添加代理（agent）的功能。具体来讲，它为Tomcat提供了一个织入代理，能够为Tomcat传递类文件，就像这些文件是被类加载器加载的一样。

7. 测试支持

    通过该模块，你会发现Spring为使用JNDI、Servlet和Portlet编写单元测试提供了一系列的mock对象实现。对于集成测试，该模块为加载Spring应用上下文中的bean集合以及与Spring上下文中的bean进行交互提供了支持。

#### Spring Portfolio

- Spring Boot
- Spring Web Flow
- Spring Web Service
- Spring Security
- Spring Integration
- Spring Batch
- Spring Data
- xxx

### 1.3 Spring各版本新增特性

## 二、 装配Bean

任何一个成功的应用都是由多个为了实现某一个业务目标而相互协作的组件构成的。这些组件必须彼此了解，并且相互协作来完成工作。例如，在一个在线购物系统中，订单管理组件需要和产品管理组件以及信用卡认证组件协作。这些组件或许还需要与数据访问组件协作，从数据库读取数据以及把数据写入数据库。

创建应用对象之间关联关系的传统方法（通过构造器或者查找）通常会导致结构复杂的代码，这些代码很难被复用也很难进行单元测试。如果情况不严重的话，这些对象所做的事情只是超出了它应该做的范围；而最坏的情况则是，这些对象彼此之间高度耦合，难以复用和测试。

在Spring中，对象无需自己查找或创建与其所关联的其他对象。相反，容器负责把需要相互协作的对象引用赋予各个对象。

创建应用对象之间协作关系的行为通常称为装配（wiring），这也是依赖注入（DI）的本质。

### 2.1 Spring配置的可选方案

- 在XML中进行显式配置。
- 在Java中进行显式配置。
- 隐式的bean发现机制和自动装配。

这三种方案可以单独使用，也可以结合使用。建议尽可能地使用自动配置的机制。显式配置越少越好。当你必须要显式配置bean的时候（比如，有些源码不是由你来维护的，而当你需要为这些代码配置bean的时候），我推荐使用类型安全并且比XML更加强大的JavaConfig(类型安全并且易于重构)。最后，只有当你想要使用便利的XML命名空间，并且在JavaConfig中没有同样的实现时，才应该使用XML。

### 2.2 自动化装配bean

Spring从两个角度来实现自动化装配：

- 组件扫描（component scanning）：Spring会自动发现应用上下文中所创建的bean。
- 自动装配（autowiring）：Spring自动满足bean之间的依赖(不用在代码里显示创建，由Spring注入)。

#### 创建可被发现的bean(组件)

步骤：

1. 使用@Component注解声明组件
2. 开启组件扫描(默认未启动)，启动的方式有两种。

    - 需要显式在Spring配置类(@Configuration声明的类)里添加@ComponentScan注解来启动组件扫描。
    - 通过XML启用组件扫描

如果没有其他配置的话，@ComponentScan默认会扫描与配置类相同的包。因此Spring将会扫描这个包以及这个包下的所有子包，查找带有@Component注解的类。如果发现，会在Spring中自动为其创建一个bean。

#### 为组件扫描的bean命名

Spring应用上下文中所有的bean都会给定一个ID。在前面的例子中，尽管我们没有明确地为SgtPeppersbean设置ID，但Spring会根据类名为其指定一个ID。具体来讲，这个bean所给定的ID为sgtPeppers，也就是将类名的第一个字母变为小写。

- @Component("idstr")注解
- @Named("idstr")注解

#### 设置ComponentScan的基础包

按照默认规则，它会以配置类所在的包作为基础包（base package）来扫描组件。但是，如果你想扫描不同的包，那该怎么办呢？或者，如果你想扫描多个基础包，那又该怎么办呢？

有一个原因会促使我们明确地设置基础包，那就是我们想要将配置类放在单独的包中，使其与其他的应用代码区分开来。如果是这样的话，那默认的基础包就不能满足要求了。

- @ComponentScan("package")
- @ComponentScan(basePackage={"package1","package2"...})
- @ComponentScan(basePackage={a.class, b.class}) :指定这些类所在的包为basePackage

tip:基础包是以String类型表示的，但这种方法是类型不安全（not type-safe）的。如果你重构代码的话，那么所指定的基础包可能就会出现错误了。推荐使用类来指定。

尽管在样例中，我为basePackageClasses设置的是组件类，但是你可以考虑在包中创建一个用来进行扫描的空标记接口（marker interface）。通过标记接口的方式，你依然能够保持对重构友好的接口引用，但是可以避免引用任何实际的应用程序代码（在稍后重构中，这些应用代码有可能会从想要扫描的包中移除掉）。

#### 自动装配（Autowired）注解

- @Autowired:Spring提供
- @Inject:Java DI规范

1. 在构造器上添加注解
2. 在修改器(如Setter方法：可以改变成员的值)上添加注解

- 不管是构造器、Setter方法还是其他的方法，Spring都会尝试满足**方法参数**上所声明的依赖。假如有且只有一个bean匹配依赖需求的话，那么这个bean将会被装配进来。
- 如果没有匹配的bean，那么在应用上下文创建的时候，Spring会抛出一个异常。为了避免异常的出现，你可以将@Autowired的required属性设置为false
- 将required属性设置为false时，Spring会尝试执行自动装配，但是如果没有匹配的bean的话，Spring将会让这个bean处于未装配的状态。但是，把required属性设置为false时，你需要谨慎对待。如果在你的代码中没有进行null检查的话，这个处于未装配状态的属性有可能会出现NullPointerException
- 如果有多个bean都能满足依赖关系的话，Spring将会抛出一个异常，表明没有明确指定要选择哪个bean进行自动装配

### 2.3 通过Java代码装配bean

尽管在很多场景下通过组件扫描和自动装配实现Spring的自动化配置是更为推荐的方式，但有时候自动化配置的方案行不通，因此需要明确配置Spring。比如说，你想要将第三方库中的组件装配到你的应用中，在这种情况下，是没有办法在它的类上添加@Component和@Autowired注解的，因此就不能使用自动化装配的方案了。

#### 在Java创建Config配置类:@Configuration

@Configuration注解表明这个类是一个配置类，该类应该包含在Spring应用上下文中如何创建bean的细节。

#### 声明简单的bean:@Bean

要在JavaConfig中声明bean，我们需要编写一个方法，这个方法会创建所需类型的实例，然后给这个方法添加@Bean注解。

```java
@Configuration
public class SampleConfig {

    /*
    @Bean注解会告诉Spring这个方法将会返回一个对象，该对象要注册为Spring应用上下文中的bean。
    默认情况bean的id就是该方法的名称，可以通过注解的name显式指定名称
    */
    @Bean(name="typeName")
    public Type type() {
        return new Type();
    }
}
```

#### 注入bean

```java
@Configuration
public class SampleConfig {

    @Bean
    public TypeA typeA() {
        return new TypeA();
    }

    /*
    方式一：
    将A类的Bean实例注入到生成的B类的bean实例中。
    */
    @Bean
    public TypeB typeB() {
        return new TypeB(typeA()); //如果有多个bean需要注入A类bean实例，Spring将会拦截所有对它的调用，并确保直接返回该方法所创建的bean，而不是每次都对其进行实际的调用。即Spring的默认是单例的(可重用的)，如果如果该bean已经创建过，不再重新创建，直接使用。
    }

    /*
    方式二：理解起来更简单
    当Spring调用typeB()方法来创建TypeB的bean时，Spring会自动装配一个TypeA的bean到方法中，然后执照合适的方式来使用它。
    */
    @Bean
    public TypeB typeB(TypeA a) {
        return new TypeB(a);
    }
}
```

>通过方式二引用其他的bean通常是最佳的选择，因为它不会要求将TypeA声明到同一个配置类之中。在这里甚至没有要求TypeA必须要在JavaConfig中声明，实际上它可以通过组件扫描功能自动发现或者通过XML来进行配置。你可以将配置分散到多个配置类、XML文件以及自动扫描和装配bean之中，只要功能完整健全即可。不管TypeA是采用什么方式创建出来的，Spring都会将其传入到配置方法中，并用来创建TypeA的bean

### 2.4 通过xml配置装备bean

#### 创建xml文件

#### bean声明：\<bean>标签

```xml
<!-- 如果没有明确给定ID，这个bean将会根据全限定类名来进行命名。默认情况下bean的ID将会是“类名#0”。其中，“#0”是一个计数的形式，用来区分相同类型的其他bean（0、1、2...递增）。-->
<bean class="com.zk.Type" id="type" />
```

当Spring发现这个\<bean>元素时，它将会调用class所指定类型的默认构造器来创建bean。

#### 借助构造器注入初始化bean

- \<constructor-arg>元素
- 使用Spring 3.0所引入的c-命名空间

两者的区别在很大程度就是是否冗长烦琐。可以看到，constructor-arg元素比使用c-命名空间会更加冗长，从而导致XML更加难以读懂。另外，有些事情constructor-arg可以做到，但是使用c-命名空间却无法实现。

```xml
<bean class="com.zk.Type" id="type">
    <constructor-arg ref="bean_id" /> //注入构造函数的bean的名称(id)
</bean>

<bean class="com.zk.Type" id="type">
    <c:xx-ref="bean_id" /> //形式一：为构造函数参数名为xx的参数注入bean
    <c:_0-ref="bean_id" /> //形式二：为构造函数第一个参数（索引从0开始）注入bean
</bean>
```

1. 注入字面量：value属性
2. 注入集合：子标签list和set等。可以使用Spring的util命名空间来简化集合注入的配置。

#### 属性注入：property标签

- property标签
- p命名空间

该选择构造器注入还是属性注入呢？作为一个通用的规则，倾向于对强依赖使用构造器注入，而对可选性的依赖使用属性注入。

### 导入混合配置

不管使用JavaConfig还是使用XML进行装配，我通常都会创建一个根配置（root configuration），如果某个配置类或文件变得笨重、繁杂，那么将相关配置独立生成新的配置，再根配置中引入它们。

#### 在JavaConfig中引用XML配置

- @Import注解：导入java配置
- @ImportResource注解：导入xml配置

#### 在xml中引用JavaConfig

- import元素：引入xml配置
- bean元素：引用java配置

## 三、高级装配

### 3.1 环境与profile:Spring profile

在开发软件的时候，有一个很大的挑战就是将应用程序从一个环境迁移到另外一个环境。开发阶段中，某些环境相关做法可能并不适合迁移到生产环境中，甚至即便迁移过去也无法正常工作。数据库配置、加密算法以及与外部系统的集成是跨环境部署时会发生变化的几个典型例子。（即针对每个环境对同一类型的Bean的生成策略不同）

其中一种方式就是在单独的配置类（或XML文件）中配置每个bean，然后在构建阶段（可能会使用Maven的profiles）确定要将哪一个配置编译到可部署的应用中。这种方式的问题在于要为每种环境重新构建应用。当从开发阶段迁移到QA阶段时，重新构建也许算不上什么大问题。但是，从QA阶段迁移到生产阶段时，重新构建可能会引入bug并且会在QA团队的成员中带来不安的情绪。

#### 配置profile bean

Spring为环境相关的bean所提供的解决方案其实与构建时的方案没有太大的差别。当然，在这个过程中需要根据环境决定该创建哪个bean和不创建哪个bean。不过Spring并不是在构建的时候做出这样的决策，而是等到运行时再来确定。这样的结果就是同一个部署单元（可能会是WAR文件）能够适用于所有的环境，没有必要进行重新构建。

1. 在java中配置profile

    - 类注解:@Profile（Spring 3.1增加）
    - 方法注解:@Profile(Spring 3.2增加)

    类注解：在3.1版本中，Spring引入了bean profile的功能。要使用profile，你首先要将所有不同的bean定义整理到一个或多个profile之中，在将应用部署到每个环境时，要确保对应的profile处于激活（active）的状态。

    ```java
    /*@Profile注解应用在了类级别上。它会告诉Spring这个配置类中的bean只有在dev profile激活时才会创建。如果dev profile没有激活的话，那么带有@Bean注解的方法都会被忽略掉。
    */
    // 开发环境配置
    @Configuration
    @Profile("Dev")
    public class DevelopmentProfileConfig {

        @Bean(destroyMethod="shutdown")
        public Bean getBean() {
            return new DevelopmentBean();
        }
    }
    ```

    ```java
    // 生产环境配置
    @Configuration
    @Profile("Prod")
    public class ProductionProfileConfig {

        public Bean getBean() {
            return new ProductionBean();
        }
    }
    ```

    方法注解：

    ```java
    @Configuration
    public class BeanProfileConfig {

        @Bean
        @Profile("Dev")
        public Bean devBean() {
            return new DevelopmentBean();
        }

        @Bean
        @Profile("Prod")
        public Bean prodBean() {
            return new ProductionBean();
        }
    }
    ```

    这里有个问题需要注意，尽管每个bean都被声明在一个profile中，并且只有当规定的profile激活时，相应的bean才会被创建，但是可能会有其他的bean并没有声明在一个给定的profile范围内。没有指定profile的bean始终都会被创建，与激活哪个profile没有关系。

2. 在xml中配置profile:在xml配置文件beans元素中设置属性profile

   所有的配置文件都会放到部署单元之中（如WAR文件），但是只有profile属性与当前激活profile相匹配的配置文件才会被用到。

   你还可以在根beans元素中嵌套定义beans元素（实际效果和单独定义配置是一样的），而不是为每个环境都创建一个profileXML文件。这能够将所有的profile bean定义放到同一个XML文件中

#### 激活profile

Spring在确定哪个profile处于激活状态时，需要依赖两个独立的属性：spring.profiles.active和spring.profiles.default。如果设置了spring.profiles.active属性的话，那么它的值就会用来确定哪个profile是激活的。但如果没有设置spring.profiles.active属性的话，那Spring将会查找spring.profiles.default的值。(没有配置profile的bean总会被创建)

有多种方式来设置这两个属性：

- 作为DispatcherServlet的初始化参数；
- 作为Web应用的上下文参数(在web.xml中设置)；
- 作为JNDI条目；
- 作为环境变量；
- 作为JVM的系统属性；
- 在集成测试类上，使用@ActiveProfiles注解设置

我所喜欢的一种方式是使用DispatcherServlet的参数将spring.profiles.default设置为开发环境的profile，我会在Servlet上下文中进行设置（为了兼顾到ContextLoaderListener）。例如，在Web应用中，设置spring.profiles.default.

按照这种方式设置spring.profiles.default，所有的开发人员都能从版本控制软件中获得应用程序源码，并使用开发环境的设置（如嵌入式数据库）运行代码，而不需要任何额外的配置。

当应用程序部署到QA、生产或其他环境之中时，负责部署的人根据情况使用系统属性、环境变量或JNDI设置spring.profiles.active即可。当设置spring.profiles.active以后，至于spring.profiles.default置成什么值就已经无所谓了；系统会优先使用spring.profiles.active中所设置的profile。