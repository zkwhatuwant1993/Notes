# 第二部分：Web中的Spring

## 五、构造Spring web应用：Spring MVC基础

知识点：

- 映射请求到Spring控制器
- 透明地绑定表单参数
- 校验表单提交

作为企业级Java开发者，你可能开发过一些基于Web的应用程序。对于很多Java开发人员来说，基于Web的应用程序是他们主要的关注点。如果你有这方面经验的话，你会意识到这种系统所面临的挑战。具体来讲，**状态管理、工作流以及验证都是需要解决的重要特性**。HTTP协议的无状态性决定了这些问题都不那么容易解决。

Spring的Web框架就是为了帮你解决这些关注点而设计的。Spring MVC基于模型-视图-控制器（Model-View-Controller，MVC）模式实现，它能够帮你构建像Spring框架那样灵活和松耦合的Web应用程序。

下面，我们将使用Spring MVC注解来构建处理各种Web请求、参数和表单输入的控制器。

### 1. Spring MVC基础

Spring将网络请求在Spring MVC组件之间移动：DispatcherServlet、处理器、映射（handler mapping）、控制器以及视图解析器（view resolver）。

每一个Spring MVC中的组件都有特定的目的，并且它也没有那么复杂。

#### web请求在Spring mvc中的处理流程

![web请求在Spring mvc中的处理流程](https://thumbnail10.baidupcs.com/thumbnail/761bab8029a6a8c61d5d387ef9c79f3d?fid=3123715832-250528-295357327739151&rt=pr&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-gNQlniQ1IENmnzpJXD8%2bI6yDvbc%3d&expires=8h&chkbd=0&chkv=0&dp-logid=3935843383975749168&dp-callid=0&time=1529395200&size=c1440_u900&quality=90&vuk=3123715832&ft=image&autopolicy=1)一路上请求会将信息带到很多站点，并生产期望的结果。

请求旅程的第一站是Spring的DispatcherServlet。与大多数基于Java的Web框架一样，Spring MVC所有的请求都会通过一个前端控制器（front controller）Servlet。前端控制器是常用的Web应用程序模式，在这里一个单实例的Servlet将请求委托给应用程序的其他组件来执行实际的处理。在Spring MVC中，DispatcherServlet就是前端控制器。

DispatcherServlet的任务是将请求发送给Spring MVC控制器（controller）。控制器是一个用于处理请求的Spring组件。在典型的应用程序中可能会有多个控制器，DispatcherServlet需要知道应该将请求发送给哪个控制器。所以DispatcherServlet以会查询一个或多个处理器映射（handler mapping） 来确定请求的下一站在哪里。处理器映射会根据请求所携带的URL信息来进行决策。

一旦选择了合适的控制器，DispatcherServlet会将请求发送给选中的控制器。到了控制器，请求会卸下其负载（用户提交的信息）并耐心等待控制器处理这些信息。（实际上，设计良好的控制器本身只处理很少甚至不处理工作，而是将业务逻辑委托给一个或多个服务对象进行处理。）

控制器在完成逻辑处理后，通常会产生一些信息，这些信息需要返回给用户并在浏览器上显示。这些信息被称为模型（model）。不过仅仅给用户返回原始的信息是不够的——这些信息需要以用户友好的方式进行格式化，一般会是HTML。所以，信息需要发送给一个视图（view），通常会是JSP。

控制器所做的最后一件事就是将模型数据打包，并且标示出用于渲染输出的视图名。它接下来会将请求连同模型和视图名发送回DispatcherServlet 。

这样，控制器就不会与特定的视图相耦合，传递给DispatcherServlet的视图名并不直接表示某个特定的JSP。实际上，它甚至并不能确定视图就是JSP。相反，它仅仅传递了一个逻辑名称，这个名字将会用来查找产生结果的真正视图。DispatcherServlet将会使用视图解析器（view resolver） 来将逻辑视图名匹配为一个特定的视图实现，它可能是也可能不是JSP。既然DispatcherServlet已经知道由哪个视图渲染结果，那请求的任务基本上也就完成了。它的最后一站是视图的实现（可能是JSP） ，在这里它交付模型数据。请求的任务就完成了。视图将使用模型数据渲染输出，这个输出会通过响应对象传递给客户端（不会像听上去那样硬编码）。