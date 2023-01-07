# 一对多
## 背景
一个客户可以有多个订单，而订单只能属于一个客户
## 数据库表
```sql
CREATE TABLE `customer` (
	`id` INT(11) NOT NULL AUTO_INCREMENT,
	`name` VARCHAR(50) NULL DEFAULT NULL,
	PRIMARY KEY (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=19
;

CREATE TABLE `orders` (
	`id` INT(11) NOT NULL AUTO_INCREMENT,
	`name` VARCHAR(50) NOT NULL DEFAULT '0',
	`cid` INT(11) NOT NULL DEFAULT '0',
	PRIMARY KEY (`id`),
	INDEX `FK_orders_customer` (`cid`),
	CONSTRAINT `FK_orders_customer` FOREIGN KEY (`cid`) REFERENCES `customer` (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=2
;
```
## 实体类
```java
@Data
public class Customer { //一的一方 one
    private Integer id;
    private String name;
    private Set<Order> orderList;
}

```
```java
@Data
public class Order { //多的一方 many
    private Integer id;
    private String name;
    private Customer customer;
}
```
## 关系映射文件配置信息
Customer.hbm.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
    <class name = "com.sean.entity.Customer" table="customer">
        <id name = "id" type="java.lang.Integer">
            <column name="id"></column>
            <generator class="identity"></generator>
        </id>
        <property name="name" type="java.lang.String">
            <column name="name"></column>
        </property>
        
     <!--配置 多的一方信息-->
    <set name="orderList" table="order" lazy="true">
        <key column="cid"></key>
        <one-to-many class="com.sean.entity.Order"></one-to-many>
    </set>
    </class>

</hibernate-mapping>
```
Order.hbm.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
    <class name = "com.sean.entity.Order" table="orders">
        <id name = "id" type="java.lang.Integer">
            <column name="id"></column>
            <generator class="identity"></generator>
        </id>
        <property name="name" type="java.lang.String">
            <column name="name"></column>
        </property>
      
     <!--配置一的一方-->
    <many-to-one name="customer" class="com.sean.entity.Customer" column="cid"></many-to-one>
    </class>

</hibernate-mapping>
```
## 添加到配置文件hibernate.cfg.xml中
```xml
<mapping resource="com/sean/entity/Customer.hbm.xml"></mapping>
<mapping resource="com/sean/entity/Order.hbm.xml"></mapping>
```
## 一对多测试
```java
void test2(){
    //获取配置信息
    Configuration configuration = new Configuration().configure();
    //获取SessionFacoty
    SessionFactory sessionFactory = configuration.buildSessionFactory();
    Session session = sessionFactory.openSession();

    Customer customer = new Customer();
    customer.setName("sean");

    Order order = new Order();
    order.setName("order");

    //关联关系
    order.setCustomer(customer);

    session.save(customer);
    session.save(order);

    session.beginTransaction().commit();
    session.close();
}
```
## 执行结果
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1627464757869-29859f4e-116d-40d0-8161-0817f18eaf64.png#height=104&id=u63ab6c81&name=image.png&originHeight=122&originWidth=663&originalType=binary&ratio=1&size=16677&status=done&style=stroke&width=567)![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1627464775360-4e83d325-31c0-4bd6-859f-315ece6e546f.png#height=113&id=u067141d1&name=image.png&originHeight=136&originWidth=681&originalType=binary&ratio=1&size=18067&status=done&style=stroke&width=565)
# 多对多
## 背景
一个学生能选多门课程，一门课程也能被多名学生选择
## 数据库表
```sql
--学生表
CREATE TABLE `students` (
	`id` INT(11) NOT NULL AUTO_INCREMENT,
	`name` VARCHAR(50) NULL DEFAULT NULL,
	PRIMARY KEY (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=6
;

--课程表
CREATE TABLE `courses` (
	`id` INT(11) NOT NULL AUTO_INCREMENT,
	`name` VARCHAR(50) NULL DEFAULT NULL,
	PRIMARY KEY (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=7
;

-- 中间表，只保存其他主表的主键作为外键
CREATE TABLE `students_courses` (
	`id` INT(11) NOT NULL AUTO_INCREMENT,
	`sid` INT(11) NULL DEFAULT NULL,
	`cid` INT(11) NULL DEFAULT NULL,
	PRIMARY KEY (`id`),
	INDEX `FK_students_courses_students` (`sid`),
	INDEX `FK_students_courses_courses` (`cid`),
	CONSTRAINT `FK_students_courses_courses` FOREIGN KEY (`cid`) REFERENCES `courses` (`id`),
	CONSTRAINT `FK_students_courses_students` FOREIGN KEY (`sid`) REFERENCES `students` (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=5
;

```
## 实体类
```java
@Data
public class Students {
    private Integer id;
    private String name;
    private Set<Courses> courses;
}
```
```java
@Data
public class Courses {
    private Integer id;
    private String name;
    private Set<Students> students;
}
```
## 关系映射文件
Students.hbm.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
    <class name = "com.sean.entity.Students" table="students">
        <id name = "id" type="java.lang.Integer">
            <column name="id"></column>
            <generator class="identity"></generator>
        </id>
        <property name="name" type="java.lang.String">
            <column name="name"></column>
        </property>
    <!--这里和中间表通过sid进行连接-->
    <set name="courses" table="students_courses">
        <key column="sid"></key>
       
        <many-to-many class="com.sean.entity.Courses" column="cid"></many-to-many>
    </set>
    </class>

