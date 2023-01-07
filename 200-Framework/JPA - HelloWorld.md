> framework: jpa 使用

## JPA 概述
JPA 即 Java Persistence API ，是Java EE 5.0后推出的访问数据持久层（ORM）的规范标准（类似于JDBC）
包名: **javax.persistence.***
![](_assets/JPA%20-%20HelloWorld/1637908691023-2a6dfad8-8ff6-4c47-89a4-fd7df8053974.jpeg)
JPA的优势

- 标准化，能让不同的ORM框架实现相同的接口，易于切换
- 有JPQL查询语法，易于编写sql
- 支持面向对象的高级特性，如继承等

JPA的技术点

- ORM映射元数据：支持xml（persistence.xml）和注解形式。元数据描述了对象和表之间的映射关系
- JPA的API 支持多种CURD的操作 
- JPQL 查询语言，可以实现通过操作对象进行数据的查询
## JPA 使用
因为JPA是一套标准规范，要用JPA需要选定一个实现了JPA标准的框架(Provider)，比如：Hibernate就是一个功能强大的ORM框架
使用步骤

1. 在**persistence.xml** 配置持久化信息
   1. 数据库连接信息
   2. 指定实现了JPA规范的ORM框架，并配置该框架的相关基本属性
```xml
//persistence.xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" 
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="2.1" 
             xsi:schemalocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd">
    <persistence-unit name="my-persistence-unit">
      	//  声明规范实现为Hibernate
        <provider>org.hibernate.ejb.HibernatePersistence</provider>
      	// 添加持久化类
      	<class>com.xxx.yyy.Student</class>
   			// 数据库配置信息
        <property name="javax.persistence.jdbc.driver" value="com.mysql.jdbc.Driver" />
        <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306" />
        <property name="javax.persistence.jdbc.user" value="root" />
        <property name="javax.persistence.jdbc.password" value="root" />
   			// ORM框架基础配置信息
      	<property name="hibernate.format_sql" value="true" />
      	<property name="hibernate.show_sql" value="true" />
     		<property name="hibernate.hbm2ddl.auto" value="update" />
      
    </persistence-unit>
</persistence>
```

2. 创建实体类，使用JPA提供的注解绑定属性和表之间的关系
```java
@Table(name="STUDENT") //对应哪个数据表
@Entity
public class Student{
  private Integer id;
	private String name;

	@Column(value = "ID") // 属性对应表的列
	@GeneratedValue(stategy=ID) //主键生产策略
	@Id //表示该属性对应表的主键
	getId(){...} //在get方法上进行标注
	setId(){...}
	
	@Column(value = "NAME") // 属性对应表的列
	getName(){...}
	setName(){....}
}
```

3. 使用JPA API进行数据操作
   1. 创建EntityManagerFactory（对应着Hibernate中的SessionFactory）
   2. 创建EntityManager（对应着Hibernate中的Session）
```java
// my-persistence-unit是xml定义的属性
EntityManagerFactory emf = Persistence.createEntityManagerFacoty("my-persistence-unit") 
EntityManager em = emf.createEntityManager();
em.getTransaction...
em.persist(Object)... // 注意em的api操作即可
transaction.submmit();
transaction.close()
```
## JPA 和 Hibernate 的关系
如前面所说，JPA是规范，使用JPA需要搭配一个实现了该规范的ORM框架，可以是Hibernate，Toplink等。选好ORM框架后，用JPA API进行操作即可。
至于Hibernate，直接使用Hibernate也没毛病。Hibernate的功能比JPA功能强大，因为除了实现JPA规范里面的东西，hibernate自己还有自己的独特的功能是JPA没有的。
![](_assets/JPA%20-%20HelloWorld/1600608894843-7bf94fcb-b44f-423a-8c78-0560b1e1c99c-20230104121318862.png)

Hibernate需要用到的配置文件有两个：
一个是Hibernate框架配置文件**hibernate.cfg.xml**，另一个是关系对象映射文件**People.hbm.xml**

使用的区别：

- JPA的 hello-world

 	[https://player.bilibili.com/player.html?bvid=BV1vW411M7zp&p=2&page=2](https://player.bilibili.com/player.html?bvid=BV1vW411M7zp&p=2&page=2)

- Hibernate的 hello-world

[https://www.yuque.com/go/doc/49926569](https://www.yuque.com/go/doc/49926569)
