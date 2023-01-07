# 引入依赖
```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.10.Final</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.11</version>
</dependency>
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.10</version>
</dependency>
```
# 创建数据库表
```sql
CREATE TABLE `people` (
	`id` INT(11) NOT NULL AUTO_INCREMENT,
	`name` VARCHAR(50) NULL DEFAULT NULL,
	`money` DOUBLE NULL DEFAULT NULL,
	PRIMARY KEY (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=2
;
```
# 创建实体类
People.class
```java
@Data //lombok插件注解
public class People {
    private Integer id;
    private String name;
    private Double money;
}
```
# Hibernate配置文件
hibernate.cfg.xml（默认文件名，如果自定义名字，需要在new Configuration_()_.configure_("自定义文件名") _指定
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!--数据库源配置-->
        <property name="connection.username">root</property>
        <property name="connection.password">root</property>
        <property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="connection.url">jdbc:mysql://localhost:3306/mytest</property>

        <!-- C3P0 -->
        <property name="hibernate.c3p0.acquire_increment">10</property>
        <property name="hibernate.c3p0.idle_test_period">10000</property>
        <property name="hibernate.c3p0.timeout">5000</property>
        <property name="hibernate.c3p0.max_size">20</property>
        <property name="hibernate.c3p0.min_size">5</property>
        <property name="hibernate.c3p0.max_statements">10</property>

        <!--数据库方言-->
        <property name="dialect">org.hibernate.dialect.MySQLDialect</property>

        <!--打印，格式化SQL-->
        <property name="show_sql">true</property>
        <property name="format_sql">true</property>
      
      <!--是否自动生成数据表-->
        <property name="hibernate.hbm2ddl.auto"></property>
        
    </session-factory>

</hibernate-configuration>
```
# 关系映射文件
People.hbm.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
    <class name = "com.sean.entity.People" table="people">
        <id name = "id" type="java.lang.Integer">
            <column name="id"></column>
            <generator class="identity"></generator>
        </id>
        <property name="name" type="java.lang.String">
            <column name="name"></column>
        </property>
        <property name="money" type="java.lang.Double">
            <column name="money"></column>
        </property>
    </class>

</hibernate-mapping>
```
在配置文件hibernate.cfg.xml里面添加关系映射文件
```xml
<!--注册实体关系映射文件-->
<mapping resource="com/sean/entity/People.hbm.xml"></mapping>
```
# 测试
```java
void test1(){{
    //获取配置信息
    Configuration configuration = new Configuration().configure();
    
    //指定特定的配置文件名
    // Configuration configuration = new Configuration().configure("hibernate.sean.xml");
    
    //获取SessionFacoty
    SessionFactory sessionFactory = configuration.buildSessionFactory();
    Session session = sessionFactory.openSession();

    People people = new People();
    people.setName("sean1");
    people.setMoney(101.0);
    
    session.save(people);
    session.beginTransaction().commit();
    
    session.close();
    System.out.println(configuration);

}}
```
# 结果
执行结果
![image.png](_assets/Hibernate%20-%20HelloWorld/1627463495610-eb20a048-2c12-41bf-8b65-362089459e5a.png)
数据库表
![image.png](_assets/Hibernate%20-%20HelloWorld/1627463471552-99f7ae99-3210-42d2-8001-6d7912b2f079.png)

