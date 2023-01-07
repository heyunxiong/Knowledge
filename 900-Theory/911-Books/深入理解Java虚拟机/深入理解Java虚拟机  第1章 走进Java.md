# 第1章 走进Java
## 1.1 概述
Java优点：
- 摆脱了平台的束缚，一次编写，到处运行
- 相对安全的内存管理和访问机制
- 热点代码检测和运行时编译
- 开源社区第三方开发类库的支持

## 1.2 Java技术体系
广义上，运行于Java虚拟机上的编程语言及其相关的程序，如Kotlin，Groovy
侠义上，JCP（Java Community Process ）官方所定义的Java技术体系：
- java程序设计语言 （语法）
- 硬件平台上的java虚拟机实现
- Class文件格式
- Java类库API（java api文档）
- 机构、开源社区的第三方java类库（apache）

Java按照功能进行划分
![Java技术体系所包括的内容](../../../100-Language/110-Java/114-Java-Wiki/_assets/Java%20Overview/image-20221016_130157684.png)
Java按照业务方向、所服务的领域划分
- Java Card：小内存设备
- Java ME：移动设备
- Java SE：桌面级应用，提供完整api
- Java EE：企业级应用，扩展性强（JDK10后，Oracle捐给了Eclipse基金会，此后被称为Jakarta EE）

## 1.3 Java发展史
创始人：James Gosling博士
- 1995年5月23日，java 1.0发布
- 1996年1月23日，JDK 1.0 发布，第一个正式版本的运行环境
- 2014年3月18日，JDK 8.0发布

## 1.4 Java虚拟机家族
### 1.4.1 虚拟机始祖：Sun Classic/Extract VM

### 1.4.2* HotSpot VM
默认的Java虚拟机，使用范围最广的虚拟机

### 1.4.3 Mobile/Embedded VM
面向移动和嵌入式方向的java虚拟机

### 1.4.4 BEA JRockit/IBM J9 VM
BEA System公司的 JRockit，IBM公司的IBM J9，跟HotSpot三分天下

### 1.4.5 BEA Liquid VM/ Azul VM
特定硬件平台也有专门的虚拟机，代表：BEA Liquid VM/ Azul VM

其他虚拟机。。。

## 1.5 Java技术未来
庞大的用户群和及其成熟的软件生态，朝夕之间难以撼动
### 1.5.1 打破语言壁垒
Oracle labs下的Graal VM被官方称为：universal vm和polyglot vm，在hotspot基础上增强而成的跨语言全栈虚拟机，可以作为“任何语言”的运行平台使用。
### 1.5.2 新一代即时编译器
对于长时间运行的应用来说，由于经过充分预热，热点代码会被hotspot的探测机制准确定位捕获，并将其编译为物理硬件可直接执行的机器码。
HotSpot中有两个即时编译器，1.编译耗时短但输出代码优化程度低的客户端编译器（C1）2.编译耗时长但输出代码优化质量高的服务端编译器（C2）
现在Oracle加入了一个全新的即时编译器：Graal编译器，准备替代C2，未来可期。

。。。。
剩下的不感兴趣，不记录了。
。。。。

2022年10月17日
Yunxiong

## Open JDK 和 Oracle JDK 的区别
![](_assets/深入理解Java虚拟机%20%20第1章%20走进Java/image-深入理解Java虚拟机%20%20第1章%20走进Java-20221017-210918752.png)
## Open JDK版本关系
![](_assets/深入理解Java虚拟机%20%20第1章%20走进Java/image-深入理解Java虚拟机%20%20第1章%20走进Java-20221017-210941146.png)

