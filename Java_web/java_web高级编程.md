# Java Web高级编程学习笔记

- [Java Web高级编程学习笔记](#java-web%E9%AB%98%E7%BA%A7%E7%BC%96%E7%A8%8B%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0)
    - [一、Java EE相关概念](#%E4%B8%80%E3%80%81java-ee%E7%9B%B8%E5%85%B3%E6%A6%82%E5%BF%B5)
        - [1. JavaEE平台规范：Servlet,过滤器，jsp,JUEL等等组件的标准。](#1-javaee%E5%B9%B3%E5%8F%B0%E8%A7%84%E8%8C%83%EF%BC%9Aservlet%E8%BF%87%E6%BB%A4%E5%99%A8%EF%BC%8Cjspjuel%E7%AD%89%E7%AD%89%E7%BB%84%E4%BB%B6%E7%9A%84%E6%A0%87%E5%87%86%E3%80%82)
        - [2. web容器/servlet容器](#2-web%E5%AE%B9%E5%99%A8servlet%E5%AE%B9%E5%99%A8)
    - [二、Servlet类](#%E4%BA%8C%E3%80%81servlet%E7%B1%BB)
        - [1. 创建Servlet类](#1-%E5%88%9B%E5%BB%BAservlet%E7%B1%BB)
            - [1. Servlet类的体系结构。](#1-servlet%E7%B1%BB%E7%9A%84%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84%E3%80%82)
            - [2. 处理HTTP请求](#2-%E5%A4%84%E7%90%86http%E8%AF%B7%E6%B1%82)
            - [3. 初始化和销毁:Servlet的生命周期](#3-%E5%88%9D%E5%A7%8B%E5%8C%96%E5%92%8C%E9%94%80%E6%AF%81servlet%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
        - [2. 配置可部署的Servlet：web.xml](#2-%E9%85%8D%E7%BD%AE%E5%8F%AF%E9%83%A8%E7%BD%B2%E7%9A%84servlet%EF%BC%9Awebxml)
            - [1. 配置Servlet:Servlet标签](#1-%E9%85%8D%E7%BD%AEservletservlet%E6%A0%87%E7%AD%BE)
            - [2. 将Servlet映射到URL:Servlet-mapping标签](#2-%E5%B0%86servlet%E6%98%A0%E5%B0%84%E5%88%B0urlservlet-mapping%E6%A0%87%E7%AD%BE)
        - [3. 了解doGet，doPost和其他方法](#3-%E4%BA%86%E8%A7%A3doget%EF%BC%8Cdopost%E5%92%8C%E5%85%B6%E4%BB%96%E6%96%B9%E6%B3%95)
            - [1. service方法](#1-service%E6%96%B9%E6%B3%95)
            - [2. HttpServletRequest接口](#2-httpservletrequest%E6%8E%A5%E5%8F%A3)
                - [1. 获取请求参数](#1-%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
                - [2. 确定与请求内容（请求正文）相关信息:getContentXXX()方法](#2-%E7%A1%AE%E5%AE%9A%E4%B8%8E%E8%AF%B7%E6%B1%82%E5%86%85%E5%AE%B9%EF%BC%88%E8%AF%B7%E6%B1%82%E6%AD%A3%E6%96%87%EF%BC%89%E7%9B%B8%E5%85%B3%E4%BF%A1%E6%81%AFgetcontentxxx%E6%96%B9%E6%B3%95)
                - [3. 获取请求正文:使用getInputStream或getReader。](#3-%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E6%AD%A3%E6%96%87%E4%BD%BF%E7%94%A8getinputstream%E6%88%96getreader%E3%80%82)
                - [4. 获取Http请求特有的数据URL,URI,和头信息](#4-%E8%8E%B7%E5%8F%96http%E8%AF%B7%E6%B1%82%E7%89%B9%E6%9C%89%E7%9A%84%E6%95%B0%E6%8D%AEurluri%E5%92%8C%E5%A4%B4%E4%BF%A1%E6%81%AF)
                - [5.会话和Cookies](#5%E4%BC%9A%E8%AF%9D%E5%92%8Ccookies)
            - [3. 使用HttpServletResonse](#3-%E4%BD%BF%E7%94%A8httpservletresonse)
                - [1. 编写响应正文](#1-%E7%BC%96%E5%86%99%E5%93%8D%E5%BA%94%E6%AD%A3%E6%96%87)
                - [2. 设置头和其他response属性](#2-%E8%AE%BE%E7%BD%AE%E5%A4%B4%E5%92%8C%E5%85%B6%E4%BB%96response%E5%B1%9E%E6%80%A7)
            - [4.使用初始化参数配置应用程序](#4%E4%BD%BF%E7%94%A8%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%82%E6%95%B0%E9%85%8D%E7%BD%AE%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)
                - [1. 使用Context初始化参数](#1-%E4%BD%BF%E7%94%A8context%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%82%E6%95%B0)
                - [2. 使用Servlet初始化参数](#2-%E4%BD%BF%E7%94%A8servlet%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%82%E6%95%B0)

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

#### 1. Servlet类的体系结构。

1. Servlet接口:定义了初始化,销毁Servlet和请求的方法。
2. GnericServlet implements Servlet：抽象类，一个不依赖协议的Servlet,定义了一个service方法，用于接收和响应客户端请求。还包含一些辅助方法：日志操作，从应用中获取Servlet的配置信息等。
3. 4.HttpServlet extends GnericServlet：实现了接收http请求的service方法.并且提供了响应每种Http方法类型的空实现。GET,HEAD,POST,PUT,DELETE,OPTIONS,TRACE

#### 2. 处理HTTP请求

doGet,doPost方法：Web容器将会处理请求的解释，并从socket中读取请求头和参数。在Servlet的方法返回之后，Web容器还将格式化响应头和主体，并写回到socket中。
参数HttpServletRequest和HttpServletResponse

#### 3. 初始化和销毁:Servlet的生命周期

init()方法：在Servlet启动时调用(在Servlet构造完成后，且在响应一第一请求前调用;如果将该Servlet配置为web应用程序部署和启动时自动启动，那么此方法也会调用).调用init方法时，Servlet中的所有属性都有设置完成，并提供对ServletConfig和ServletContext的访问。
destory()方法:在Servlet不再接收请求后立即调用（通常发生在web应用程序被停止或者卸载，或者web容器关闭时）

### 2. 配置可部署的Servlet：web.xml

Servlet部署描述文件:WEB-INFO/web.xml

#### 1. 配置Servlet:Servlet标签

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

#### 2. 将Servlet映射到URL:Servlet-mapping标签

1. 使用web.xml设置
    ```xml
    <!-- 告诉web容器如何创建该Servlet-->
    <Serlvet-mapping>
    <!--指定Servlet的名字，与<Servlet>标签下的<Servlet-name>标签对应-->
    <!-- 表示映射的是哪个Servlet -->
    <Servlet-name>name</Servlet-name>
    <!-- 访问该web应用的相对URL/path的请求将由该Servlet处理-->
    <url-pattern>/path1</url-pattern>
    <!-- 可以将多个url映射到同一个Servlet-->
    <url-pattern>/path2</url-pattern>
    <url-pattern>/path3</url-pattern>
    </Serlvet-mapping>
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

#### 1. service方法

Servlet类的service方法将会处理所有到达的请求,然后根据所使用的协议(如HttServlet使用的http协议)解析并处理（调用doGet，doPost或其他方法）请求中的数据,然后返回客户端可接受的响应(符合协议).

#### 2. HttpServletRequest接口

Extends the ServletRequest interface to provide request information for HTTP servlets.
扩展自ServletRequest接口来提供收到请求的额外的与HTTP协议相关的信息。它定义了多个可以获得HTTP请求详细信息的相关方法.它也允许设置**请求特性**。

The servlet container creates an HttpServletRequest object and passes it as an argument to the servlet's service methods (doGet, doPost, etc).
Servlet容器创建一个HttpServletRequest的实例并将该对象做为参数传给该servlet的service方法。

##### 1. 获取请求参数

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

##### 2. 确定与请求内容（请求正文）相关信息:getContentXXX()方法

##### 3. 获取请求正文:使用getInputStream或getReader。

    注意：不要在同一个reqeust对象上同时使用这两个方法，会抛出抛出IllegalStateException.因为该流只能读取一次。

##### 4. 获取Http请求特有的数据URL,URI,和头信息

    - getRequestURL
    - getRequestURI
    - getServletPath
    - getHeaderXXX

##### 5.会话和Cookies

    - getSession
    - getCookies

#### 3. 使用HttpServletResonse

使用该对象可以完成设置响应头、响应正文、重写向请求、响应状态码以及将cookies返回到客户端等任务。

##### 1. 编写响应正文

1. 使用getOutPutStream或getWriter
2. 设置内容类型和编码格式:setContentTypep和setCharacterEncoding.

注意：如何要设置内容类型和编码格式，必须在getOutputStrem或getWriter之前设置，否则将使用web容器的默认编码返回输出流.

##### 2. 设置头和其他response属性

    - setHeaderXXX()
    - setStatus
    - sendError
    - sendRedirect

#### 4.使用初始化参数配置应用程序

##### 1. 使用Context初始化参数

1. 在web.xml中配置Context参数
    ```xml
    <Context-param>
        <param-name></param-name>
        <param-value></param-value>
    </Context-param>
    ```
    应用程序中的所有Servlet都共享这些数据。

2. 在Servlet中获取
    ```java
        ServletContext context = this.getServletContext();
        context.getInitParameter();
    ```

##### 2. 使用Servlet初始化参数

1. 在web.xml中配置Servlet初始化参数
    ```xml
    <Servlet>
        <Servlet-name></Servlet-name>
        <Servlet-class></Servlet-class>
    </Servlet>
    <init-param>
            <param-name>p1</param-name>
            <param-value>v1</param-value>
        </init-param>
    <init-param>
        <param-name>p1</param-name>
        <param-value>v1</param-value>
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