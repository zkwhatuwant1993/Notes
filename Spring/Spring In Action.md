# Spring In Action

Sping是一个模块化框架，目的是简化Java EE应用程序开发(最初是用来替代更加重量级的企业级Java技术，尤其是EJB)。

本书涵盖了Spring框架的许多领域，既有核心框架，也有各种功能扩展，不少的同学曾经对我言及，感觉书中所讲述的内容深度不够，但是我个人认为，对于开源框架的学习，我们会有不同的掌握深度，从最初始的使用、配置，到设计原理，再到源码分析，一本书很难面面俱到深入介绍所有的内容，但是它却能够提供一个方向，让我们按图索骥深入学习更多的知识。

## Spring Core：配置Spring容器和为Spring管理的对象应用切面

## 一. Spring简介

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

<!-- c标签做为子元素 -->
<bean class="com.zk.Type" id="type">
    <c:xx-ref="bean_id" /> //形式一：为构造函数参数名为xx的参数注入bean
    <c:_0-ref="bean_id" /> //形式二：为构造函数第一个参数（索引从0开始）注入bean
</bean>

<!-- c标签做为属性，其中xx为参数名称 -->
<bean class="com.zk.Type" id="type" c:xx="">
</bean>
```

1. 注入字面量：constructor-arg元素的value属性和c标签直接bean元素的属性
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

### 3.2 条件化地配置bean

1. Conditional接口
    @Conditional注解（Spring4引入）：它可以用到带有@Bean注解的方法上。如果给定的条件计算结果为true，就会创建这个bean，否则的话，这个bean会被忽略

    ```java
    @Configration
    public class MyConfig {

        @Bean
        @Conditional(FooCondition.class)
        public Type type() {
            return new Type();
        }
    }
    ```

2. Conditional接口

    Conditional注解接收一个Condition接口的实现。Condition接口定义了一个matchs方法，当此方法返回true时表示这个bean可以被创建。

    ```java
    public interface Condition {
        boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata);
    }
    ```

3. matches方法参数

    ConditionContext接口：

    - 借助getRegistry()返回的BeanDefinitionRegistry检查bean定义；
    - 借助getBeanFactory()返回的ConfigurableListableBeanFactory检查bean是否存在，甚至探查bean的属性；
    - 借助getEnvironment()返回的Environment检查环境变量是否存在以及它的值是什么；
    - 读取并探查getResourceLoader()返回的ResourceLoader所加载的资源；
    - 借助getClassLoader()返回的ClassLoader加载并检查类是否存在。

    AnnotatedTypeMetadata接口：能够让我们检查带有@Bean注解的方法上还有什么其他的注解。

> 非常有意思的是，从Spring 4开始，@Profile注解进行了重构，使其基于@Conditional和Condition实现.@Profile本身也使用了@Conditional注解，并且引用ProfileCondition作为Condition实现,并且在做出决策的过程中，考虑到了ConditionContext和AnnotatedTypeMetadata中的多个因素

### 3.3　处理自动装配的歧义性

当有多个bean满足自动装配所需的bean时，Spring会抛出NoUniqueBeanDefinitionException。

#### 标识首选(primary)bean

- java中配置：@Primary注解，用于@Component标识的类或@Bean标识的方法
- xml: bean元素中的属性primary

#### 使用限定符：@Qualifier

设置首选bean的局限性在于@Primary无法将可选方案的范围限定到唯一一个无歧义性的选项中。它只能标示一个优先的可选方案。当首选bean的数量超过一个时，我们并没有其他的方法进一步缩小可选范围。

与之相反，Spring的限定符能够在所有可选的bean上进行缩小范围的操作，最终能够达到只有一个bean满足所规定的限制条件。

1. @Qualifier注解的基本用法

    - 用于@Component标注的类或者@Bean标识的方法所要创建的bean。标注参数为字符串，表示该bean的限定字符串。**不用@Qualifier标注的bean的默认限定符为该bean的ID**
    - 用于@Autowired和@Inject标注的成员和方法（需要自动装配bean的地方）：限定注入的bean，查找自动装配时所标注的限定符与bean配置时所标注的@Component及所有自定义的限定符完全匹配的bean，并注入。

2. 使用自定义限定符注解

    因为Java不允许在同一个条目上重复出现相同类型的多个注解。当多个bean具有相同的限定符的限定时，不能使用多个@Qualifier注解加上不同的限定符字符串来标注bean。为了进一步区分唯一要装配的bean，需要使用自定义限定符注解。

    >注：Java 8允许出现重复的注解，只要这个注解本身在定义的时候带有@Repeatable注解就可以。不过，Spring的@Qualifier注解并没有在定义时添加@Repeatable注解。

    所需要做的就是创建一个注解，它本身要使用@Qualifier注解来标注。这样我们将不再使用@Qualifier("Feature")，而是使用自定义的@Feature注解。然后我们就能根据需求使用多个不同的自定义限定符注解来标注bean来区分他们。

    自定义限定符注解：

    ```java
    @Target(xxx)
    @Rentention(RententionPolicy.RUNTIME)
    @Qualifier
    public @interface BeanFeature1 {}

     @Target(xxx)
    @Rentention(RententionPolicy.RUNTIME)
    @Qualifier
    public @interface BeanFeature2 {}

     @Target(xxx)
    @Rentention(RententionPolicy.RUNTIME)
    @Qualifier
    public @interface BeanFeature3 {}

    ```

    使用限定符注解：

    ```java
    @Component
    @BeanFeature1
    @BeanFeature2
    public class TypeA implements MyInterface {};

    @Component
    @BeanFeature1
    @BeanFeature3
    public class TypeB implements MyInterface {};
    ```

### 3.4 bean的作用域

- java中配置：@Scope
- xml中配置：scope属性

在默认情况下，Spring应用上下文中所有bean都是作为以单例（singleton）的形式创建的。也就是说，不管给定的一个bean被注入到其他bean多少次，每次所注入的都是同一个实例。在大多数情况下，单例bean是很理想的方案。初始化和垃圾回收对象实例所带来的成本只留给一些小规模任务，在这些任务中，让对象保持无状态并且在应用中反复重用这些对象可能并不合理。

有时候，可能会发现，你所使用的类是易变的（mutable），它们会保持一些状态，因此重用是不安全的。在这种情况下，将class声明为单例的bean就不是什么好主意了，因为对象会被污染，稍后重用的时候会出现意想不到的问题。

Spring定义了多种作用域，可以基于这些作用域创建bean，包括：

- 单例（Singleton）：在整个应用中，只创建bean的一个实例。
- 原型（Prototype）：每次注入或者通过Spring应用上下文获取的时候，都会创建一个新的bean实例。
- 会话（Session）：在Web应用中，为每个会话创建一个bean实例。
- 请求（Rquest）：在Web应用中，为每个请求创建一个bean实例。

#### 使用会话和请示作用域

在Web应用中，如果能够实例化在会话和请求范围内共享的bean，那将是非常有价值的事情。例如，在典型的电子商务应用中，可能会有一个bean代表用户的购物车。如果购物车是单例的话，那么将会导致所有的用户都会向同一个购物车中添加商品。另一方面，如果购物车是原型作用域的，那么在应用中某一个地方往购物车中添加商品，在应用的另外一个地方可能就不可用了，因为在这里注入的是另外一个原型作用域的购物车

就购物车bean来说，会话作用域是最为合适的，因为它与给定的用户关联性最大。

```java
@Component
@Scope(
    value=WebApplicationContext.SOCPE_SESSION,
    proxyMode=ScopedProxyMode.INTERFACES)
