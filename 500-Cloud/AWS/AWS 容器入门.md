## AWS 容器入门

视频地址：https://study.163.com/course/courseMain.htm?courseId=1212169804

容器的历史

容器的术语

容器和虚拟机的区别

为什么要使用容器





## 什么是容器

容器的历史

现实例子：

以前，人们使用航海运行的时候，转载的货物各异，能放稳的不能放稳的，意碎的，易腐烂的，大的小的等等，这种不规则的货物，使得船只无法预测能装多少货物。

直到后来，利用集装箱，船只只针对集装箱进行装卸载，而不是关注单个货物，效率提高了。

而且规范的集装箱有利于火车，货车，船只的设计

在计算平台，引用了实际例子，真所谓，艺术源自生活。

容器是一种标准化软件单元

![image-20211212142535063](_assets/AWS%20容器入门/image-20211212142535063.png)

容器是独立的轻量级软件包，其中包括运行程序所需的一切：代码，运行时环境。系统工具、设置等

![image-20211212142725128](_assets/AWS%20容器入门/image-20211212142725128.png)



虚拟化和抽象

![image-20211212142952713](_assets/AWS%20容器入门/image-20211212142952713.png)



docker作为虚拟化平台。

![image-20211212143055416](_assets/AWS%20容器入门/image-20211212143055416.png)



![image-20211212143126638](C:\Users\heyunxiong\AppData\Roaming\Typora\typora-user-images\image-20211212143126638.png)



![image-20211212143217407](_assets/AWS%20容器入门/image-20211212143217407.png)



使用dockerfile创建镜像

![image-20211212143422915](_assets/AWS%20容器入门/image-20211212143422915.png)



镜像与容器的关系

![image-20211212143540436](_assets/AWS%20容器入门/image-20211212143540436.png)



把容器看做是计算单元，而不是存储单元，持久化的数据需要挂载卷存储。

容器与微服务

容器的发展离不开微服务的高速发展

传统与微服务

![image-20211212143935343](_assets/AWS%20容器入门/image-20211212143935343-16392923331892.png)





![image-20211212144150553](_assets/AWS%20容器入门/image-20211212144150553-16392923281901.png)



