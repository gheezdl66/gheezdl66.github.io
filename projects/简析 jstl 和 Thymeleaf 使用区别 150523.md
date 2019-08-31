### 简析 jstl 、JSP、servlet、 Thymeleaf 联系

#### 1. [jstl](JSP标准标签库，是JSP标签的集合，封装了很多JSP应用程序的核心功能)

> [**1.1 安装使用**](在JSP)

#### 2. [jsp](元素+模板 组成)

> [**2.1 概念：**](Myeclipse项目结构一般将css、images、admin（后台管理页面）、pages（主页面）等文件夹放在Webroot目录下) 建立在servlet规范功能上的动态网页技术，在网页中嵌入Java代码，和 JSP 标记产生动态内容
>
> **2.2 三元素：**
>
> * 2.2.1 [*指令元素：*](page指令、include指令、taglib指令)
>
>   > [page]( * 标注常用)
>   >
>   > ```
>   > <%@ page 
>   >   ** language="java"   //指定在脚本元素中使用的脚本语言
>   >   ** import="com.test.Person" //指定在脚本环境下可以使用的类
>   >      extends="className"  //指定JSP页面转换后的Servlet类从哪一个类继承
>   >      session="true"     //指定页面是否参加到HTTP会话中，若为true则在JSP页面中可以使用隐含的session对象
>   >      buffer="none"      //指定out对象使用的缓冲区大小    
>   >      autoFlush="true"     //指定当缓冲区慢的时候，缓存的输出是否应该自动刷新
>   >      isThreadSafe="true"//指定对JSP页面的访问是否是线程安全的
>   >      info="info_text"    //指定页面的相关信息
>   >      errorPage="error_url"  //指定当JSP页面发生异常时，将转向哪一个错误处理页面
>   >      isErrorPage="false"   //指定当前的页面是否是另一个页面的错误处理页面
>   >   ** contentType="text/html; charset=ISO-8859-1" //指定相应页面的MIME类型和字符编码
>   >   ** pageEncoding="ISO-8859-1" 指定页面使用的字符编码，如果设置了该属性，则页面使用该属性指定字符集，没有设置则使用contextType属性指定的字符集
>   >      isErrorPage="false"    //定义在JSP页面中是否执行或忽略EL表达式
>   >      deferredSyntaxAllowedAsLiteral="false"    //指示在JSP页面的模板文本中是否允许出现字符序列
>   >      trimDirectiveWhitespaces="false" //指示模板中的空白怎么处理
>   > %>
>   > ```
>   >
>   > include
>   >
>   > ```
>   > 用于在JSP页面中静态包含一个文件，可以是JSP页面、HTML网页、文本文件或一段Java代码
>   > <%@ include file="date.jsp" %>
>   > ```
>   >
>   > taglib
>   >
>   > ```
>   > 允许页面使用用户定制标签
>   > ```
>
> * 2.2.2 [*脚本元素：*](声明+脚本段+表达式)
>
>   > [声明](声明jsp页面的脚本语言中的变量和方法)
>   >
>   > ```
>   > <%!  %>:内的变量和方法是同一个 类 的变量和方法，即成员变量和成员方法--->可以声明方法
>   > <%   %>:内的变量是 方法 的变量，即局部变量                       --->不可以声明方法
>   > ```
>   >
>   > [脚本段](请求处理期间要执行的Java代码段)
>   >
>   > ```
>   > <html>
>   >     <head>
>   >     <title>Hello JSP</title>
>   >     </head>
>   >     <body>
>   >         <%out.write("hello world!"); %>
>   >     </body>
>   > </html>
>   > ```
>   >
>   > [表达式](是Java语言中完整的表达式，在请求处理时计算这些表达式，计算的结果将被转换为字符串，插入到输出流中)
>   >
>   > ```
>   > <%@ page import="java.util.Date" contentType="text/html; charset=UTF-8"%>
>   > <html>
>   >     <head>
>   >     <title>Hello JSP</title>
>   >     </head>
>   >     <body>
>   >         现在的时间：<%= new Date().toLocaleString() %>
>   >     </body>
>   > </html>
>   > ```
>
> * 2.2.3[*动作元素：*](规范定义20个标准动作元素)
>
> **2.3 jsp 九大内置对象**
>
> ```HTML
> out、request √、response √、session √、application √ |config、pageContext、page、Exception
> ```
>
> **2.4 保存数据的几大对象**
>
> ```
> Application(存货周期最长)、session、request、pageContext(存货周期最短)、cookie（保存在客户端）
> ```
>
> **2.5 客户端请求新页面方式**
>
> ```
> 1>超链接
> 2>超链接+js
> 3>submit提交表单
> 4>使用js提交表单
> 5>关于乱码（web.xml添加过滤器的可能）
> ```
>
> **2.6 页面组成**
>
> ```
> 1>指令元素
> 2>HTML标签 
> 3>CSS
> 4>JavaScript
> 5>Java小脚本(脚本元素)
> ```
>
> 