public class ShoppingCart {}
```

@Scope有一个proxyMode属性，这个属性解决了将会话或请求作用域的bean注入到单例bean中所遇到的问题.下面是问题场景。

    假设我们要将ShoppingCart bean注入到单例StoreService bean的Setter方法

    因为StoreService是一个单例的bean，会在Spring应用上下文加载的时候创建。当它创建的时候，Spring会试图将ShoppingCart bean注入到 setShoppingCart()方法中。但是ShoppingCart bean是会话作用域的，此时并不存在。直到某个用户进入系统，创建了会话之后，才会出现ShoppingCart实例。

    另外，系统中将会有多个ShoppingCart实例：每个用户一个。我们并不想让Spring注入某个固定的ShoppingCart实例到StoreService中。我们希望的是当StoreService处理购物车功能时，它所使用的ShoppingCart实例恰好是当前会话所对应的那一个。

    Spring并不会将实际的ShoppingCart bean注入到StoreService中，Spring会注入一个到ShoppingCart bean的代理.这个代理会暴露与ShoppingCart相同的方法，所以StoreService会认为它就是一个购物车。但是，当StoreService调用ShoppingCart的方法时，代理会对其进行懒解析并将调用委托给会话作用域内真正的ShoppingCart bean。

现在，我们带着对这个作用域的理解，讨论一下proxyMode属性。如配置所示，proxyMode属性被设置成了ScopedProxyMode.INTERFACES，这表明这个代理要实现ShoppingCart接口，并将调用委托给实现bean。

如果ShoppingCart是接口而不是类的话，这是可以的（也是最为理想的代理模式）。但如果sShoppingCart是一个具体的类的话，Spring就没有办法创建基于接口的代理了。此时，它必须使用CGLib来生成基于类的代理。所以，如果bean类型是具体类的话，我们必须要将proxyMode属性设置为ScopedProxyMode.TARGET_CLASS，以此来表明要以生成目标类扩展的方式创建代理。

请求作用域同理。作用域代理能够延迟注入请求和会话作用域的bean

#### 在XML中声明bean作用域：\<aop:scoped-proxy>

默认情况下，它会使用CGLib创建目标类的代理。但是我们也可以将proxy-target-class属性设置为false，进而要求它生成基于接口的代理

### 3.5 运行时注入值

当讨论依赖注入的时候，我们通常所讨论的是将一个bean引用注入到另一个bean的属性或构造器参数中。它通常来讲指的是将一个对象与另一个对象进行关联。但是bean装配的另外一个方面指的是将一个值注入到bean的属性或者构造器参数中。

有时候硬编码是可以的，但有的时候，我们可能会希望避免硬编码值，而是想让这些值在运行时再确定。

Spring提供了两种在运行时求值的方式：这两种技术的用法是类似的，不过它们的目的和行为是有所差别的

- 属性占位符（Property placeholder）。
- Spring表达式语言（SpEL）。

#### 属性占位符

1. 使用@PropertySource注解和Environment接口来检索属性
2. 解析属性占位符：

    Spring一直支持将属性定义到外部的属性的文件中，并使用占位符值将其插入到Spring bean中。在Spring装配中，占位符的形式为使用“${ ... }”包装的属性名称。

    - xml:直接使用。
    - 自动装配：结合@Value注解

    为了使用占位符，我们必须要配置一个PropertyPlaceholderConfigurer bean或PropertySourcesPlaceholderConfigurer bean。从Spring 3.1开始，推荐使用PropertySourcesPlaceholderConfigurer，因为它能够基于Spring Environment及其属性源来解析占位符。

    如果你想使用XML配置的话，Spring context命名空间中的\<context:propertyplaceholder>元素将会为你生成PropertySourcesPlaceholderConfigurer bean：

解析外部属性能够将值的处理推迟到运行时，但是它的关注点在于根据名称解析来自于Spring Environment和属性源的属性。而Spring表达式语言提供了一种更通用的方式在运行时计算所要注入的值。

#### 使用Spring表达式语言进行装配

Spring 3引入了Spring表达式语言（Spring Expression Language，SpEL），它能够以一种强大和简洁的方式将值装配到bean属性和构造器参数中，在这个过程中所使用的表达式会在运行时计算得到值

SpEL拥有很多特性，包括：

- 使用bean的ID来引用bean；
- 调用方法和访问对象的属性；
- 对值进行算术、关系和逻辑运算；
- 正则表达式匹配；
- 集合操作。

SpEL还能够用在依赖注入以外的其他地方。例如，Spring Security支持使用SpEL表达式定义安全限制规则。另外，如果你在Spring MVC应用中使用Thymeleaf模板作为视图的话，那么这些模板可以使用SpEL表达式引用模型数据。

但需要注意的是，不要让你的表达式太智能。你的表达式越智能，对它的测试就越重要。SpEL毕竟只是String类型的值，可能测试起来很困难。鉴于这一点，我建议尽可能让表达式保持简洁，这样测试不会是什么大问题。

## 四、面向切面

- 面向切面编程的基本原理
- 通过POJO创建切面
- 使用@AspectJ注解
- 为AspectJ切面注入依赖

在软件开发中，散布于应用中多处的功能被称为横切关注点（cross-cutting concern）。通常来讲，这些横切关注点从概念上是与应用的业务逻辑相分离的（但是往往会直接嵌入到应用的业务逻辑之中）。把这些横切关注点与业务逻辑相分离正是面向切面编程（AOP）所要解决的问题。

DI有助于应用对象之间的解耦，而AOP可以实现横切关注点与它们所影响的对象之间的解耦。

### 什么是面向切面编程

切面提供了取代继承和委托的另一种可选方案，而且在很多场景下更清晰简洁。在使用面向切面编程时，我们仍然在一个地方定义通用功能，但是可以通过声明的方式定义这个功能要以何种方式在何处应用，而无需修改受影响的类。横切关注点可以被模块化为特殊的类，这些类被称为切面（aspect）。

这样做有两个好处：首先，现在每个关注点都集中于一个地方，而不是分散到多处代码中；其次，服务模块更简洁，因为它们只包含主要关注点（或核心功能）的代码，而次要关注点的代码被转移到切面中了。

#### AOP术语

1. 通知(advice)

    通知定义了切面的功能以及何时使用。

    Spring切面可以应用5种类型的通知：

    - 前置通知（Before）：在目标方法被调用之前调用通知功能；
    - 后置通知（After）：在目标方法完成之后调用通知，此时不会关心方法的输出是什么；
    - 返回通知（After-returning）：在目标方法成功执行之后调用通知；
    - 异常通知（After-throwing）：在目标方法抛出异常后调用通知；
    - 环绕通知（Around）：通知包裹了被通知的方法，在被通知的方法调用之前和调用之后执行
    - 自定义的行为。

2. 连接点(join point)

    我们的应用可能也有数以千计的时机应用通知。这些时机被称为连接点。连接点是在应用执行过程中能够插入切面的一个点。这个点可以是调用方法时、抛出异常时、甚至修改一个字段时。切面代码可以利用这些点插入到应用的正常流程之中，并添加新的行为。

3. 切点（Poincut）：特定的连接点的组合

    一个切面并不需要通知应用的所有连接点。切点有助于缩小切面所通知的连接点的范围。

    如果说通知定义了切面的“什么”和“何时”的话，那么切点就定义了“何处”。切点的定义会匹配通知所要织入的一个或多个连接点。我们通常使用明确的类和方法名称，或是利用正则表达式定义所匹配的类和方法名称来指定这些切点。有些AOP框架允许我们创建动态的切点，可以根据运行时的决策（比如方法的参数值）来决定是否应用通知。

4. 切面（Aspect）

    切面是通知和切点的结合。通知和切点共同定义了切面的全部内容——它是什么，在何时和何处完成其功能。

5. 引入（Introduction）

    引入允许我们向现有的类添加新方法或属性。例如，我们可以创建一个Auditable通知类，该类记录了对象最后一次修改时的状态。这很简单，只需一个方法，setLastModified(Date)，和一个实例变量来保存这个状态。然后，这个新方法和实例变量就可以被引入到现有的类中，从而可以在无需修改这些现有的类的情况下，让它们具有新的行为和状态。

6. 织入（Weaving）

    织入是把切面应用到目标对象并创建新的代理对象的过程。切面在指定的连接点被织入到目标对象中,在目标对象的生命周期里有多个点可以进行织入：

    - 编译期：切面在目标类编译时被织入。这种方式需要特殊的编译器。AspectJ的织入编译器就是以这种方式织入切面的。
    - 类加载期：切面在目标类加载到JVM时被织入。这种方式需要特殊的类加载器（ClassLoader），它可以在目标类被引入应用之前增强该目标类的字节码。AspectJ 5的加载时织入（load-time weaving，LTW）就支持以这种方式织入切面。
    - 运行期：切面在应用运行的某个时刻被织入。一般情况下，在织入切面时，AOP容器会为目标对象动态地创建一个代理对象。Spring AOP就是以这种方式织入切面的。

#### Spring对AOP的支持

并不是所有的AOP框架都是相同的，它们在连接点模型上可能有强弱之分。有些允许在字段修饰符级别应用通知，而另一些只支持与方法调用相关的连接点。它们织入切面的方式和时机也有所不同。但是无论如何，创建切点来定义切面所织入的连接点是AOP框架的基本功能。

Spring提供了4种类型的AOP支持：

- 基于代理的经典(旧)Spring AOP；
- 纯POJO切面:使用xml配置和aop命名空间
- @AspectJ注解驱动的切面:使用注解
- 注入式AspectJ切面（适用于Spring各版本）：需要拦截构造器或属性时

前三种都是Spring AOP实现的变体，**Spring AOP构建在动态代理基础之上**，因此，Spring对AOP的支持局限于方法拦截。

1. Spring通知是Java编写的

    Spring所创建的通知都是用标准的Java类编写的。这样的话，我们就可以使用与普通Java开发一样的集成开发环境（IDE）来开发切面。而且，定义通知所应用的切点通常会使用注解或在Spring配置文件里采用XML来编写，这两种语法对于Java开发者来说都是相当熟悉的。AspectJ与之相反。虽然AspectJ现在支持基于注解的切面，但AspectJ最初是以Java语言扩展的方式实现的。这种方式有优点也有缺点。通过特有的AOP语言，我们可以获得更强大和细粒度的控制，以及更丰富的AOP工具集，但是我们需要额外学习新的工具和语法。

2. Spring在运行时通知对象：

    通过在代理类中包裹切面，Spring在运行期把切面（切面由Spring管理，所以需要定义为bean）织入到Spring管理的bean中。代理类封装了目标类(核心业务类)，并拦截被通知方法（业务方法）的调用，再把调用转发给真正的目标bean。当代理拦截方法调用时，当代理拦截到方法调用时，在调用目标bean方法之前，会执行切面逻辑。

    直到应用需要被代理的bean时，Spring才创建代理对象。例如使用的ApplicationContext的话，在ApplicationContext从BeanFactory中加载所有bean的时候，Spring才会创建被代理的对象。因为Spring运行时才创建代理对象，所以我们不需要特殊的编译器来织入Spring AOP的切面。

### Spring AOP:通过切点来选择连接点:切点表达式

在Spring AOP中，要使用AspectJ的切点表达式语言来定义切点。关于Spring AOP的AspectJ切点，最重要的一点就是Spring仅支持AspectJ切点指示器（pointcut designator）的一个子集。让我们回顾下，Spring是基于代理的，而某些切点表达式是与基于代理
的AOP无关的(也就是Spring不支持的)。

### Spring AOP:使用注解创建切面:@Aspect

1. AspectJ提供了五个注解来定义通知：他们的参数都是**切点表达式**

    - @After 通知方法会在目标方法返回或抛出异常后调用
    - @AfterReturning 通知方法会在目标方法返回后调用
    - @AfterThrowing 通知方法会在目标方法抛出异常后调用
    - @Around 通知方法会将目标方法封装起来
    - @Before 通知方法会在目标方法调用之前执行

    ```java
    // 定义业务类:如Performance
    package com.zk;
    public interface Perfomance {
        public void perform();
    }
    ```

2. 通过@Pointcut注解声明频繁使用的切点表达式

需要注意的是，除了注解和没有实际操作的performance()方法，Audience类依然是一个POJO。我们能够像使用其他的Java类那样调用它的方法，它的方法也能够独立地进行单元测试，这与其他的Java类并没有什么区别。

#### 环绕通知

前置通知和后置通知有一些限制。具体来说，如果不使用成员变量存储信息的话，在前置通知和后置通知之间共享信息非常麻烦。

假设备我们需要知道某个业务逻辑执行需要多长时间，。使用前置通知和后置通知实现该功能的唯一方式是在前置通知中记录开始时间并在某个后置通知中报告表演耗费的时间。但这样的话我们必须在一个成员变量中保存开始时间。因为Audience是单例的，如果像这样保存状态的话，将会存在线程安全问题。

#### advice中的参数：限制连接点的匹配(切入点)和访问被通知方法中的参数

通过切点表达式声明。

#### 注解引入新功能

为被通知的对象引入全新的功能，不仅仅是原有的业务功能(方法)。实际上，利用被称为引入的AOP概念，切面可以为Spring bean添加新方法。**代理拦截调用并委托给实现该方法的其他对象**。

如果除了实现这些接口，代理也能暴露新接口的话，会怎么样呢？那样的话，切面所通知的bean看起来像是实现了新的接口，即便底层实现类并没有实现这些接口也无所谓。

@DeclareParent:声明了此切面所通知的bean要在它的对象层次结构中拥有新的父类型（就是我们引入新功能所属的接口）。

```java
// 定义新功能接口
public interface MyInterface {
    void doSomething();

// 提供实现
public class DefaultImpl implements MyInterface {

