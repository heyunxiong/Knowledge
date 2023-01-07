> Web Knowledge： Tomcat 汤姆猫服务器

![](_assets/Web%20Server%20-%20Tomcat/1637568700607-3ee5425c-7608-4e83-b60c-e1c6ec5f3164.png)
## Tomcat 概述
>  This is the top-level entry point of the documentation bundle for the Apache Tomcat Servlet/JSP container. Apache Tomcat version 8.0 implements the Servlet 3.1 and JavaServer Pages 2.3 [specifications](https://wiki.apache.org/tomcat/Specifications) from the [Java Community Process](https://www.jcp.org/), and includes many additional features that make it a useful platform for developing and deploying web applications and web services.

Tomcat是一种开源的web应用服务器，主要用来运行java web应用程序，即系Servlet容器。
实现了对Servlet和JavaServer Page（JSP）的支持，并提供了作为Web服务器的一些特有功能。

> Tomcat 是一个「Application Server」，或者更准确的来说，是一个「Servlet/JSP」应用的容器（Ruby/Python 等其他语言开发的应用也无法直接运行在 Tomcat 上）。

**目前常见的web应用服务器**
![](_assets/Web%20Server%20-%20Tomcat/1637569335273-3546d21b-0ee2-47b5-9c46-e0291fb48871.webp)
Tomcat 和 Jetty 都只提供了 Java Web 容器必需的 Servlet 和 JSP 规范，开发者要想实现其他的功能，需要自己依赖其他开源实现
Websphere 来自IBM提供的web服务器，功能强大，但笨重。

## Tomcat 目录
Tomcat 根目录
![image.png](_assets/Web%20Server%20-%20Tomcat/1637569509264-27cd47d2-864a-47e9-9d92-9ddb67b2b6b3.png)

| 目录 | 说明 |
| --- | --- |
| bin | 启动和关闭tomcat的bat文件 |
| conf | 存放配置文件 |
| conf/server.xml | 该文件用于配置server相关的信息，比如tomcat启动的端口号，配置主机(Host) |
| conf/web.xml | 配置与web应用（web应用相当于一个web站点） |
| conf/tomcat-user.xml | 配置用户名密码和相关权限 |
| lib | 该目录放置运行tomcat运行需要的jar包 |
| logs | 存放日志，当我们需要查看日志的时候，可以查询信息 |
| temp | 临时文件 |
| webapps | 放置我们的web应用 |
| work		 | 工作目录，该目录用于存放jsp被访问后生成对应的server文件和.class文件 |

## Tomcat 容器架构
![](_assets/Web%20Server%20-%20Tomcat/1637571200591-025c315b-f9d4-49f2-beb1-46558b5a04c7.webp)
## Tomcat 启动过程
## Tomcat 请求处理
## Tomcat 应用部署

参考资料

- 

