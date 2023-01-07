什么是seata？ 
[cnblogs.com/lay2017/p/12207951.html](https://www.cnblogs.com/lay2017/p/12207951.html)

### 什么是seata？

seata全称是：**s**imple **e**xtensiable **a**utonomous **t**ransaction **a**rchitecture，中文直译就是：简单的、可扩展的、自治的事务架构。

seata是一款开源的分布式事务的解决方案，致力于提供简单易用、高性能的服务。

同时，seata支持多种模式

1、at模式

2、tcc模式

3、saga模式

4、xa模式

总的来说，seata提供了分布式事务的一站式解决方案。

在此之前，seata的原名叫做fescar。

fescar全称是：**f**ast **e**a**s**y **c**ommit **a**nd **r**ollback，中文直译就是：快速、简单地提交和回滚。fescar这个名字非常简单粗暴地表达了它具备的高性能特征。

而从fescar到seata，也就意味着这款分布式事务中间件已经取得了阶段性的成果。


### 简要发展史

我们简单了解一下相关的发展史。阿里巴巴作为国内领先的互联网公司，在微服务的实践，分布式事务问题的处理都是比较早的，已经具备了很强沉淀积累。

2014 - 阿里中间件团队发布txc（taobao transaction constructor）在阿里内部提供分布式事务服务；

2016 - txc经过改造和升级，变成了gts（global transaction service）在阿里云作为服务对外开放，也成为当时唯一一款对外的服务；

2019 - 阿里经过txc和gts的技术积累，决定开源（Apache开源协议）。并且，在github上发起了一个项目叫做fescar（fast easy commit and rollback）开始拥有了社区群体；

2019 - fescar被重命名为了seata（simple extensiable autonomous transaction architecture），项目迁移到了新的github地址。