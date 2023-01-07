> Web Knowledge： Servlet Overview

## 什么是Servlet ?
> Java Servlet technology provides Web developers with a simple, consistent mechanism for extending the functionality of a Web server and for accessing existing business systems. A servlet can almost be thought of as an applet that runs on the server side--without a face. Java servlets make many Web applications possible.
> 「[official ](https://www.oracle.com/java/technologies/java-servlet-tec.html)」

Servlet（Server Applet），全称 Java Server Applet；是用Java编写的服务器端程序；主要功能在于交互式地浏览和修改数据，生成动态Web内容。
狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。「[link](https://zh.wikipedia.org/wiki/Java_Servlet)」
Servlet相关的包：**javax.servlet，javax.servlet.http，javax.servlet.annotation 和 javax.servlet.descriptor**
Servlet 运行在应用服务器(Servlet容器)中：比如Tomcat。
## Servlet 接口
Servlet接口是所有Servlet类必须直接或者间接实现的一个接口；
```java
// Defines methods that all servlets must implement.
public interface Servlet{....}
```
Servlet接口中定了5个方法：

- **void  init(ServletConfig config)**

Called by the servlet container to indicate to a servlet that the servlet is being placed into service.

- **void  service(ServletRequest req, ServletResponse res)**

Called by the servlet container to allow the servlet to respond to a request.

- **void  destroy( )**

Called by the servlet container to indicate to a servlet that the servlet is being taken out of service.

- **ServletConfig  getServletConfig( )**

Returns a ServletConfig object, which contains initialization and startup parameters for this servlet.

- **String  getServletInfo( )**

Returns information about the servlet, such as author, version, and copyright.
其中init、service、destroy是Servlet生命周期方法。

- init方法第一次请求Servlet的时候调用，此后不会调用。
- service方法每次请求都会调用
- destroy方法，当要销毁Servlet的时候，Servlet容器（Tomcat）会调用这个方法

Servlet中重要的几个对象
ServletRequest、ServletResponse、ServletConfig、ServletContext
## GenericServlet
实现了Servlet接口，直接实现Servlet接口需要实现全部方法，通过GenericServlet可以减少
```java
public abstract class GenericServlet implements Servlet, ServletConfig, Serializable
```
## 💥HttpServlet
**javax.servlet.http**
针对Http的请求的Servlet，间接实现了Servlet接口，而且相对应的重要对象都带有Http前缀。
```java
public abstract class HttpServlet extends GenericServlet
```
HttpServlet会重写Servlet接口中service方法，然后调用自己新的service方法，该方法接受HttpServletRequest和HttpServletResponse对象
```java
@Override
public void service(ServletRequest req, ServletResponse res) 
												throws ServletException, IOException{
    HttpServletRequest  request;
    HttpServletResponse response;
    
    if (!(req instanceof HttpServletRequest &&
            res instanceof HttpServletResponse)) {
        throw new ServletException("non-HTTP request or response");
    }

    request = (HttpServletRequest) req;
    response = (HttpServletResponse) res;

    service(request, response); //HttpServlet内置重载方法
}
}
```
HttpServlet用来处理HTTP请求，也即系目前我们常用的，需要继承该类编写自己的Servlet。
每种方法都对应着HTTP的请求方法

- doGet( ) , if the servlet supports HTTP GET requests
- doPost( ) , for HTTP POST requests
- doPut( ) , for HTTP PUT requests
- doDelete( ) , for HTTP DELETE requests
- init( ) and destroy( ), to manage resources that are held for the life of the servlet
- getServletInfo( ), which the servlet uses to provide information about itself
## 使用HttpServlet
使用HttpServlet不用覆盖service方法，而是覆盖doGet或者doPost方法
```java
public class MyServlet extends HttpServlet {
  doGet(HttpServletRequest request, HttpServletResponse response){...}
  doPost(HttpServletRequest request,HttpServletResponse response){....}
}
```
## @WebServlet注解
从Servlet3.0开始，配置Servlet支持注解方式，例如：@WebServlet、@WebInitParm 、@WebFilter 和 @WebLitener 等，但还是保留了配置web.xml方式。

- Servlet类上使用@WebServlet注解进行配置
- web.xml文件中配置

@WebServlet常用属性

| 属性名 | 类型 | 标签 | 描述 | 是否必需 |
| --- | --- | --- | --- | --- |
| name | String | <servlet-name> | 指定 Servlet 的 name 属性。如果没有显式指定，则取值为该 Servlet 的完全限定名，即包名+类名。 | 否 |
| value | String[ ] | <url-pattern> | 该属性等价于 urlPatterns 属性，两者不能同时指定。如果同时指定，通常是忽略 value 的取值。 | 是 |
| urlPatterns | String[ ] | <url-pattern> | 指定一组 Servlet 的 URL 匹配模式。 | 是 |
| loadOnStartup | int | <load-on-startup> | 指定 Servlet 的加载顺序。 | 否 |
| initParams | WebInitParam[ ] | <init-param> | 指定一组 Servlet 初始化参数。 | 否 |
| asyncSupported | boolean | <async-supported> | 声明 Servlet 是否支持异步操作模式。 | 否 |
| description | String | <description> | 指定该 Servlet 的描述信息。 | 否 |
| displayName | String | <display-name> | 指定该 Servlet 的显示名。 | 否 |

1. 启用@WebServlet
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://xmlns.jcp.org/xml/ns/javaee"
    xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
    id="WebApp_ID" metadata-complete="false" version="4.0">
    <!-- metadata-complete取值为true，表示关闭注解支持 -->
    <!-- metadata-complete取值为false，表示启用注解支持 -->
</web-app>
```

2. 使用@WebServlet

loadOnStartup的启动顺序，值越小，servlet的优先级越高，就越先被加载
```java
@WebServlet(asyncSupported = true, 
            name = "myServlet", 
            description = "name描述", 
            loadOnStartup = 1, 
            urlPatterns = {"/MyServlet", "/*" }, 
  					initParams = {
						@WebInitParam(name = "abc", value = "www.123.net", description = "init参数1"),
						@WebInitParam(name = "xyz", value = "www.456.com", description = "init参数2") }
           )
public class MyServlet extends HttpServlet {
  ....
  }
```
参考资料：

- [https://www.oracle.com/java/technologies/java-servlet-tec.html](https://www.oracle.com/java/technologies/java-servlet-tec.html)
- [https://zh.wikipedia.org/wiki/Java_Servlet](https://zh.wikipedia.org/wiki/Java_Servlet)
- [https://www.w3cschool.cn/servlet/](https://www.w3cschool.cn/servlet/)
- [http://c.biancheng.net/servlet2/webservlet.html](http://c.biancheng.net/servlet2/webservlet.html)
