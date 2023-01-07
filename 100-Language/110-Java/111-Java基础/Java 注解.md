> Java 基础知识： Java注解

## 什么是Java注解？
jdk5 引入的东西，给程序看的。
## 注解的作用

- 注解不是程序，对程序加以解释
- 可以被编译器读取，让程序知道这代码用来干嘛的。
## Java 内置注解
常见的几个
### @Override
定义在java.lang.Override中，此注释只能修饰方法，表示重写父类的方法
### @Deprecated
定义在java.lang.Deprecated中，可以修饰属性，方法，类；表示此方法已经过时，不鼓励使用（有安全性的考虑），但仍可以使用，往往有其替代的方法。
### @SuppressWarnings
定义在java.lang.SuppressWarnings中，用来抑制编译时的警告信息。

   - @SuppressWarnings("all")
   - @SuppressWarnings("unchecked")
   - @SuppressWarnings(value={"unchecked","deprecation"})
## Java 元注解
jdk 1.5 规定的四个标准 meta-annotation：@Target, @Retention, @Documented, @Inherited
jdk 1.7 添加了三个额外的注解：@SafeVarargs，@FunctionalInterface， @Repeatable 
### @Target
**@Target  表示注解适用的范围，即该注解可以被用在什么地方**
```java
@Target (ElementType.TYPE)
public @interface Table{
	public String tableName() default "className";
}
```
取值：
ElementType 中的值

- CONSTRUCTOR:    		  用于描述构造器
- FIELD:                    		  用于描述域
- LOCAL_VARIABLE: 		  用于描述局部变量
- METHOD:             		  用于描述方法
- PACKAGE:             		  用于描述包
- PARAMETER:         		  用于描述参数
- TYPE:                    		  用于描述类、接口(包括注解类型) 或enum声明
### @Retention
**@Retention 表示注解的保留时间，即该annotation的生命周期**

- SOURCE:      在源文件中有效（即源文件保留）
- CLASS:         在class文件中有效（即class保留）
- RUNTIME:    在运行时有效（即运行时保留）
### @Document
**@Documented 表示是否能被javadoc等工具类形成文档**
### @Inherited
**@Inherited 表示该注解的被标记的类型能被继承**

**jdk1.7后添加的：**
### @SafeVarargs
@SafeVarargs ：在声明可变参数的构造函数或⽅法时，Java 编译器会报 unchecked 警告。使⽤ @SafeVarargs 可以忽略这些警告
### @FunctionalInterface
@FunctionalInterface : 表明这个⽅法是⼀个函数式接⼝
### @Repeatable
@Repeatable ： 标识某注解可以在同⼀个声明上使⽤多次
## 自定义注解
**定义注解格式： **
```java
public @interface 注解名 {  
	定义体  
}
```
**注解参数的可支持数据类型：**

- 所有基本数据类型（int,float,boolean,byte,double,char,long,short)
- String 类型
- Class 类型
- enum 类型
- Annotation 类型
- 以上所有类型的数组
## 参考链接
[https://www.cnblogs.com/peida/archive/2013/04/24/3036689.html](https://www.cnblogs.com/peida/archive/2013/04/24/3036689.html)
