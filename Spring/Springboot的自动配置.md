

# Springboot的自动配置

## 自动配置 Tomcat

引入依赖

spring-boot-starter-web里面就引用了tomcat的依赖，所以在我们的pom.xml就可以不需要配置Tomcat

~~~xml
	<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.4.8</version>
      <scope>compile</scope>
    </dependency>
~~~

自动配置

## 自动配置 SpringMVC

同理

~~~xml
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.3.8</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.8</version>
      <scope>compile</scope>
    </dependency>
~~~

springmvc的相关配置已经配好了





主程序DemoApplocatijon.java要所在的包及其子包都会被扫描到。







@Configuration 

proxyBeanMethod的用法

full proxyBeanMethod =true

lite proxyBeanMethod=false





