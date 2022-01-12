> 记录Java语言中遇到的术语缩写。

| **缩写** | **全称** | **中文解释** |
| :---: | :---: | :---: |
| JDK | Java Development Kit | java开发工具箱 |
| JRE |  Java Runtime Environment | java运行时环境 |
| JSR | Java Specification Request | java规范请求，每个版本都会对应一个JSR |
| JEP | Java Enhancement Proposal | java增强请求，通过的请求会归入到JSR中 |
| SDK | dk, Development Kit |  至于S。 目前不太清楚什么意思，如果是针对java的话，应该就是 SE。 和JDK 同一个意思，难道software？ |
| RMI | Remote Method Invocation | 远程方法调用 |
| JMS | Java Messaging Service | java消息服务 |
| JNDI | Java Naming and Directory interface | java命名目录接口 |

关于RMI，java api包下有一个对应独立的包(java.rmi.)，其描述为：提供RMI包。 
**RMI是远程方法调用。 **

- 这是一种使一个Java虚拟机上的对象能够调用另一个Java虚拟机中对象的方法的机制。 可以以这种方式调用的任何对象都必须实现Remote接口。 
- 当调用这样一个对象时，它的参数是“marshalled”，并从本地虚拟机发送到远程对象，其中参数是“未编组的”。当方法终止时，结果从远程机器编组并发送给呼叫者的虚拟机。 如果方法调用导致抛出异常，则会向调用者指示异常。