#### 3. [servlet](由JVM的垃圾回收器进行回收)

> **3.1. http请求类型：**
>
> Get、Post、Put、Delete
>
> [**3.2 生命周期**](Server Applet，小服务程序或服务连接器，用Java编写的服务器端程序，主要功能在于交互式地浏览和修改数据，生成动态Web内容)
>
> [init()](最开始并只创建一次，创建加载一些数据用于整个servlet生命周期)===》[重写doGet/doPost()]()===》[destroy()](和init()方法一样只调用一次，使servlet关闭数据库连接，停止后台进程，将cookie列表和点击计数器写入磁盘)===》[JVM对servlet进行回收](destroy()调用完后servlet对象被标记为垃圾回收等待JVM垃圾回收器进行回收)
>
> ```
> //全部根据传入的参数来执行响应操作，一般是get接受服务器请求，post对请求发出响应
> public void doGet(HttpServletRequest request,
>                   HttpServletResponse response)
>     throws ServletException, IOException {
>     // Servlet 代码
> }
>
> public void doPost(HttpServletRequest request,
>                    HttpServletResponse response)
>     throws ServletException, IOException {
>     // Servlet 代码
> }
> ```
>
> **3.3 servlet 部署**
>
> > 在web.xml文件中部署servlet对象，使web.xml文件在加载时使自定义 servlet或默认DispatcherServlet加载进去
>
> ```
> <?xml version="1.0" encoding="UTF-8"?>
> <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>     xmlns="http://xmlns.jcp.org/xml/ns/javaee"
>     xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
>     id="WebApp_ID" version="3.1">
>     <display-name>WeixinDFF</display-name>
>     <welcome-file-list>
>         <welcome-file>index.html</welcome-file>
>         <welcome-file>index.jsp</welcome-file>
>         <welcome-file>default.html</welcome-file>
>         <welcome-file>default.jsp</welcome-file>
>     </welcome-file-list>
>     <servlet>
>         <servlet-name>coreServlet</servlet-name>
>         <servlet-class>com.dff.weixin.servlet</servlet-class>
>     </servlet>
>     
>     <servlet-mapping>
>         <servlet-name>coreServlet</servlet-name>
>         <url-pattern>/coreServlet</url-pattern>
>     </servlet-mapping>
> </web-app>
> ```
>
> [**3.4 ServletConfig // ServletContext**](使用<init-param>子元素将初始化参数名和参数值传递给Servlet，访问Servlet配置参数通过ServletConfig对象完成)
>
> 前者：获取 ***当前Servlet*** 配置参数
>
> 后者：获取 ***整个web应用*** 的配置参数
>
> ```
> 参数说明：@ 必须参数, ^ 非必须参数
> <servlet>@                                 // 一般servlet和servlet-mapping成对存在
>     <servlet-name>@，定义Servlet名称，在整个web应用中唯一</servlet-name>
>     <serlvet-class>@，指定Servlet完全限定名称，即包名</servlet-class>
>     <jsp-file>^，指定应用中JSP文件完整路径，由 / 开始</jsp-file>
>     <init-param>  
>       <param-name>publishContext</param-name>  
>       <param-value>false</param-value>  
>     </init-param>  
>     <load-on-startup>1</load-on-startup>
> </servlet>
> <servlet-mapping>@, 将URL模式映射到某个servlet
>     <servlet-name>@，对应上面的servlet-name</servlet-name>
>     <url-pattern>@, 映射路径，指定相对于servlet的URL路径，
>                   该路径相对于web应用的上下文的根路径</url-pattern>
> </servlet-mapping>
> <description>：^                         //为Servlet指定一个文本描述。
> <display-name>：^                        //为Servlet提供一个简短的名字被某些工具显示。
> <icon>：^                          //为Servlet指定一个图标，在图形管理工具中表示该Servlet。
> ```

#### 4. [Thymeleaf](是一个跟 Velocity、FreeMarker 类似的模板引擎，可以完全替代 JSP )

> 

#### 5. jstl与jsp及servlet版本之间  的关系

> ![1565657741019](F:\桌面\mkd\pics\1565657741019.png)





