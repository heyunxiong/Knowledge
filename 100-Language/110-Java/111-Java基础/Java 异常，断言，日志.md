> Java 基础知识： 异常、断言、日志

## 异常
@me：在程序运行的过程中，确保即使有了错误，也能有兜底的方法去处理，而不至于让机器一直无脑的跑下去。处理的方式就是告知调用者：喂。你这里有问题哦，然后给出相信的错误信息。
### Java处理异常的流程
在 Java 中， 如果某个方法不能够采用正常的途径完整它的任务，就可以通过另外一个路径退出方法。在这种情况下，方法并不返回任何值， 而是抛出( throw) 一个封装了错误信息的对象。需要注意的是，这个方法将会立刻退出，并不返回任何值。 此外， 调用这个方法的代码也将无法继续执行，取而代之的是， 异常处理机制开始搜索能够处理这种异常状况的异常处理器 （exception handler )
### 异常层次结构
![](_assets/Java%20异常，断言，日志/1636124960283-ec20d54f-0661-4535-86a5-809dd36a5720.jpeg)

### 结构解析
在 Java 程序设计语言中， 异常对象都是继承于 Throwable 的一个实例
#### Error
Error 类层次结构描述了 Java 运行时系统的内部错误和资源耗尽错误。 应用程序不应该抛出这种类型的对象。 如果出现了这样的内部错误， 除了通告给用户，并尽力使程序安全地终止之外， 再也无能为力了。这种情况很少出现
#### Exception
在设计 Java 程序时， 需要关注 Exception 层次结构。 这个层次结构又分解为两个分支：
RuntimeException 和其他异常的区别：由程序错误导致的异常属于 RuntimeException ; 而程序本身没有问题， 但由于像 I/O 错误这类问题导致的异常属于其他异常:
#### RuntimeException 
一个分支派生于 RuntimeException 如果出现 RuntimeException 异常， 那么就一定是你的问题，由程序错误导致的异常属于 RuntimeException 

- 常见的RuntimeException
   - 错误的类型转换
   - 数组访问越界
   - 访问 null 指针
#### 其他异常

- 其他异常
   - 试图在文件尾部后面读取数据
   - 试图打开一个不存在的文件
   - 试图根据给定的字符串查找 Class 对象， 而这个字符串表示的类并不存在
#### 非受查( unchecked ) 异常，受查( checked ) 异常，
J ava 语 言 规 范 将 派 生 于 Error 类 或 RuntimeException 类的所有异常称为非受查( unchecked ) 异常， 所有其他的异常称为受查（checked) 异常。继承Error类和RuntimeException类的就是非受检查异常，像什么i/o异常， FileNotFoundException, EOFException属于受检查异常
### 如何抛出异常
**
方法上声明抛出异常，使用 throws 子句

- 1 ) 调用一个抛出受査异常的方法， 例如， FilelnputStream 构造器。
- 2 ) 程序运行过程中发现错误， 并且利用 throw语句抛出一个受查异常
- 3 ) 程序出现错误， 例如，a[-l]=0 会抛出一个 ArraylndexOutOffloundsException 这样的非受查异常
- 4 ) Java 虚拟机和运行时库出现的内部错误

**2.throw 抛出一个异常实例**
如果在子类中覆盖了超类的一个方法， 子类方法中声明的受查异常不能比超类方法中声明的异常更通用， 父类的方法如果是protected级别。那么子类的方法不能是public，只能是protected，private
#### 创建异常类
创建自己的异常类就是一件顺理成章的事情了。我们需要做的只是定义一个派生于Exception 的类，或者派生于 Exception 子类的类。
```java
class FileFormatException extends IOException {
    public FileFormatException() { }
    public FileFormatException(String gripe) {
        super(gripe);
    }
}
```
#### 捕获异常

- 如果在 try语句块中的任何代码抛出了一个在 catch 子句中说明的异常类， 那么
   - 1 ) 程序将跳过 try语句块的其余代码。
   - 2 ) 程序将执行 catch 子句中的处理器代码
- 如果在 try 语句块中的代码没有拋出任何异常，那么程序将跳过 catch 子句。
- 如果方法中的任何代码拋出了一个在 catch 子句中没有声明的异常类型，那么这个方法就会立刻退出
- 请记住， 编译器严格地执行 throws 说明符。 如果调用了一个抛出受查异常的方法，就必须对它进行处理， 或者继续传递。哪种方法更好呢？ 通常， 应该捕获那些知道如何处理的异常， 而将那些不知道怎样处理的异常继续进行传递,如果想传递一个异常， 就必须在方法的首部添加一个 throws 说明符， 以便告知调用者这个方法可能会抛出异常。
### 常见的异常

- **RuntimeException**

![image.png](_assets/Java%20异常，断言，日志/1636205068873-abbbf1f9-e0ac-4c31-beeb-c748a5cbc045.png)

- **UncheckedException**

