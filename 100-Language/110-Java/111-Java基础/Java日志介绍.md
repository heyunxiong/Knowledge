Java日志
[https://www.cnblogs.com/chenhongliang/p/5312517.html](https://www.cnblogs.com/chenhongliang/p/5312517.html)
[https://www.cnblogs.com/baizhanshi/p/7911123.html](https://www.cnblogs.com/baizhanshi/p/7911123.html)
[https://www.cnblogs.com/liufei-kuaile/p/7575779.html](https://www.cnblogs.com/liufei-kuaile/p/7575779.html)

java日志框架组合

## 两个概念

### 日志系统

日志接口的具体实现。经典的有log4j，jdk自带的有java.util.Logging，还有log4j作者推出的被高度评价的logBack等等。

### 日志接口（门面）

如果只存在一种日志系统，日志接口完全没有必要存在（logBack无法独立使用）。但事与愿违，为了解决多个日志系统的兼容问题，日志接口应运而生。主流的日志接口有commons-logging和sl4j。

## 日志框架介绍

-   Log4j(Log for Java) Apache Log4j是一个基于Java的日志记录工具。它是由Ceki Gülcü首创的，现在则是Apache软件基金会的一个项目。
    
-   Log4j 2 Apache Log4j 2是apache开发的一款Log4j的升级产品，Log4j 2 不兼容Log4j。各个方面都与Logback非常相似。
    
-   Commons Logging Apache基金会所属的项目，是一套Java日志接口，之前叫Jakarta Commons Logging，后更名为Commons Logging。
    
-   Slf4j(Simple Logging Facade for Java) 类似于Commons Logging，是一套简易Java日志门面，本身并无日志的实现。
    
-   Logback 一个“可靠、通用、快速而又灵活的Java日志框架”，属于(Slf4j阵营)
    
-   Jul(Java Util Logging) 自Java1.4以来的官方日志实现