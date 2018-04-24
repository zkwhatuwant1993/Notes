# Java Web高级编程学习笔记：阅读API和JSR等Java EE文档

- [Java Web高级编程学习笔记：阅读API和JSR等Java EE文档](#java-webapijsrjava-ee)
    - [一、Java EE相关概念](#java-ee)
        - [1. JavaEE平台规范：Servlet,过滤器，jsp,JUEL等等组件的标准。](#1-javaeeservlet-jsp-juel)
        - [2. web容器/servlet容器](#2-web-servlet)
    - [二、Servlet类](#servlet)
        - [1. 创建Servlet类](#1-servlet)
            - [1.1 Servlet类的体系结构。](#11-servlet)
            - [1.2 处理HTTP请求](#12-http)
            - [1.3 初始化和销毁:Servlet的生命周期](#13--servlet)
        - [2. 配置可部署的Servlet：web.xml](#2-servletwebxml)
            - [2.1 配置Servlet:Servlet标签](#21-servlet-servlet)
            - [2.2 将Servlet映射到URL:Servlet-mapping标签](#22-servleturl-servlet-mapping)
        - [3. 了解doGet，doPost和其他方法](#3-dogetdopost)
            - [3.1. service方法](#31-service)
            - [3.2 HttpServletRequest接口](#32-httpservletrequest)
                - [3.2.1 获取请求参数](#321)
                - [3.2.2 确定与请求内容（请求正文）相关信息:getContentXXX()方法](#322--getcontentxxx)
                - [3.2.3 获取请求正文:使用getInputStream或getReader。](#323--getinputstreamgetreader)
                - [3.2.4 获取Http请求特有的数据URL,URI,和头信息](#324-httpurl-uri)
                - [3.2.5 会话和Cookies](#325-cookies)
            - [3.3 使用HttpServletResonse](#33-httpservletresonse)
                - [3.3.1 编写响应正文](#331)
                - [3.3.2 设置头和其他response属性](#332-response)
        - [4.使用初始化参数配置应用程序](#4)
            - [4.1 使用Context初始化参数](#41-context)
            - [4.2 使用Servlet初始化参数](#42-servlet)
        - [5. 通过表单上传文件:Servlet的multipart-config及Http-response的header设置(attachment)](#5--servletmultipart-confighttp-responseheaderattachment)
        - [6. 编写多线程安全的应用程序](#6)
            - [6.1 理解请求、线程、方法执行](#61)
            - [6.2 保护共享资源：多线程的典型问题，即资源竞争（处理不好会导致死锁）。](#62)
    - [三. JSP的基本规则：JAVA模板引擎(用于代替手动拼接字符串，但其本质还是做页面字符串的拼接)。](#jspjava)
        - [1.JSP的运行原理(本质是一个Servlet)](#1jspservlet)
        - [2. 指令、声明、脚本和表达式](#2)
        - [3. 注释代码](#3)
        - [4. 在JSP中导入JAVA类:导入指令](#4-jspjava)
        - [5. 常用指令](#5)
            - [5.1 修改页面属性](#51)
            - [5.2 包含其他JSP页面](#52-jsp)
            - [5.3 包含标签库](#53)
            - [5.4 jsp标签](#54-jsp)
        - [6.在JSP中使用JAVA(以及不鼓励使用JAVA的原因)](#6jspjavajava)
            - [6.1 JSP中的内置(隐式)变量](#61-jsp)
            - [6.2. JSP中不要滥用JAVA代码，应该只做页面展示相关的事。](#62-jspjava)
        - [7. 结合使用Servlet和JSP：业务逻辑和表示展分享。](#7-servletjsp)
            - [7.1 JSP属性的复用：在配置文件web.xml中设置JSP属性，使用jsp-config标签](#71-jspwebxmljspjsp-config)
                - [7.1.1 匹配不同的JSP属性：jsp属性组jsp-property-group](#711-jspjspjsp-property-group)
                - [7.1.2 jsp属性](#712-jsp)
            - [7.2 将Servlet中的**请求转发**给JSP](#72-servletjsp)
                - [7.2.1 **请求转发与重定向的区别**](#721)
            - [7.3 关于JSP文档(JSPX)：使用xml文档来实现JSP](#73-jspjspxxmljsp)
    - [四、会话(Session):维持状态](#session)
        - [4.1 使用会话的原因](#41)
            - [4.1.1 维持状态](#411)
            - [4.1.2 记住用户](#412)
            - [4.1.3 应用程序工作流](#413)
        - [4.2 使用cookie和URL参数和服务器传递Session ID](#42-cookieurlsession-id)
            - [4.2.1 Cookie技术](#421-cookie)
            - [4.2.2 URL中的Session ID](#422-urlsession-id)
            - [4.2.3 Session中的漏洞](#423-session)
        - [4.3 在Session中存储数据](#43-session)
            - [4.3.1 在web.xml中配置Session](#431-webxmlsession)
            - [4.3.2 存储和获取数据](#432)
            - [4.3.3 删除数据](#433)
            - [4.3.4 相关方法](#434)
        - [4.4 会话事件与监听器](#44)
            - [4.4.1 注册监听器](#441)
            - [4.4.2 维护活跃会话列表：使用JAVA容器维护会话](#442-java)
        - [4.5 将使用Sesssion的应用程序集群化](#45-sesssion)
            - [4.5.1 在集群中使用Session ID](#451-session-id)
            - [4.5.2 了解会话复制和故障恢复](#452)
    - [五、JSP-EL](#jsp-el)
        - [5.1 EL表达式基本语法](#51-el)
            - [5.1.1 立即执行](#511)
            - [5.1.2 延迟执行](#512)
            - [5.1.3 使用EL表达式](#513-el)
        - [5.2  EL语法](#52-el)
            - [5.2.1 保留字](#521)
            - [5.2.2 操作符优先级](#522)
            - [5.2.3 常量（字面量）](#523)
            - [5.2.4 操作对象的属性和方法](#524)
            - [5.2.5 EL函数](#525-el)
            - [5.2.6 静态字段和方法访问](#526)
            - [5.2.7 枚举](#527)
            - [5.2.8 lambda表达式：匿名函数](#528-lambda)
            - [5.2.9 在EL中访问集合：获取集合中的元素](#529-el)
        - [5.3 在EL中使用域变量](#53-el)
            - [5.3.1 在EL中使用隐式域(scope)](#531-elscope)
            - [5.3.2 使用隐式的EL变量(内置变量)](#532-el)
        - [5.4 使用流API访问集合：集合流API](#54-apiapi)
            - [5.4.1 了解中间操作](#541)
            - [5.4.2 使用终结操作](#542)
    - [六、使用JSTL（Java标准标签库）](#jstljava)
        - [6.1 JSP标签和JSTL](#61-jspjstl)
        - [6.2 使用core标签库](#62-core)
            - [6.2.1 <c:out>](#621-c-out)
            - [6.2.2 <c:url>](#622-c-url)
            - [6.2.3 <c:if>](#623-c-if)
            - [6.2.4 <c:choose>](#624-c-choose)
            - [6.2.5 <c:forEach>](#625-c-foreach)
            - [6.2.6 <c:forTokens>](#626-c-fortokens)
            - [6.2.7 <c:redirect>](#627-c-redirect)
            - [6.2.8 <c:import>获取特定URL资源的内容。](#628-c-importurl)
            - [6.2.9 <c:set>和<c:remove>](#629-c-setc-remove)
        - [6.3 使用国际化(i18n)和格式化标签库(FMT命令空间)](#63-i18nfmt)
            - [6.3.1 国际化和本地化组件](#631)
            - [6.3.2 <fmt:message>](#632-fmt-message)
            - [7.3.3 <fmt:setLocale>：java.util.Locale](#733-fmt-setlocalejavautillocale)
            - [7.3.4 <fmt:bundle>和<fmt:setBundel>:java.util.ResourceBundle](#734-fmt-bundlefmt-setbundel-javautilresourcebundle)
            - [6.3.5 <fmt:timeZone>和<fmt:setTimeZone>](#635-fmt-timezonefmt-settimezone)
            - [6.3.6 <fmt:formatDate>和<fmt:parseDate>](#636-fmt-formatdatefmt-parsedate)
            - [6.3.7 <fmt:formartNumber>和<fmt:parseNumber>](#637-fmt-formartnumberfmt-parsenumber)
    - [七、 自定义标签和函数库](#)
        - [7.1 了解TLD、标签文件和标签处理器](#71-tld)
        - [7.1.1 读取Java标签库TLD(c.tld)](#711-javatldctld)
            - [7.1.2 标签文件指令](#712)
        - [7.2 将标签文件用作HTML模板](#72-html)
        - [7.3 标签处理器](#73)
    - [八、 过滤器](#)
        - [8.1 使用过滤器的目的](#81)
        - [8.2 创建、配置和映射过滤器：类似Servlet](#82-servlet)
            - [8.2.1 过滤器链](#821)
            - [8.2.2 映射到URL-Pattern和Servlet名称](#822-url-patternservlet)
            - [8.2.3 映射到不同的请求派发器类型](#823)
            - [8.2.4 在部署描述符中配置Filter](#824-filter)
            - [8.2.4 使用注解配置：@WebFilter](#824-webfilter)
            - [8.2.4 编程方式配置](#824)
        - [8.3 Filter生命周期](#83-filter)
        - [8.4 过滤器排序](#84)
            - [8.4.1 使用过滤器处理异步请求:AsyncContext](#841--asynccontext)

勘误表：http:www.wrox.com/go/projavaforwebapps

## 一、Java EE相关概念

### 1. JavaEE平台规范：Servlet,过滤器，jsp,JUEL等等组件的标准。

### 2. web容器/servlet容器

- tomcat（只实现了一部分标准）
- GlassFish(基于tomcat，完整的实现了JavaEE应用规范的服务器，包含web容器)
- JBoss,WildFly
- Jetty

## 二、Servlet类

功能：用于接收和响应来自web客户端的请求，使用http协议进行通信。
描述：Servlet是所有Web应用程序的核心类，它是唯一的既可以直接处理和响应用户请求，也可以将处理工作委托给应用程序中的其他类。除非某个过滤器提前拦截了某个客户端的请求，否则所有的请求都将发送到某些Servlet。

### 1. 创建Servlet类

#### 1.1 Servlet类的体系结构。

1. Servlet接口:定义了初始化,销毁Servlet和请求的方法。
2. GnericServlet implements Servlet：抽象类，一个不依赖协议的Servlet,定义了一个service方法，用于接收和响应客户端请求。还包含一些辅助方法：日志操作，从应用中获取Servlet的配置信息等。
3. 4.HttpServlet extends GnericServlet：实现了接收http请求的service方法.并且提供了响应每种Http方法类型的空实现。GET,HEAD,POST,PUT,DELETE,OPTIONS,TRACE

#### 1.2 处理HTTP请求

doGet,doPost方法：Web容器将会处理请求的解释，并从socket中读取请求头和参数。在Servlet的方法返回之后，Web容器还将格式化响应头和主体，并写回到socket中。
参数HttpServletRequest和HttpServletResponse

#### 1.3 初始化和销毁:Servlet的生命周期

init()方法：在Servlet启动时调用(在Servlet构造完成后，且在响应一第一请求前调用;如果将该Servlet配置为web应用程序部署和启动时自动启动，那么此方法也会调用).调用init方法时，Servlet中的所有属性都有设置完成，并提供对ServletConfig和ServletContext的访问。
destory()方法:在Servlet不再接收请求后立即调用（通常发生在web应用程序被停止或者卸载，或者web容器关闭时）

### 2. 配置可部署的Servlet：web.xml

Servlet部署描述文件:WEB-INFO/web.xml

#### 2.1 配置Servlet:Servlet标签

- web-app标签中的version属性:Servlet api的版本
- display-name标签：应用程序在应用服务器中显示的名称。
- Servlet标签：告诉web容器如何创建该Servlet

```xml
<!-- 告诉web容器如何创建该Servlet-->
<Serlvet>
    <!--指定Servlet的名字,可以通过getServletName()方法获取-->
    <Servlet-name>name</Servlet-name>
    <!-- 指定Servlet对应的java类-->
    <Servlet-class>class全名</Servlet-class>
    <!-- 在应用程序启动之后立即启动该Servlet。标签中的数值表示如果有其他Servlet配置了该项，数值小的先启动；如果数值相同，那么按照web.xml中的出现顺序启动-->
    <load-on-startup>1</load-on-startup>
</Servlet>
```

#### 2.2 将Servlet映射到URL:Servlet-mapping标签

1. 使用web.xml设置
    ```xml
    <!-- 告诉web容器如何创建该Servlet-->
    <servlet-mapping>
    <!--指定Servlet的名字，与<Servlet>标签下的<Servlet-name>标签对应-->
    <!-- 表示映射的是哪个Servlet -->
    <servlet-name>name</Servlet-name>
    <!-- 访问该web应用的相对URL/path的请求将由该Servlet处理-->
    <url-pattern>/path1</url-pattern>
    <!-- 可以将多个url映射到同一个Servlet-->
    <url-pattern>/path2</url-pattern>
    <url-pattern>/path3</url-pattern>
    </servlet-mapping>
    ```
2. 使用注解
    ```java
    @WebServlet(
        name = "servletName",
        urlPatterns = {"/url-pattern1","/url-pattern2"...}
    )
    class MyServlet extends HttpServlet{}
    ```

### 3. 了解doGet，doPost和其他方法

#### 3.1. service方法

Servlet类的service方法将会处理所有到达的请求,然后根据所使用的协议(如HttServlet使用的http协议)解析并处理（调用doGet，doPost或其他方法）请求中的数据,然后返回客户端可接受的响应(符合协议).

#### 3.2 HttpServletRequest接口

Extends the ServletRequest interface to provide request information for HTTP servlets.
扩展自ServletRequest接口来提供收到请求的额外的与HTTP协议相关的信息。它定义了多个可以获得HTTP请求详细信息的相关方法.它也允许设置**请求特性**。

The servlet container creates an HttpServletRequest object and passes it as an argument to the servlet's service methods (doGet, doPost, etc).
Servlet容器创建一个HttpServletRequest的实例并将该对象做为参数传给该servlet的service方法。

##### 3.2.1 获取请求参数

1. 请求参数的两种形式
    - 查询参数(URL参数):application/x-www-form-urlencoded或multipart/form-data编码的请求正文。所有的请求方法都支持查询参数.它将被添加到Http请求的第一行数据中(请求头)。
    - post参数:保存在请求正文中。

    注意：从技术上讲,HTTP协议的RFC规范并不禁止在任何HTTP方法中使用查询参数。不过许多web服务器都将忽略通过DELETE,TRACE和OPTIONS传入的查询参数，不建议在这些请求中使用查询参数。

2. 相关方法
    - getParameter
    - getParameterMap
    - getParameterNames
    - getParameterValues

    注意：第一次调用request对象的这些方法时,Web容器将判断该请求是否包含了post变量,如果包含了,它将读取reqeust的InputStream并解析这些Post变量。该InputStream只能读取一次,所以调用了一个请求的InputStream之后，再次获取请求参数，会抛出IllegalStateException;同理，如果获取了请求参数，再调用InputStream也会抛出该异常。所以任何时候获取post参数都最好使用参数方法去获取，不要用getInputStream或getInputReader去获取。

##### 3.2.2 确定与请求内容（请求正文）相关信息:getContentXXX()方法

##### 3.2.3 获取请求正文:使用getInputStream或getReader。

    注意：不要在同一个reqeust对象上同时使用这两个方法，会抛出抛出IllegalStateException.因为该流只能读取一次。

##### 3.2.4 获取Http请求特有的数据URL,URI,和头信息

- getRequestURL
- getRequestURI
- getServletPath
- getHeaderXXX

##### 3.2.5 会话和Cookies

- getSession
- getCookies

#### 3.3 使用HttpServletResonse

使用该对象可以完成设置响应头、响应正文、重写向请求、响应状态码以及将cookies返回到客户端等任务。

##### 3.3.1 编写响应正文

1. 使用getOutPutStream或getWriter
2. 设置内容类型和编码格式:setContentTypep和setCharacterEncoding.

注意：如何要设置内容类型和编码格式，必须在getOutputStrem或getWriter之前设置，否则将使用web容器的默认编码返回输出流.

##### 3.3.2 设置头和其他response属性

- setHeaderXXX()
- setStatus
- sendError
- sendRedirect

### 4.使用初始化参数配置应用程序

#### 4.1 使用Context初始化参数

1. 在web.xml中配置Context参数

    ```xml
    <context-param>
        <param-name></param-name>
        <param-value></param-value>
    </context-param>
    ```

    应用程序中的所有Servlet都共享这些数据。

2. 在Servlet中获取

    ```java
    ServletContext context = this.getServletContext();
    context.getInitParameter();
    ```

#### 4.2 使用Servlet初始化参数

1. 在web.xml中配置Servlet初始化参数
    ```xml
    <servlet>
        <servlet-name></servlet-name>
        <servlet-class></servlet-class>
    </servlet>
    <init-param>
            <param-name>p1</param-name>
            <param-value>v1</param-value>
        </init-param>
    <init-param>
        <param-name>p2</param-name>
        <param-value>v2</param-value>
    </init-param>
    ```
2. 在Servlet中获取
    ```java
    ServletConfig config = this.getServletConfig();
    config.getInitParameter();
    ```
3. 使用注解
     ```java
    @WebServlet(
        name = "servletName",
        urlPatterns = {"/url-pattern1","/url-pattern2"...},
        initParams = {
        @WebInitParam(name = "name1",value = "value1"),
        @WebInitParam(name = "name2",value = "value2")
        }
    )
    class MyServlet extends HttpServlet{}
    ```
4. 使用xml配置和使用注解配置的区别
   - 使用注解:参数如果需要修改，那么修改后需要重新编译应用程序才能生效.
   - 使用xml:参数修改后，重启应用程序即可生效。

### 5. 通过表单上传文件:Servlet的multipart-config及Http-response的header设置(attachment)

1. 在web.xml中配置Servlet
    ```xml
    <servlet>
        <servlet-name></servlet-name>
        <servlet-class></servlet-class>
        <multipart-config>
            <location></location>
            <file-size-threshold></file-size-threshold>
            <max-file-size></max-file-size>
            <max-request-size></max-request-size>
        </multipart-config>
    </servlet>
    ```

2. 使用注解
    ```java
    @WebServlet(
        name = "servletName",
        urlPatterns = {"/url-pattern1","/url-pattern2"...},
        initParams = {
        @WebInitParam(name = "name1",value = "value1"),
        @WebInitParam(name = "name2",value = "value2")
        }
    )
    @MultipartConfig(
        fileSizeThreshold = 5_242_880, //5MB
        maxFileSize = 20_971_520L, //20MB
        maxRequestSize = 41_943_040L //40MB
    )
    class MyServlet extends HttpServlet{}
    ```

### 6. 编写多线程安全的应用程序

#### 6.1 理解请求、线程、方法执行

**为什么需要线程池**：创建和销毁线程会产生许多开销，这会降低application的运行速度，所以采用可利用的线程组成的线程池可以减少这种开销，提高性能。但是在也要特别注意多线程下的安全问题。

请求队列：当容器收到请求，它将在线程池中寻找可以用线程。如果找不到，并且线程池已经达到了最大线程数，那么该请求就会被放入一个队列(先进先出)中，等待获取可用的线程来处理该请求。一旦一个线程被用来处理某个请求，那么它对其他请求来说是不可用的（贯穿整个请求的生命周期），只有请求被处理，response已经发送到客户端后，该线程才会变成可用状态并返回到线程池中，用于处理下一个请求。

tips:有也**异步**的处理方式，此时线程池不与Servlet的生命周期绑定。

#### 6.2 保护共享资源：多线程的典型问题，即资源竞争（处理不好会导致死锁）。

1. 一个Servlet中的静态变量和成员变量都能同时被多个线程访问，所以多线程环境下需要做处理，如使用volitle关键字(保证编译器不做优化，每次读取都是最新值)，将访问共享资源的代码放在同步块中。
2. 所以永远不要在Servlet中使用静态变量和成员变量来存储request和response对象，因为任何属于request和response对象的资源都应该只用作本地变量和参数。

## 三. JSP的基本规则：JAVA模板引擎(用于代替手动拼接字符串，但其本质还是做页面字符串的拼接)。

- JAVA模板引擎出现的原因：手动拼接页面字符串随着页面的复杂程度难以阅读和维护。用于代替手动拼接字符串，但其本质还是做页面字符串的拼接
- JAVA模板引擎：用来渲染及展示web页面。常见的有JSP,Velocity, Freemaker,Thymeleaf.
- JSP可以使用：HTML标签,内置的JSP标签,自定义JSP标签,EL。

### 1.JSP的运行原理(本质是一个Servlet)

JSP是一个精心设计的Servlet，在运行时JSP代码将由JSP编译器转换进行转换，它将解析出JSP代码的所有特征并生成对应的JAVA代码，由JSP转换得到的JAVA类都继承了Servlet类，有其生命周期。

### 2. 指令、声明、脚本和表达式

```xml
<%@ 指令内容 %>
<%! 声明内容 %>
<% 脚本内容 %>
<%= 表达式 %>
```

1. 使用指令

    指令用于指示JSP解释器执行某个操作(例如设置内容类型)或者对文件作出假设（例如声明脚本语言的类型）、导入类、在转换时包含的其他JSP或者包含JSP标签库

2. 使用声明

    声明用于在JSPServlet类的范围内**声明一些东西**（即定义**成员**变量，方法或声明标签中的类），这些声明都将在JSP转换为Servlet类时添加到内的主体中（即作用域是整个类），所以声明中定义的类实际 上是Servlet的内部类。

3. 使用脚本

    和声明一样，脚本中也包含了JAVA代码，这些代码会在JSP转换时添加到_jspService方法体中（即作用域为局部）。该方法中所有的局部变量都可以在脚本中使用，任何在该方法中合法的代码在脚本中也是合法的。另外还可以使用条件语句、操作对象和执行数学计算，这些在声明中是无法完成的。

4. 使用表达式

    表达式可用于向客户端输出内容，它将把代码的返回值输出到客户端，任何赋值表达式的整个右侧都可以用在表达式中。表达式的作用域与脚本相同。

### 3. 注释代码

1. xml注释：<!-- -->
2. java行注释 //
3. java块注释 /* */
4. JSP注释 <%-- --%>

用JSP注释包含的内容，不仅不会发送到浏览器，编辑器不会解释和转换它们（忽略）。其他3种注释里的内容都会添加到JSPServlet类中。

### 4. 在JSP中导入JAVA类:导入指令

```xml
<!-- JSP默认导入java.lang包里的类-->
<%@ import="java.util.*,java.io.IOException" %>
```

**注意**：对于不产生输出的JSP标记、声明、指令和脚本，它们都会向客户端输出一行空白。

### 5. 常用指令

#### 5.1 修改页面属性

- pageEncoding
- session
- isElIgnored
- buffer和autoflash:
- errorPage
- isErrorPage
- isThreadSafe
- extends
- 其他

#### 5.2 包含其他JSP页面

- 静态包含:<%@ include file="filepath" %>,编译器将被包含的JSP文件的内容替换include指令,再将合并的JSP文件转换成JAVA代码并编译,该动作只执行一次。
- 动态包含：<%@ jsp:include page="filepath" %>先生成java代码，每次访问页面执行该代码，将request和response对象交由该方法处理。

```java
org.apache.jasper.runtime.JspRuntimeLibrary.include(request, response, "index.jsp", out, false);
```

#### 5.3 包含标签库

```xml
<!-- uri指定标签库的命令空间，prefix指定引用库时使用的别名 -->
<%@ taglib uri="namespace" prefix="alias" %>
```

#### 5.4 jsp标签

- jsp:include
- jsp:forward
- jsp:useBean
- jsp:getProperty
- jsp:setProperty

### 6.在JSP中使用JAVA(以及不鼓励使用JAVA的原因)

#### 6.1 JSP中的内置(隐式)变量

JSP规范要求JSP的转换器和编译器提供这些变量，并且名字也要完全相同。它们被定义在JSP执行的Servlet方法的开头(Tomcat中是_jspService方法)，即这些变量的作用域在该方法中。这也意味着不能在JSP中使用声明来定义他们（作用域在整个类。）

- request和response
- session
- out
- application
- config
- pageContext
- page
- exception

#### 6.2. JSP中不要滥用JAVA代码，应该只做页面展示相关的事。

### 7. 结合使用Servlet和JSP：业务逻辑和表示展分享。

#### 7.1 JSP属性的复用：在配置文件web.xml中设置JSP属性，使用jsp-config标签

##### 7.1.1 匹配不同的JSP属性：jsp属性组jsp-property-group

```xml
<jsp-config>
    <jsp-property-group>
        <url-pattern>patter1</>
        <url-pattern>patter2</>
        <!-- jsp属性 -->
        ...
    </jsp-property-group>
    <jsp-property-group>
        <url-pattern>patter1</>
        <url-pattern>patter2</>
        <!-- jsp属性 -->
        ...
    </jsp-property-group>
</jsp-config>
```

- 如果应用程序中的某些文件同时匹配**serlvet-mapping**和JSP属性组中的**url-pattern**，那么更精确（相对于模糊）的URL会匹配成功，如果两者的url-pattern是一致的，那么优先匹配属性组而不是Servlet映射。
- 如果某些文件同时匹配多个属性组中的**url-pattern**,那么更精确（相对于模糊）的URL会匹配成功。如果多个匹配一致，那么按照在web.xml中的书写顺序，这些pattern中的第一个将成功匹配。
- 如果有文件同时匹配多个属性组中的**url-pattern**,并且这些属性组还包含了**include-prelude**或**include-coda**属性，那么这些属性将同时作用于该文件（因为一个jsp可以包含多个**其他**jsp文件）,但是只有一个组（根据上面两条规则匹配成功的属性组）的其他属性能够对该文件生效

##### 7.1.2 jsp属性

除了jsp-property-group标签和其下的url-pattern标签是必要的，其他jsp属性可选，但是在添加他们的时候有严格顺序（顺序略）。

#### 7.2 将Servlet中的**请求转发**给JSP

由Sevlet处理业务逻辑以及必需的数据存储或者读取，然后创建可以由JSP轻松处理的数据模型，最终将请求转发给JSP.

##### 7.2.1 **请求转发与重定向的区别**

请求转发：

请求转发，即request.getRequestDispatcher().forward()，是一种服务器的行为，客户端只有一次请求，服务器端转发后会将请求对象保存，地址栏中的URL地址不会改变，得到响应后服务器端再将响应发给客户端；

转发过程：
客户浏览器发送http请求----》web服务器接受此请求--》调用内部的一个方法在容器内部完成请求处理和转发动作----》将目标资源发送给客户；在这里，转发的路径必须是同一个web容器下的url，其不能转向到其他的web路径上去，中间传递的是自己的容器内的request。在客户浏览器路径栏显示的仍然是其第一次访问的路径，也就是说客户是感觉不到服务器做了转发的。转发行为是浏览器只做了一次访问请求。

请求重定向：

请求重定向，即response.sendRedirect()，是一种客户端行文，从本质上讲等同于两次请求，前一次请求对象不会保存，地址栏的URL地址会改变。

重定向过程：客户浏览器发送http请求----》web服务器接受后发送302状态码响应及对应新的location给客户浏览器--》客户浏览器发现是302响应，则自动再发送一个新的http请求，请求url是新的location地址----》服务器根据此请求寻找资源并发送给客户。在这里location可以重定向到任意URL，既然是浏览器重新发出了请求，则就没有什么request传递的概念了。在客户浏览器路径栏显示的是其重定向的路径，客户可以观察到地址的变化的。重定向行为是浏览器做了至少两次的访问请求的。

#### 7.3 关于JSP文档(JSPX)：使用xml文档来实现JSP

## 四、会话(Session):维持状态

### 4.1 使用会话的原因

关联同一用户的多个请求。

#### 4.1.1 维持状态

会话用于维护请求与请求之间的状态，Http请求自身是无状态的.从服务器的角度来说，当用户的Web浏览器打开第一个连接到服务器的套接字时请求就开始了，直到服务器返回最后一个数据包并关闭连接时，该请求结束。

#### 4.1.2 记住用户

#### 4.1.3 应用程序工作流

### 4.2 使用cookie和URL参数和服务器传递Session ID

web会话的基本理论和JavaEE Web应用程序中会话实现规范

web会话的基本理论:会话是由服务器或Web应用程序管理的某些数据（文件、内存片段对象或者容器），它包含了分配给他的各种不同数据。用户浏览器中不用保持或维持任何此类数据。

**Session ID**:关联用户浏览器和容器，随机生成的字符串(随机：防止会话劫持)。

**http会话流程**：略。

#### 4.2.1 Cookie技术

Http Cookie技术：将Session ID从服务器返回给用户浏览器，并在该浏览器之后的请求中包含此ID。cookie是一种必须的通信机制，可以通过Set-Cookie响应头在服务器和浏览器之间传递任意数据，并存储在用户计算机中，然后再通过请求头Cookie从浏览器返回到服务器中。

#### 4.2.2 URL中的Session ID

请求URL中的Session ID的产生：包含在应用程序返回的response中的Location头和返回页面的所有URL里(超链接，表单，重定向)。

**JavaEE Servlet API中的解决方案**：HttpServletResponse接口定义了两个可以重写URL的方法：encodeURL和encodeRedirectURL,它们都将在必须的时候把Session ID内嵌在URL中。需要满足以下4个条件：

- 会话对于当前请求是活跃的
- JSESSIONID cookie在请求中不存在
- URL不是绝对URL，并且都是同一WebAPP中的URL
- 在web.xml中启用了对会话URL重写的支持。

注：另一种方案是使用JSTL。

#### 4.2.3 Session中的漏洞

相关请访问Open Web Application Security Project(OWASP):<https://www.owasp.org/>

- 复制粘贴错误（暴露Session ID）
- 会话固定(分享带有SessionID的URL,当其他人访问该URL使用了该SessionID，等同于SessionID暴露了)
- 跨站脚本(如JavaScript)和Session劫持
- 不安全的cookie：MitM攻击。

最安全的防护：使用SSL/TLS会话ID

### 4.3 在Session中存储数据

#### 4.3.1 在web.xml中配置Session

```xml
<!-- 书写顺序固定 -->
<session-config>
    <session-timeout>30</session-timeout>
    <cookie-config>
        <name>JSESSIONID</name>
        <domain>xxx.com</domain>
        <path>/path</path>
        <comment><![CDATA[comment]]></comment>
        <http-only>true</http-only>
        <max-age>seconds</max-age>
        <tracking-mode>COOKIE</tracking-mode>
        <tracking-mode>URL</tracking-mode>
        <tracking-mode>SSL</tracking-mode>
    </cookie-config>
</session-config>
```

注：也可以代码中配置。

#### 4.3.2 存储和获取数据

#### 4.3.3 删除数据

使用removeAttribute()方法或将存储在Session中的对应数据置为空(空串，空容器等)。

#### 4.3.4 相关方法

- getCreationTime()
- getLastAccessedTime()
- isNew()
- getMaxInactiveInterval/setMaxInactiveInterval
- invalidate()注销会话

### 4.4 会话事件与监听器

会话事件：JavaEE中会话最重要的特性之一就是会话事件。当会话发生变化时（如：添加或移除属性），Web容器将这些变化通知应用程序。该功能通过**发布/订阅模式**实现，从而可以将修改会话和监听会话的代码解耦合。

监听器：用于监听会话事件。
tips:如果使用了一些第三方代码：如Spring Framework或Spring Security--对会话进行修改时，该功能非常有用，因为你可以在代码中检测到这些变化并且不需要修改第三方代码。

#### 4.4.1 注册监听器

1. web.xml中使用\<listener\>进行配置
2. 使用WebListener注解。
3. 从Servlet3.0/JavaEE开始，还可以在代码中使用ServletConfig中的addListener()方法。不过该方法只能在ServletContextListenr和contextInitialized方法或者ServletContainerInitializer中的onStartup方法中调用。

#### 4.4.2 维护活跃会话列表：使用JAVA容器维护会话

功能：当有一个会话被创建，将该会话添加到维护列表中；当一个会话被销毁时，从维护列表中移除；当一个会话被更新(changeSessionId)...,类似于anroid中维护Activity列表.

### 4.5 将使用Sesssion的应用程序集群化

群集实例间的通信（消息队列）：AMQP,JMS,MSMQ。

#### 4.5.1 在集群中使用Session ID

沾滞会话:使负载均衡机制能够感知到会话，并且总是将来自于同一会话的请求发送到相同的服务器。（支持扩展性，不支持高可用性，如果创建该会话的web服务器终止，该会话将丢失）

#### 4.5.2 了解会话复制和故障恢复

会话复制：如果创建某个会话的服务器终止了，那么该会话将丢失。使用会话复制技术，可以将会话在整个集群中复制，无论他产生于哪个实例，它对所有web容器都是可用的。

在web.xml中使用\<distribuable/ \>代表了会话将在整个集群中复制。当某个实例创建了会话，它将被复制到其他实例中。如果会话的属性发生了变化，改变后的会话也会被重新复制到其他实例中，使所有实例保持最新的会话状态。

tips：这两种技术并不互斥，结合两者来实现**故障恢复：会话仍然被复制，但同一会话的请求也将被发送到同一服务器，如果该服务器终止，此时请求将被发送到另一个得知此会话的实例。**要满足实际需求需要多种技术结合。

## 五、JSP-EL

EL最初是JSTL的一部份（由于其流行，现在是JSP规范的一部分），用于在不使用脚本、声明或者表达式的情况下，在JSP页面中渲染数据，简化JSP书写。
它的灵感和设计依据来源于ECMAScript和XPath语言。

### 5.1 EL表达式基本语法

EL的基本语法描述了一个必须和其他JSP页面语法分开执行的表达式。JSP转换器必须能够检测到EL表达式的开始和结束，并能与其他页面区分开，然后正确的解析和执行表达式。

EL的语法有两种不同的类型：立即执行和延迟执行。

#### 5.1.1 立即执行

立即执行的表达式将在页面渲染的时候，被JSP引擎解析和执行。**因为JSP从上到下执行，这意味着EL表达式将在JSP引擎发现它，并在执行其他页面部分之前执行他**。

```jsp
${expr}
```

#### 5.1.2 延迟执行

延迟执行EL是JUEL的一部分，主要满足JavaServer Faces的需要。

```jsp
#{expr}
```

在**JSF**中，延迟执行EL将在页面渲染或回传到页面时执行，或者同时在两个阶段执行，这与在JSP中不同，**JSP中的EL表达式**没有生命周期概念。

在JSP中，#{}迟延执行语法只是一个有效的JSP标签属性，用于将EL表达式的执行推迟到渲染过程中。不同于在属性值绑定到标签之前执行的EL表达式(如：${})，该标签的属性将获取得一个对未执行的EL表达式的引用。该标签可以之后某个合适的时候，调用一个方法来执行该EL。

#### 5.1.3 使用EL表达式

- El可以直接用在JSP的任何位置，除了JSP指令(指令会在JSP编译时执行，而EL是在JSP渲染时执行),另外JSP脚本，声明，JSP表达式中的EL也是无效的，而且可能导致错误。
- HTML/CSS/JS代码中

### 5.2  EL语法

#### 5.2.1 保留字

- true
- false
- null
- instanceof
- empty
- div
- mod
- and
- or
- not
- eq
- ne
- lt
- gt
- le
- ge

#### 5.2.2 操作符优先级

1. \[\]（中括号）和"."(点)操作符
2. ()分组括号：作用和数学上的括号一样
3. 1元运行符：unary,-取负,not,!和empty
4. 数学运行符：x,/和div,%和mod
5. \+ math,binary \-
6. 字符串链接符 +=
7. 比较运算：<,lt,>,gt,<=,le,>=,ge
8. 比较运算：==,eq,!=,ne
9. &&,and
10. ||,or
11. 三目运算： (? : )
12. lambada表达式:->
13. 赋值:=
14. 分号表达式;(类似c中的逗号运行，结果为最后一个分号右边的表达式的值)

#### 5.2.3 常量（字面量）

JUEL可以使用通过使用特定的语法指定字面量。如true,false,null关键字，他们都是字面量

1. EL中的字符串：使用双引号或单引号
2. EL中的数值常量：整数默认是int,小数是float，超过大小自动转换，并且不能显示指定数值类型，只能以隐式的方式进行处理。
3. EL中的常量集合
    - 常量集合将构造一个HashSet\<Object\>,使用{常量1,2..}
    - 常量列表将构造一个ArrayList\<Object\>，使用[常量1,2...]
    - 常量Map将构造一个HashMap\<Object,Object\>,使用{key1:value1...}

#### 5.2.4 操作对象的属性和方法

1. 获取对象属性

    ```js
    /*
    获取对象的属性：要求该成员变量必须符合JavaBean的标准
    **/

    //方法一：
    ${object.xxx} //实际调用的是 object.getXXX()方法，如果该对象没有getXXX()方法将会报错

    //方法二：使用[]操作符
    ${object.["xxxx"]} //实际调用的是 object.getXXX()方法
    ```

2. 操作对象方法

    ```js
    /*
    EL是用来渲染页面的，所有该方法必须有返回值
    如果返回值是一个对象，那么会调用他的toString()方法
    **/
    ${object.method(参数列表)}
    ```

#### 5.2.5 EL函数

EL函数的标准定义在TLD（标签库描述符,是一个文件）中
在EL中,函数是映射到类中**静态方法**的一个特殊工具。如xml标签一样，函数会被映射到命名空间。

```js
//ns命令空间，fn函数名
${[ns]:[fn]{参数列表}}
```

常用JSTL EL函数：

- ${fn:contains(String1,String2)}
- ${fn:escapeXml(String)}
- ${fn:join(String[],String)}
- ${fn:length(Object)}
- ${fn:toLowerCase(String)}和${fn:toUpperCase(String)}
- ${fn:trim(String)}
- 更多可用函数查看JSTL文档

#### 5.2.6 静态字段和方法访问

```js
/*
获取静态字段值
注意：只能获取，不能修改该静态常量的值
**/
${java.lang.Integer.MAX_VALUE} //全类名.变量名
//如果该类已经使用JSP page指令导入，可简化
${Integer.MAX_VALUE}

/*
调用静态方法：与使用静态常量一致
**/

/*
还可以调用类的构造函数得到该类的一个实例，然后访问他的属性、方法
**/
${com.zk.User()}
${com.zk.User('First','Last').firstName}
```

#### 5.2.7 枚举

EL中的枚举将在必须的时候被强制转换为字符串，或者从字符串转换为枚举。

例如JSP中有一个局部变量dayOfWeek变量，它是Java 8新增的日期和时间API中java.time.DayOfWeek枚举类的实例。
可以使用下面的字符串测试dayOfWeek代表的是不是星期六:

```js
${dayOfWeek == 'SATURDAY'} //不安全，周六的字符串可能写错，编译器无法检查

${dayOfWeek == java.time.DayOfWeek.SATURDAY}
```

#### 5.2.8 lambda表达式：匿名函数

EL3.0中新增特性

#### 5.2.9 在EL中访问集合：获取集合中的元素

在ES中能直接访问map,list，其他类型的集合不能直接访问。但所有集合类型都能使用empty操作符来判断是否为空。

```js
/*
访问map
**/
// 方式一：推荐
${map["key"]}

//方式二:使用这种方法，key的命令必须符合Java中标识符的命令标准。
${map.key}

/*
访问list
**/
//方式一：推荐
${list[index]}

//方式二：该index值必须能够转换为整数。而且和map使用方式不太容易区别开
${list["index"]}
```

### 5.3 在EL中使用域变量

- page域
- request域
- session域
- application域

#### 5.3.1 在EL中使用隐式域(scope)

EL中定义了11个隐式域变量，当一个EL表达式引用了一个变量时，EL求值程序将按照下面的流程解析变量：

1. 检查该变量是否是隐式域变量
2. 如果不在11个隐式变量之中，EL求值程序将在page scope当中寻找该属性(PageContext.getAttribute("varName")),检查其中是否包含了同名变量(大小写敏感)，如果找到，则使用该属性值作为变量的值。
3. 如果在page scope中未找到,在request域里查找...
4. 在session scope里查找...
5. 在application scope里查找...
6. 都没找到，报错

所以4个scope的优先级是：page > request > session >application.

```xml
<!-- 下面的JSP注释告诉IDE本页面中使用了一个在隐式scope中的user变量,他的类型是com.zk.User。-->
<!-- 这可以使IDE能在编译前识别该类型，它就能正常提供自动完成、智能建议，检查EL表达式是否正确等功能 -->
<%--@elvariable id="user" type="com.zk.User"--%>
```

#### 5.3.2 使用隐式的EL变量(内置变量)

- pageContext是PageContext类的一个实例
- pageScope是一个Map<String,Object>,他包含了所有绑定到PageContext的属性。
- requestScope是一个Map<String,Object>,他包含了所有绑定到ServletRequest的属性.
- sessionScope是一个Map<String,Object>,他包含了所有绑定到当前会话的属性。
- applicationScope是一个Map<String,Object>，他包含了所有绑定到ServletContext的属性
- param和paramValues：提供对请求参数的访问。
- header和headerValues提供对请求头的访问。
- initParam，它包含了该applicaiton中的ServlectContext实例的所有上下文初始化参数。
- cookie，他包含了用户浏览器发送的请求中的所有cookie.

### 5.4 使用流API访问集合：集合流API

Jave EE7的EL3.0新增的重大特性之一是：支持Java SE8引入的**集合流API**。因为EL3.0将以原生的方式支持该API,所以如果希望使用该EL特性，并不需要在Java 8中运行应用程序。

流API的基础是所有collection中存在的无参stream方法。该方法将返回java.util.stream.Stream类的一个实例，通过该对象可以操作集合的**副本**(如过滤和排序等)。

JDK8 的Stream 是一个受到**函数式编程**和**多核时代**影响而产生的东西。很多时候我们需要到底层返回数据，上层再对数据进行遍历，进行一些数据统计，但是之前的Java API 中很少有这种方法，这就需要我们自己来 Iterator 来遍历，如果JDK 能够为我们提供一些这种方法，并且能够为我们优化就好了。

所以JDK8加入 了 java.util.stream包，实现了集合的流式操作，流式操作包括集合的**过滤，排序，映射**等功能。根据流的操作性，又可以分为 **串行流** 和 **并行流**。根据操作返回的结果不同，流式操作又分为**中间操作**和**最终操作**。大大方便了我们对于集合的操作。

- 串行流:操作在一个线程中依次完成。
- 并行流在多个线程中完成。
- 最终操作：返回一特定类型的结果。
- 中间操作：返回流本身。

链式管道:管道源(源Stream) ->中间操作(如过滤和排序)->最终结果(如结果stream转换成可遍历和显示的List)

#### 5.4.1 了解中间操作

中间操作都是基于Stream执行的，并不会修改原始集合，这些操作只会影响流中副本的内容。

1. 过滤元素filter()和distinct()
2. 对元素进行排序sort()
3. 限制流中元素的大小limit()和subStream()
4. 元素映射map()

#### 5.4.2 使用终结操作

1. forEach()遍历元素
2. 聚合函数
3. toArray(),toList()
4. reduce()
5. collection()

总结：尽管EL表达式可以替换许多JAVA代码，但它们无法替换JSP中所有的JAVA代码。如：不能在循环中使用EL，或者根据某些表达式是否为真执行指定代码(分支)。为此我们需要JSTL.

## 六、使用JSTL（Java标准标签库）

### 6.1 JSP标签和JSTL

使用jsp指令taglib引入的标签库中的URI并不是实际的TLD文件的位置(并不是一个真正的URI)，该URI只是一种用于识别唯一TLD的技术，通过这种方式可以正确地关联到相应的TLD文件。

使用该了该指令将阻止XML文档解析器解析JSP，相反WEB容器中的JSP解析器可以识别。

当JSP解析器遇到taglib指令时，它会根据URI在**JSP规范中定义的不同位置中**定位相应的TLD文件。JSP规范定义的这些位置如下(搜索范围优先级从上到下)：

1. 如果使用的容器是一个兼容Java EE的容器，那么解析器将搜索所有匹配Java EE规范的TLD文件，包括JSP标签库，JSTL和所有JavaServer Faces库。
2. 部署描述符文件(web.xml)中\<jsp-config>中的显式\<taglib>声明。
3. /WEB-INF目录或所有子目录中的TLD文件，或者/WEB-INF/lib所有JAR文件的MATA-INF目录中的所有TLD文件。
4. 最后，解析器将检查web容器或者应用服务器中的所有TLD文件(到这步一般这个web容器不与Java EE规范兼容，)

JSTL中的5个标签库:

- core
- format
- function
- sql
- xml

### 6.2 使用core标签库

#### 6.2.1 <c:out>

```xml
<c:out value="${el}" defalut="${el}">
<!-- 该标签实际赞同于${fn:escapeXml(variable)} ,默认会对xml保留字符进行转义-->
<c:out value="${el}" defalut="${el}" escapeXml=true>
```

#### 6.2.2 <c:url>

标签<c:url>最大的作用是正确的**对URL进行编码**，并通过JSP输出到Response中

```xml

<!-- 当JSP引擎渲染JSP时，会解析<c:url>标签并替换它，它将把所有不是JSP特有语法的问法当作普通文本 -->
<a href="<c:url value='https://www.baidu.com'>"/>超链接</a>

<!-- 绝对URL -->
<c:url value=“https://www.baidu.com”>
    <c:param name="paramName" value="paramValue" />
</c:url>

<!-- 相对URL，此时该标签生成的URL的父path为application部署的context -->
<c:url value=“/view.jsp”>
    <c:param name="paramName" value="paramValue" />
</c:url>

<!-- 相对URL，也可以通过属性指定context -->
<c:url value=“/view.jsp” context="/">
    <c:param name="paramName" value="paramValue" />
</c:url>

<!-- 如果某个URL**需要使用多次**，可以将该URL保存到scope中(默认为page scope) -->
<c:url value=“/view.jsp” var="urlName" scope="request">
    <c:param name="paramName" value="paramValue" />
</c:url>
```

#### 6.2.3 <c:if>

单条件标签，用于控制是否渲染指定内容。

#### 6.2.4 <c:choose>

多条件标签，用于控制是否渲染指定内容。

#### 6.2.5 <c:forEach>

varStatus属性

- begin
- end
- step
- index
- count
- current
- first
- last

#### 6.2.6 <c:forTokens>

#### 6.2.7 <c:redirect>

重定向：在响应头中添加HTTP Location Header并修改响应状态码，它将终止JSP的执行。

#### 6.2.8 <c:import>获取特定URL资源的内容。

#### 6.2.9 <c:set>和<c:remove>

### 6.3 使用国际化(i18n)和格式化标签库(FMT命令空间)

国际化和本地化(l10n):首先通过架构进行国际化，然后通过转换进行本地化。

#### 6.3.1 国际化和本地化组件

国际化和本地化工作由三个部分组成：

- 文本转换:使用其他语言的用户能够使用该应用程序
- 特殊字符格式化：根据不同的语言环境将日期、时间、数字(包括货币和百分比)进行正确格式化。
- 价格本地化（除需求指定实现，一般显示为一种国际性货币，如美元）：将价格以用户本地货币显示。

区域设置：语言代码_国家代码（如en_US）。（参考ISO标签和JDK API java.util.Local）

国际化和本地化标签分为两大类：

- i18n标签
- 日期、时间、数字格式化标签  （JDK 相关API）

i18n标签的**资源包**：它定义了特定区域设置的对象。资源包由对应着包中条目的键组成，将开发都选择的区域代码添加到任意的基本名称上即可组成完整的资源包名称。特定的键通常在所有的资源包都有条目存在，每种支持的语言和国家各有一条。

#### 6.3.2 <fmt:message>

该标签将在资源包中定位到某个本地化消息，然后将它内嵌在页面的消息中或者保存到EL变量中。

本地化消息文件中的占位符："{index}",index从0开始。如果消息中包含了占位符但未使用<fmt:param>替换对应的值，那么该占位符将保持原样显示。

```xml
<fmt:message key="keyOfMessage">
    <fmt:param value="${el}"> <!-- 替换index为0的占位符-->
    <fmt:param value="${el}"> <!-- 替换index为1的占位符-->
</fmt:message>
```

#### 7.3.3 <fmt:setLocale>：java.util.Locale

该标签将设置i18n解析资源包时使用的区域设置并进行格式化。

JSTL中的i18n标签依赖于本地化上下文告诉它们当前的资源包和区域设置。可使用<fmt:setLocale>和其他技术指定当前本地化上下文区域设置。

#### 7.3.4 <fmt:bundle>和<fmt:setBundel>:java.util.ResourceBundle

<fmt:bundle>指定上下文，<fmt:setBundel>保存为EL变量

<fmt:setLocale>和<fmt:setBundle>是指定使用资源包两种方式。当i18n标签需要本地化上下文时，搜索过程如下：

1. 如果在<fmt:message>中指定了bundle属性，那么使用该值.
2. 如果i18n标签被内嵌在<fmt:bundle>中，那么它将使用该资源包。
3. 上下文初始化参数或者EL变量javax.servlet.jsp.jstl.fmt.localizationContent指定的默认上下文。

```xml
<!-- setBundle 标签如果不指定var属性，那么该标签生成的EL变量将保存在名为javax.servlet.jsp.jstl.fmt.localizationContent的变量中-->
<!-- basename表示资源包名称-->
<fmt:setBundle basename="name1" var="bundleName" />
<fmt:bundle basename="name2">
    <fmt:message key="messageKey1" />
    <fmt:message key="messageKey2" bundle="${bundleName}" />
</fmt:bundle>
```

#### 6.3.5 <fmt:timeZone>和<fmt:setTimeZone>

时区设置优先级：

1. 格式化标签中指定的timeZone属性
2. <fmt:timeZone>标签
3. 上下文初始化参数或者javax.servlet.jsp.jstl.fmt.timeZone的el变量
4. 容器提供的时区。

#### 6.3.6 <fmt:formatDate>和<fmt:parseDate>

#### 6.3.7 <fmt:formartNumber>和<fmt:parseNumber>

## 七、 自定义标签和函数库

### 7.1 了解TLD、标签文件和标签处理器

两种定义方式方式：

1. TLD文件：标签库描述文件，是一个XML文件，可以包含多个标签定义。
2. tag/tagx文件:是一个JSP文件。一个文件代表一个标签。

**标签处理器**：所有JSP标签都将引起某些标签处理器的执行。标签处理器是javax.servlet.jsp.tagext.Tag或者javax.servlet.jsp.tagext.SimpleTag的实现类，其中包含了用于完成标签目的的必要代码。
标签处理器在TLD的标签定义中指定，容器使用该信息将JSP中的标签映射到对应的Java代码。

**标签文件**：**标签**不一这定要被显示地编写为Java代码，正如容器可以将JSP文件转换和编译成HttpServlet一样，它也可以将**标签文件**转换和编译成SimpleTag。标签文件不如直接的Java代码强大，并且它无法像显示的标签处理器一样解析标签中的**嵌套标签**，但是标签文件可以使用JSP这样的简单标签并支持在其中使用其他JSP标签。**TLD中的标签定义可以指向一个标签处理器或者标签文件**。

```xml
<!-- tagdir目录下的所有.tag和.tagx文件都会被绑定到myTags命名空间 -->
<!-- Application中的文件必须被添加到/WEB-INF/tags目录下或其子目录下-->
<%@ taglib prefix="myTags" tagdir="/WEB-INF/tag"%>

<!-- 使用标签 -->
<!-- 其中myTags代表taglib中属性tagdir目录 标签main是tag目录下的一个.tag文件的文件名,即main.tag-->
<myTags:main ...>
```

tip:JSP标签文件在应用程序(项目)文件中必须放到/WEB-INF/tags目录下，并且可以在TLD中声明。如果标签文件被添加到JAR中，必须放到/META-INF/tag目录下且必须在该JAR的/META-INF/目录中的tld声明。

### 7.1.1 读取Java标签库TLD(c.tld)

在org.glassfish.web:javax.servlet.jsp.jstl Maven artfcat JAR文件的/MEATA-INF/tag目录下可以找到该文件。

```xml
<!-- 文档根元素，声明了将使用XML schema定义文件的位置（xxx.xsd）,该文件描述xml文件的结构(也就是tld文件)-->
<taglib xmlns="http://java.sun.com/xml/ns/javaee"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-jsptaglibrary_2_1.xsd"
    version="2.1">
    <!-- xsd文件严格了元素顺序，如元素顺序有误，则该TLD文件无效-->
    <!--前5个元素声明了关于标签库的通用信息-->
    <description>JSTL 1.2 core library</description>
    <display-name>JSTL core</display-name>
    <tlib-version>1.2</tlib-version>
    <short-name>c</short-name>
    <uri>http://java.sun.com/jsp/jstl/core</uri>
```

1. 定义验证器和监听器

    ```xml
    <validator>
        <description>
            Provides core validation features for JSTL tags.
        </description>
        <validator-class>
            org.apache.taglibs.standard.tlv.JstlCoreTLV
        </validator-class>
    </validator>
    ```

    验证器的实现是比较复杂的，因为它要求实际的去解析JSP语法，通常情况下我们不要使用它。

2. 定义标签:tag标签

    ```xml
    <tag>
        <description>
        Simple conditional tag, which evalutes its body if the
        supplied condition is true and optionally exposes a Boolean
        scripting variable representing the evaluation of this condition
        </description>
        <name>if</name>
        <!-- 声明负责执行标签的标签处理器类(Tag或SimpleTag) -->
        <tag-class>org.apache.taglibs.standard.tag.rt.core.IfTag</tag-class>
        <!-- 指定允许嵌套内容类型，JSP表示该标签的嵌套内容可以是任何JSP内容，但不包括声明-->
        <body-content>JSP</body-content>
        <attribute>
            <description>
    The test condition that determines whether or
    not the body content should be processed.
            </description>
            <name>test</name>
            <required>true</required>
            <rtexprvalue>true</rtexprvalue>
        <type>boolean</type>
        </attribute>
        <attribute>...</attribute>
    </tag>
    ```

3. 定义标签文件(xx.tag/tagx):\<tag-file>

4. 定义函数：实际上是一个JAVA类的静态方法。
5. 定义标签库扩展(不常用)

#### 7.1.2 标签文件指令

- include
- taglib
- tag

### 7.2 将标签文件用作HTML模板

使用标签文件最强大的特性：就是使用它为应用程序创建HTML模板。该模板可以处理跨应用程序多个页面的重复任务,减少重复代码并易于修改。

### 7.3 标签处理器

重要：**了解标签处理器的不同类型**

## 八、 过滤器

### 8.1 使用过滤器的目的

过滤器是可以**拦截**访问资源的**请求和响应**的应用组件，它们将以某种方式作用于这些请求或响应。过滤器可以检测和修改请求和响应。实现javax.servlet.Filter接口用于创建过滤器，和Servlet一样，它可以在部署描述符中和代码中注册声明。

以下是几个过滤器的应用例子：

- 日志过滤器
- 验证过滤器
- 压缩和加密过滤器
- 错误过滤器

### 8.2 创建、配置和映射过滤器：类似Servlet

- doFilter()方法
- FilterChain对象
- FilterChain.doFilter()方法

#### 8.2.1 过滤器链

工作流程（类似栈）：

请求->容器->过滤器链->Servlet处理请求并响应
Servlet响应->过滤器链->容器->浏览器客户端

Filter调用FilterChian.doFilter()将在过滤器链中调用下一个Filter。如果调用的Filter是过滤器链中的最后一个过滤器，那么将在过滤器链结束时访问该资源(将控制权交给Servlet),如果当前过滤器示调用FilterChain.doFilter(),那么过滤器链将被中断，所有之后的过滤器和Servlet将无法接收处理该请求。

#### 8.2.2 映射到URL-Pattern和Servlet名称

通过URL-Pattern匹配拦截请求：如同Servlet一样，过滤器可以映射到URL,这会决定哪个或哪些过滤器将拦截某个请求。任何匹配某个过滤器的URL-pattern的请求在被匹配的Servlet处理之前将首先进入该过滤器。

通过Servlet名称拦截所有匹配该Servlet的请求。

一个过滤器可以同时拦截多个URL-Pattern和Servlet名称，多个过滤器也可以拦截相同的URL或者Servlet名称。

#### 8.2.3 映射到不同的请求派发器类型

在Servlet容器中，可以通过多种方式派发请求：

- 普通请求
- 转发请求：jsp:forward或者调用RequestDispatcher的forward方法。
- 包含请求：jsp:include标签或者调用RequestDispatcher的include方法时将分产生一个一同的与原始请求相关的内部包含请求。
- 错误资源请求
- 异步请求：在处理其他请求的过程中，使用AsyncContext派发的请求。

#### 8.2.4 在部署描述符中配置Filter

```xml
<filter>
    <filter-name><filter-name>
    <filetr-class><filter-class>
</filter>
<filter-mapping>
    <filter-name><filter-name>
    <url-pattern>pattern1</url-pattern>
    <url-pattern>pattern2</url-pattern>
    ...
    <servlet-name></servlet-name>
    ...
    <!-- 请求转发类型：REQUEST/FORWARD/INCLUDE/ERROR -->
    <!-- 过滤器可以map到0个或多个请求转发类型,默认REQUEST-->
    <dispatcher>REQUEST</dispatcher>
    ...
</filter-mapping>
```

#### 8.2.4 使用注解配置：@WebFilter

使用注解的缺点：不能对过滤器链上的过滤器进行排序。

#### 8.2.4 编程方式配置

如同Servlet、监听器和其他组件一样，可以在ServletContext中配置过滤器。因为这必须要在ServletContext启动之前完成(意思是在初始化中注册)，所以需要在ServletContextListener的contextInitialized方法中实现，也可以在ServletContainerInitializer的onStartup方法中添加过滤器。

### 8.3 Filter生命周期

与Servlet不同的是，过滤器不可以在第一个请求到达时加载。过滤器的init方法总是在应用程序启动时调用：在ServletContextListerner初始化之后，Servlet初始化之前，按照xxx顺序依次加载。

### 8.4 过滤器排序

过滤器的顺序决定了它们在过滤器链中出现的位置。

默认的过滤器顺序：

1. 匹配请求的过滤器将按照它们出现在部署描述符或者编程式配置中的顺序添加到过滤器链中(如果同时在部署描述符或者编程式配置中设置了过滤器，如果需要代码配置中的过滤器出现在XML配置的过滤器之前，那么需要在代码配置中使用addMapping方法的第2个参数)
2. URL映射的过滤器优先级比Servlet名称映射的过滤器优先级高。这意味着如果这两种类型的过滤器同时匹配某个请求，URL映射过滤器在过滤器链中出现的位置将总是在Servlet名称过滤器之前(即URL映射过滤器先执行。即使url映射的过滤器在Servlet名称过滤器之后声明)。

#### 8.4.1 使用过滤器处理异步请求:AsyncContext

异步请求处理的关键在于：Servlet的service方法可以在响应发送到客户端之前返回。然后请求处理将被委托到另一个线程或者基于某些事件(监听器)完成。