![image.png](_assets/Java%20异常，断言，日志/1636205100108-3cdd2d56-7cf1-4349-98fa-8c0fb03f7407.png)
## 断言
### 断言的作用
关键assert，在开发的过程中用到的，上线就移除了，适用于开发测试阶段，上线前移除。断言机制允许在测试期间向代码中插入一些检査语句。当代码发布时，这些插人的检测语句将会被自动地移走
### 使用方法

- assert 条件；
- assert 条件：表达式；
- 如果结果为 false, 则抛出一个 AssertionError 异常。
### 启用断言

- java -enableassertions MyApp
- 也可以在某个类或整个包中使用断言， 例如：java -ea:MyClass -eaiconi.inycompany.inylib.. , MyApp，这条命令将开启 MyClass 类以及在 com.mycompany.mylib 包和它的子包中的所有类的断言。选项 -ea 将开启默认包中的所有类的断言
- 也可以用选项 -disableassertions 或 -da 禁用某个特定类和包的断言：java -ea:... -da:MyClass MyApp
## 日志
###  java日志体系框架的历史

- 1996年，欧洲电子那帮人搞事情
- 大概是2000年左右Log4j问世，（Log for java,作者Ceki Gulcu）得到了广泛应用，几乎是java社区的日志标准，不久后（2001年1月8日），成为了Apache基金会项目成员之一，于是Apache想让jdk并入该日志框架，但被拒绝了
- 2002年4月，java1.4发布，Sun公司推出了自己的日志库JUL，java.util.logging // 就是看log4j太好了，自己照着搞出来一个，不能然log4j一家独大，毕竟java是自己家的东西。
- 2002年8月，由于JUL和log4j之间切换需要大量的代码，两者的兼容性不好。于是Apache推出了JCL接口（jakarta commons loggings，后面叫commons logging）JCL可以调用Log4j和JUL
- 2006年，Ceki Gulku不适应Apache的工作方式，离开了Apache，然后自己创建了Slf4j（日志门面接口，类似于Commons Logging）和Logback（Slf4j的实现）//它两组合是最合适的，毕竟同一个人搞出来的。
- 2012年7月，Apache眼看Log4j又被Logback反超的势头，于2012年7月重写了Log4j，成立了新的项目Log4j2，具有Logback的所有特性，Log4j2不兼容log4j
- 比较常用的组合：
   - Slf4j+Logback
   - Commons Logging+Log4j
### 日志级别
如果对 com.mycompany 日志记录器设置了日志级别，它的子记录器也会继承这个级别 ，
通常， 有以下 7 个日志记录器级别：
SEVERE，WARNING，INFO，CONFIG，FINE，FINER，FINEST
java日志框架组合
两个概念：日志系统和日志门面
### 日志系统
日志接口的具体实现。经典的有log4j，jdk自带的有java.util.Logging，还有log4j作者推出的被高度评价的logBack等等。
### 日志接口（门面）
如果只存在一种日志系统，日志接口完全没有必要存在（logBack无法独立使用）。但事与愿违，为了解决多个日志系统的兼容问题，日志接口应运而生。主流的日志接口有commons-logging和sl4j。
### 日志框架介绍
Log4j(Log for Java) Apache Log4j是一个基于Java的日志记录工具。它是由Ceki Gülcü首创的，现在则是Apache软件基金会的一个项目。
Log4j 2 Apache Log4j 2是apache开发的一款Log4j的升级产品，Log4j 2 不兼容Log4j。各个方面都与Logback非常相似。
Commons Logging Apache基金会所属的项目，是一套Java日志接口，之前叫Jakarta Commons Logging，后更名为Commons Logging。
Slf4j(Simple Logging Facade for Java) 类似于Commons Logging，是一套简易Java日志门面，本身并无日志的实现。
Logback 一个“可靠、通用、快速而又灵活的Java日志框架”，属于(Slf4j阵营)
Jul(Java Util Logging) 自Java1.4以来的官方日志实现
![image.png](_assets/Java%20异常，断言，日志/1636172980912-ae9bd563-5df6-4178-95a6-67cc126a78dc.png)


![image.png](_assets/Java%20异常，断言，日志/1636172971706-711f5e28-29aa-4e2c-bc86-faf09b4e99c3.png)

> 日志资料参考文章
[https://www.cnblogs.com/chenhongliang/p/5312517.html](https://www.cnblogs.com/chenhongliang/p/5312517.html)
[https://www.cnblogs.com/baizhanshi/p/7911123.html](https://www.cnblogs.com/baizhanshi/p/7911123.html)
[https://www.cnblogs.com/liufei-kuaile/p/7575779.html](https://www.cnblogs.com/liufei-kuaile/p/7575779.html)
> [https://www.pdai.tech/md/develop/package/dev-package-x-log.html](https://www.pdai.tech/md/develop/package/dev-package-x-log.html)
> [https://mp.weixin.qq.com/s/pdYw88oPPWCzgeeNRx0d8g](https://mp.weixin.qq.com/s/pdYw88oPPWCzgeeNRx0d8g)

