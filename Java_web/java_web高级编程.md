# Java Web高级编程学习笔记

- [Java Web高级编程学习笔记](#java-web%E9%AB%98%E7%BA%A7%E7%BC%96%E7%A8%8B%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0)
    - [一、Java EE相关概念](#%E4%B8%80%E3%80%81java-ee%E7%9B%B8%E5%85%B3%E6%A6%82%E5%BF%B5)
        - [1. JavaEE平台规范：Servlet,过滤器，jsp,JUEL等等组件的标准。](#1-javaee%E5%B9%B3%E5%8F%B0%E8%A7%84%E8%8C%83%EF%BC%9Aservlet%E8%BF%87%E6%BB%A4%E5%99%A8%EF%BC%8Cjspjuel%E7%AD%89%E7%AD%89%E7%BB%84%E4%BB%B6%E7%9A%84%E6%A0%87%E5%87%86%E3%80%82)
        - [2. web容器/servlet容器](#2-web%E5%AE%B9%E5%99%A8servlet%E5%AE%B9%E5%99%A8)
    - [二、Servlet类](#%E4%BA%8C%E3%80%81servlet%E7%B1%BB)
        - [1. 创建Servlet类](#1-%E5%88%9B%E5%BB%BAservlet%E7%B1%BB)
            - [1.1 Servlet类的体系结构。](#11-servlet%E7%B1%BB%E7%9A%84%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84%E3%80%82)
            - [1.2 处理HTTP请求](#12-%E5%A4%84%E7%90%86http%E8%AF%B7%E6%B1%82)
            - [1.3 初始化和销毁:Servlet的生命周期](#13-%E5%88%9D%E5%A7%8B%E5%8C%96%E5%92%8C%E9%94%80%E6%AF%81servlet%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
        - [2. 配置可部署的Servlet：web.xml](#2-%E9%85%8D%E7%BD%AE%E5%8F%AF%E9%83%A8%E7%BD%B2%E7%9A%84servlet%EF%BC%9Awebxml)
            - [2.1 配置Servlet:Servlet标签](#21-%E9%85%8D%E7%BD%AEservletservlet%E6%A0%87%E7%AD%BE)
            - [2.2 将Servlet映射到URL:Servlet-mapping标签](#22-%E5%B0%86servlet%E6%98%A0%E5%B0%84%E5%88%B0urlservlet-mapping%E6%A0%87%E7%AD%BE)
        - [3. 了解doGet，doPost和其他方法](#3-%E4%BA%86%E8%A7%A3doget%EF%BC%8Cdopost%E5%92%8C%E5%85%B6%E4%BB%96%E6%96%B9%E6%B3%95)
            - [3.1. service方法](#31-service%E6%96%B9%E6%B3%95)
            - [3.2 HttpServletRequest接口](#32-httpservletrequest%E6%8E%A5%E5%8F%A3)
                - [3.2.1 获取请求参数](#321-%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
                - [3.2.2 确定与请求内容（请求正文）相关信息:getContentXXX()方法](#322-%E7%A1%AE%E5%AE%9A%E4%B8%8E%E8%AF%B7%E6%B1%82%E5%86%85%E5%AE%B9%EF%BC%88%E8%AF%B7%E6%B1%82%E6%AD%A3%E6%96%87%EF%BC%89%E7%9B%B8%E5%85%B3%E4%BF%A1%E6%81%AFgetcontentxxx%E6%96%B9%E6%B3%95)
                - [3.2.3 获取请求正文:使用getInputStream或getReader。](#323-%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E6%AD%A3%E6%96%87%E4%BD%BF%E7%94%A8getinputstream%E6%88%96getreader%E3%80%82)
                - [3.2.4 获取Http请求特有的数据URL,URI,和头信息](#324-%E8%8E%B7%E5%8F%96http%E8%AF%B7%E6%B1%82%E7%89%B9%E6%9C%89%E7%9A%84%E6%95%B0%E6%8D%AEurluri%E5%92%8C%E5%A4%B4%E4%BF%A1%E6%81%AF)
                - [3.2.5 会话和Cookies](#325-%E4%BC%9A%E8%AF%9D%E5%92%8Ccookies)
            - [3.3 使用HttpServletResonse](#33-%E4%BD%BF%E7%94%A8httpservletresonse)
                - [3.3.1 编写响应正文](#331-%E7%BC%96%E5%86%99%E5%93%8D%E5%BA%94%E6%AD%A3%E6%96%87)
                - [3.3.2 设置头和其他response属性](#332-%E8%AE%BE%E7%BD%AE%E5%A4%B4%E5%92%8C%E5%85%B6%E4%BB%96response%E5%B1%9E%E6%80%A7)
        - [4.使用初始化参数配置应用程序](#4%E4%BD%BF%E7%94%A8%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%82%E6%95%B0%E9%85%8D%E7%BD%AE%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)
            - [4.1 使用Context初始化参数](#41-%E4%BD%BF%E7%94%A8context%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%82%E6%95%B0)
            - [4.2 使用Servlet初始化参数](#42-%E4%BD%BF%E7%94%A8servlet%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%82%E6%95%B0)
        - [5. 通过表单上传文件:Servlet的multipart-config及Http-response的header设置(attachment)](#5-%E9%80%9A%E8%BF%87%E8%A1%A8%E5%8D%95%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6servlet%E7%9A%84multipart-config%E5%8F%8Ahttp-response%E7%9A%84header%E8%AE%BE%E7%BD%AEattachment)
        - [6. 编写多线程安全的应用程序](#6-%E7%BC%96%E5%86%99%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8%E7%9A%84%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)
            - [6.1 理解请求、线程、方法执行](#61-%E7%90%86%E8%A7%A3%E8%AF%B7%E6%B1%82%E3%80%81%E7%BA%BF%E7%A8%8B%E3%80%81%E6%96%B9%E6%B3%95%E6%89%A7%E8%A1%8C)
            - [6.2 保护共享资源：多线程的典型问题，即资源竞争（处理不好会导致死锁）。](#62-%E4%BF%9D%E6%8A%A4%E5%85%B1%E4%BA%AB%E8%B5%84%E6%BA%90%EF%BC%9A%E5%A4%9A%E7%BA%BF%E7%A8%8B%E7%9A%84%E5%85%B8%E5%9E%8B%E9%97%AE%E9%A2%98%EF%BC%8C%E5%8D%B3%E8%B5%84%E6%BA%90%E7%AB%9E%E4%BA%89%EF%BC%88%E5%A4%84%E7%90%86%E4%B8%8D%E5%A5%BD%E4%BC%9A%E5%AF%BC%E8%87%B4%E6%AD%BB%E9%94%81%EF%BC%89%E3%80%82)
    - [三. JSP的基本规则：JAVA模板引擎(用于代替手动拼接字符串，但其本质还是做页面字符串的拼接)。](#%E4%B8%89-jsp%E7%9A%84%E5%9F%BA%E6%9C%AC%E8%A7%84%E5%88%99%EF%BC%9Ajava%E6%A8%A1%E6%9D%BF%E5%BC%95%E6%93%8E%E7%94%A8%E4%BA%8E%E4%BB%A3%E6%9B%BF%E6%89%8B%E5%8A%A8%E6%8B%BC%E6%8E%A5%E5%AD%97%E7%AC%A6%E4%B8%B2%EF%BC%8C%E4%BD%86%E5%85%B6%E6%9C%AC%E8%B4%A8%E8%BF%98%E6%98%AF%E5%81%9A%E9%A1%B5%E9%9D%A2%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E6%8B%BC%E6%8E%A5%E3%80%82)
        - [1.JSP的运行原理(本质是一个Servlet)](#1jsp%E7%9A%84%E8%BF%90%E8%A1%8C%E5%8E%9F%E7%90%86%E6%9C%AC%E8%B4%A8%E6%98%AF%E4%B8%80%E4%B8%AAservlet)
        - [2. 指令、声明、脚本和表达式](#2-%E6%8C%87%E4%BB%A4%E3%80%81%E5%A3%B0%E6%98%8E%E3%80%81%E8%84%9A%E6%9C%AC%E5%92%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [3. 注释代码](#3-%E6%B3%A8%E9%87%8A%E4%BB%A3%E7%A0%81)
        - [4. 在JSP中导入JAVA类:导入指令](#4-%E5%9C%A8jsp%E4%B8%AD%E5%AF%BC%E5%85%A5java%E7%B1%BB%E5%AF%BC%E5%85%A5%E6%8C%87%E4%BB%A4)
        - [5. 常用指令](#5-%E5%B8%B8%E7%94%A8%E6%8C%87%E4%BB%A4)
            - [5.1 修改页面属性](#51-%E4%BF%AE%E6%94%B9%E9%A1%B5%E9%9D%A2%E5%B1%9E%E6%80%A7)
            - [5.2 包含其他JSP页面](#52-%E5%8C%85%E5%90%AB%E5%85%B6%E4%BB%96jsp%E9%A1%B5%E9%9D%A2)
            - [5.3 包含标签库](#53-%E5%8C%85%E5%90%AB%E6%A0%87%E7%AD%BE%E5%BA%93)
            - [5.4 jsp标签](#54-jsp%E6%A0%87%E7%AD%BE)
        - [6.在JSP中使用JAVA(以及不鼓励使用JAVA的原因)](#6%E5%9C%A8jsp%E4%B8%AD%E4%BD%BF%E7%94%A8java%E4%BB%A5%E5%8F%8A%E4%B8%8D%E9%BC%93%E5%8A%B1%E4%BD%BF%E7%94%A8java%E7%9A%84%E5%8E%9F%E5%9B%A0)
            - [6.1 JSP中的内置(隐式)变量](#61-jsp%E4%B8%AD%E7%9A%84%E5%86%85%E7%BD%AE%E9%9A%90%E5%BC%8F%E5%8F%98%E9%87%8F)
            - [6.2. JSP中不要滥用JAVA代码，应该只做页面展示相关的事。](#62-jsp%E4%B8%AD%E4%B8%8D%E8%A6%81%E6%BB%A5%E7%94%A8java%E4%BB%A3%E7%A0%81%EF%BC%8C%E5%BA%94%E8%AF%A5%E5%8F%AA%E5%81%9A%E9%A1%B5%E9%9D%A2%E5%B1%95%E7%A4%BA%E7%9B%B8%E5%85%B3%E7%9A%84%E4%BA%8B%E3%80%82)
        - [7. 结合使用Servlet和JSP：业务逻辑和表示展分享。](#7-%E7%BB%93%E5%90%88%E4%BD%BF%E7%94%A8servlet%E5%92%8Cjsp%EF%BC%9A%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91%E5%92%8C%E8%A1%A8%E7%A4%BA%E5%B1%95%E5%88%86%E4%BA%AB%E3%80%82)
            - [7.1 JSP属性的复用：在配置文件web.xml中设置JSP属性，使用jsp-config标签](#71-jsp%E5%B1%9E%E6%80%A7%E7%9A%84%E5%A4%8D%E7%94%A8%EF%BC%9A%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6webxml%E4%B8%AD%E8%AE%BE%E7%BD%AEjsp%E5%B1%9E%E6%80%A7%EF%BC%8C%E4%BD%BF%E7%94%A8jsp-config%E6%A0%87%E7%AD%BE)
                - [7.1.1 匹配不同的JSP属性：jsp属性组jsp-property-group](#711-%E5%8C%B9%E9%85%8D%E4%B8%8D%E5%90%8C%E7%9A%84jsp%E5%B1%9E%E6%80%A7%EF%BC%9Ajsp%E5%B1%9E%E6%80%A7%E7%BB%84jsp-property-group)
                - [7.1.2 jsp属性](#712-jsp%E5%B1%9E%E6%80%A7)
            - [7. 将Servlet中的**请求转发**给JSP](#7-%E5%B0%86servlet%E4%B8%AD%E7%9A%84%E8%AF%B7%E6%B1%82%E8%BD%AC%E5%8F%91%E7%BB%99jsp)

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

#### 7. 将Servlet中的**请求转发**给JSP

由Sevlet处理业务逻辑以及必需的数据存储或者读取，然后创建可以由JSP轻松处理的数据模型，最终将请求转发给JSP.

请求转发与重定向的区别:重定向会改变客户浏览器的URL并且收到重定向的状态码，请求转发不会。