</hibernate-mapping>
```
Courses.hbm.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
    <class name = "com.sean.entity.Courses" table="courses">
        <id name = "id" type="java.lang.Integer">
            <column name="id"></column>
            <generator class="identity"></generator>
        </id>
        <property name="name" type="java.lang.String">
            <column name="name"></column>
        </property>
    <!--这里和中间表通过cid进行连接-->
    <set name="students" table="students_courses">
        <key column="cid"></key>
        
        <many-to-many class="com.sean.entity.Students" column="sid"></many-to-many>
    </set>
    </class>

</hibernate-mapping>
```
## 添加到配置文件中去
```xml
<mapping resource="com/sean/entity/Students.hbm.xml"></mapping>
<mapping resource="com/sean/entity/Courses.hbm.xml"></mapping>
```
## 多对多测试
```java
public class TestMany2Many {
    public static void main(String[] args) {
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();

        //从学生的角度出发，一个学生选了多门课程；相反的，也可以从课程的角度出发，一门课被多名学生选择
        Students students = new Students();
        students.setName("seanhe");

        Courses courses = new Courses();
        courses.setName("Java test");

        Courses courses2 = new Courses();
        courses2.setName("C++ test");

        Set<Courses> coursesSet = new HashSet<>();
        coursesSet.add(courses);
        coursesSet.add(courses2);
        students.setCourses(coursesSet);
        
        session.save(courses);
        session.save(courses2);
        session.save(students);
        
        session.beginTransaction().commit();
        session.close();

    }
}
```

## 执行结果
![image.png](_assets/Hibernate%20-%20级联操作/1627465603871-559f3b67-4c61-4088-aac5-0a4c9def12cd.png)
![image.png](_assets/Hibernate%20-%20级联操作/1627465618188-beea4356-0078-4eff-8386-f952b5b399e3.png)
![image.png](_assets/Hibernate%20-%20级联操作/1627465636751-8552ee45-59ff-4538-a65f-a7ee52ebda18.png)
后台打印的sql

```

Hibernate: 
    insert 
    into
        courses
        (name) 
    values
        (?)
Hibernate: 
    insert 
    into
        courses
        (name) 
    values
        (?)
Hibernate: 
    insert 
    into
        students
        (name) 
    values
        (?)
Hibernate: 
    insert 
    into
        students_courses
        (sid, cid) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        students_courses
        (sid, cid) 
    values
        (?, ?)
```