    public void doSomthing() {
        // do some thing
    }
}

//定义切面
@AspectJ
@Component
public class MyInterfaceIntroducer {

    @DeclareParent(value = "com.zk.aspect.Performance+",
    defaultImpl = DefaultImpl.class)
    public static MyInterface myInterface;
}
```

@DeclareParents注解由三部分组成：

- value属性指定了哪种类型的bean要引入该接口。在本例中，也就是所有实现Performance的类型。（标记符后面的加号表示是Performance的所有子类型，而不是Performance本身。）
- defaultImpl属性指定了为引入功能提供实现的类。在这里，我们指定的是DefaultEncoreable提供实现。
- @DeclareParents注解所标注的静态属性指明了要引入了接口。在这里，我们所引入的是Encoreable接口。

Spring的自动代理机制将会获取到它的声明，当Spring发现一个bean使用了@Aspect注解时，Spring就会创建一个代理，然后将调用委托给被代理的bean或被引入的实现，这取决于调用的方法属于被代理的bean还是属于被引入的接口。

调用流程：bean自动注入(实际上是拥有bean的所有接口的代理对象) -> 将bean(代理对象)强转为新功能接口类型(spring创建的代理对象也实现了该接口) -> 调用新功能 -> 代理对象拦截调用并转到内部的bean对象或者接口的实现的引入。

在Spring中，注解和自动代理提供了一种很便利的方式来创建切面。它非常简单，并且只涉及到最少的Spring配置。**但是，面向注解的切面声明有一个明显的劣势：你必须能够为通知类添加注解。为了做到这一点，必须要有源码**。

### 在xml中声明切面：Spring的aop命名空间

使用原则：基于注解的配置要优于基于Java的配置，基于Java的配置要优于基于XML的配置。但是，如果你需要声明切面，但是又不能为通知类添加注解的时候，那么就必须转向XML配置了。

关于Spring AOP配置元素，第一个需要注意的事项是大多数的AOP配置元素必须在\<aop:config>元素的上下文内使用。这条规则有几种例外场景，但是把bean声明为一个切面时，我们总是从\<aop:config>元素开始配置的。

\<aop:pointcut>元素所定义的切点可以被同一个\<aop:aspect>元素之内的所有通知元素引用。如果想让定义的切点能够在多个切面使用，我们可以把\<aop:pointcut>元素放在\<aop:config>元素的范围内。

### 注入到AspectJ切面

虽然Spring AOP能够满足许多应用的切面需求，但是与AspectJ相比，Spring AOP 是一个功能比较弱的AOP解决方案。AspectJ提供了Spring AOP所不能支持的许多类型的切点。

例如，当我们需要在创建对象时应用通知，构造器切点就非常方便。不像某些其他面向对象语言中的构造器，Java构造器不同于其他的正常方法。这使得Spring基于代理的AOP无法把通知应用于对象的创建过程。

对于大部分功能来讲，AspectJ切面与Spring是相互独立的。虽然它们可以织入到任意的Java应用中，这也包括了Spring应用，但是在应用AspectJ切面时几乎不会涉及到Spring。

但是精心设计且有意义的切面很可能依赖其他类来完成它们的工作。如果在执行通知时，切面依赖于一个或多个类，我们可以在切面内部实例化这些协作的对象。但更好的方式是，我们可以借助Spring的依赖注入把bean装配进AspectJ切面中。

>需要注意的是，AspectJ切面根本不需要Spring就可以织入到我们的应用中。当需要使用Spring提供的自动注入功能时，必须将该AspectJ切面声明为Spring bean.

```xml
<!-- 将AspectJ切面声明为一个spring bean -->
<bean class = "com.zk.MyAspect"
    factory-method="aspectOf">
</bean>
```

很大程度上，\<bean>的声明与我们在Spring中所看到的其他\<bean>配置并没有太多的区别，但是最大的不同在于使用了factory-method属性。通常情况下，Spring bean由Spring容器初始化，但是AspectJ切面是由AspectJ在运行期创建的。等到Spring要为MyAspect注入属性时，MyAspect已经被实例化了。

因为Spring不能负责创建MyAspect，那就不能在 Spring中简单地把MyAspect声明为一个bean。相反，我们需要一种方式为Spring获得已经由AspectJ创建的MyAspect实例的句柄，从而可以注入。幸好，所有的AspectJ切面都提供了一个静态的aspectOf()方法，该方法返回切面的一个单例。所以为了获得切面的实例，我们必须使用factory-method来调用asepctOf()方法而不是调用MyAspect的构造器方法。
