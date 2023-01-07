> ORM Framework： Hibernate 

# Hibernate与Spring Data JPA的区别是什么？
> [_原文：https://dzone.com/articles/what-is-the-difference-between-hibernate-and-sprin-1_](https://dzone.com/articles/what-is-the-difference-between-hibernate-and-sprin-1)

这两种技术非常相似，那么区别是什么呢？
在这篇文章中，我想描述一下Hibernate ORM框架与Spring Data JPA两者之间的区别。
首先让我们来了解一下JPA，Hibernate和Spring Data JPA的定义，这会让讨论他们之间的区别变得简单。
## 什么是Java Persistence API？
Java Persistence API提供了一个规范，用于将Java对象中的数据持久化、读取和管理到数据库中的关系表中。
获取更多关于JPA的信息 [JPA Tutorial - Java Persistence API](http://www.javaguides.net/p/jpa-tutorial-java-persistence-api.html)（你能找到所有关于JPA的信息）
## 什么是Hibernate框架
Java环境中，Hibernate是一种对象-关系映射解决方案。对象-关系映射或者ORM是编程技巧，映射应用程序模板对象域到关系型数据库表。Hibernate是基于java的ORM工具，提供了映射应用程序模型对象到关系型数据库表，或者反过来。
![](_assets/「译」Hibernate与Spring%20Data%20JPA的区别/orm-example.png)
获取更多关于Hibernate的信息 [Hibernate ORM](http://www.javaguides.net/p/hibernate-tutorial.html)（你能找到所有关于Hibernate的信息)

## 什么是Spring Data JPA
Spring Data JPA是Spring框架的一部分。Spring Data类库抽象的目标是显著地减少必须实现数据访问层的样板代码总量对不同的持久化存储。
Spring Data JPA不是JPA的提供者。而是一个在JPA基础上增加了额外抽象的类库/框架（就像Hibernate实现了JPA）
现在，您已经熟悉了JPA、Hibernate和Spring Data JPA的定义。现在，让我们讨论Hibernate和Spring Data JPA之间的区别。
## Hibernate和Spring Data JPA之间的区别是什么?
Hibernate是一个JPA实现，而Spring Data JPA是一个JPA数据访问抽象。Spring Data提供了GenericDao自定义实现的解决方案。它还可以通过方法名称约定为您生成JPA查询。
对于Spring Data，您可以使用Hibernate、Eclipse Link或任何其他JPA提供程序。一个非常有趣的好处是，您可以使用@Transactional注释声明性地控制事务边界。
Spring Data JPA不是一个实现或JPA提供者，它只是一个抽象，用于显著减少为各种持久性存储实现数据访问层所需的样板代码数量。我希望这篇文章对你有用。您可以在StackOverflow上找到这个问题的更多答案。
Hibernate提供了Java Persistence API的参考实现，这使它成为一个很好的ORM工具选择，并具有松散耦合的优点。
**请记住，Spring Data JPA总是需要JPA提供者，比如Hibernate或Eclipse Link。**

---

参考资料：

- [JPA视频教程](https://www.bilibili.com/video/BV1vW411M7zp)
- [https://www.quora.com/What-is-the-difference-between-Hibernate-and-JPA](https://www.quora.com/What-is-the-difference-between-Hibernate-and-JPA)

![image.png](_assets/「译」Hibernate与Spring%20Data%20JPA的区别/1600608894843-7bf94fcb-b44f-423a-8c78-0560b1e1c99c.png)

