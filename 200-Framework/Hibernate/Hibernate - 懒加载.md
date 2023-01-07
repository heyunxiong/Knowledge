# 背景
懒加载 = 延迟加载 = 惰性加载
## 关闭懒加载的情况
在客户订单例子中，查询客户信息的时候，因为级联关系的存在，或者说客户中持有订单的引用，会将订单信息一并查询出来；需要发送两条select sql，不管订单的信息有没有用到。
## 开启懒加载的情况
而懒加载的作用就是：查询客户信息的时候，如果不需要使用到订单的信息，不需要去查询订单的信息，只返回客户信息即可；需要访问到订单信息的时候，再去查询订单信息。
# 一对多：一的一方 Customer
## 实体类
```java
@Getter
@Setter
public class Customer {
    private Integer id;
    private String name;
    private Set<Order> orderList;

    @Override
    public String toString() {
        return "Customer{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}
```
```java
@Getter
@Setter
public class Order {
    private Integer id;
    private String name;
    private Customer customer;

    @Override
    public String toString() {
        return "Order{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}
```
## 开启懒加载 lazy="true"
Customer.hbm.xml：默认是开启的true，可以不写
```xml
<set name="orderList" table="order"> 
    <key column="cid"></key>
    <one-to-many class="com.sean.entity.Order"></one-to-many>
</set>
```
### 测试代码：未使用Order信息
```java
public class TestLazy {
    public static void main(String[] args) {
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();

        Customer customer = session.get(Customer.class,18);
        System.out.println(customer); //只是打印客户信息

        session.close();
    }
}
```
### 测试结果
只会打印一条查询客户信息的sql，表明开启了懒加载
![image.png](_assets/Hibernate%20-%20懒加载/1627525202850-5cbae9bb-0062-44a9-b08a-59e977808c53.png)

### 测试代码：使用Order信息
```xml
public class TestLazy {
    public static void main(String[] args) {
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();

        Customer customer = session.get(Customer.class,18);
        System.out.println(customer.getOrderList().size());

        session.close();
    }
}
```
### 测试结果
打印两条select sql，需要使用order的信息才会去查询。
![image.png](_assets/Hibernate%20-%20懒加载/1627525625345-14b84dff-d9ab-4b23-8c9e-13dccd310a06.png)

## 关闭懒加载 lazy="false"
在Customer.hbm.xml：将lazy改为false，关闭懒加载
```xml
<set name="orderList" table="order" lazy="false"> 
    <key column="cid"></key>
    <one-to-many class="com.sean.entity.Order"></one-to-many>
</set>
```
### 测试代码：同样未使用Order信息
```java
public class TestLazy {
    public static void main(String[] args) {
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();

        Customer customer = session.get(Customer.class,18);
        System.out.println(customer); //只是打印客户信息

        session.close();
    }
}
```
### 关闭懒加载的结果
即使没有使用到order信息，还是会查询出来；
![image.png](_assets/Hibernate%20-%20懒加载/1627525528264-e51bd3f7-c103-4726-85da-1cc09982f41c.png)

## 懒加载 lazy="extra"
相较于false，更加懒惰，或者说更加智能；
同样的测试代码，extra会使用聚合函数返回一个结果集大小，而false或者true的情况下会select 所有列；
`System.out.println(customer.getOrderList().size())`
结果显示，去查看orderlist的大小的时候，不是去查每个column，而是智能的返回一个大小结果count(id);
![image.png](_assets/Hibernate%20-%20懒加载/1627525762500-647bff2f-abba-44db-b18c-f51053188594.png)

## 遇到的问题
一直查询最终导致“栈溢出”；

- 原因：

从类的关系中可以看到，代码中的print方法调用的是Customer类中有toString方法，而toString方法中用到了Orders，所有会去查orders的信息；而Orders类中持有Customer的引用，又会去创建并查询Customer的信息。。
无限套娃：Customer-->订单--->Customer2--->订单2--->Customer3....
![image.png](_assets/Hibernate%20-%20懒加载/1627524817347-c8f185f6-eeef-4d0c-9887-7e4cef1964fa.png)
![image.png](_assets/Hibernate%20-%20懒加载/1627524838622-8dcb8205-387b-4cdf-9c19-c188dda1e734.png)

- 解决：

1.修改下两个实体类的toString ，先不要打印order、customer的信息
2.把“@Data”修改成@Getter，@Setter

# 一对多：多的一方 Orders
## 开启懒加载 lazy = "proxy"
默认是proxy（可以理解成true）
```xml
<many-to-one name="customer" class="com.sean.entity.Customer" column="cid" lazy="proxy">
</many-to-one>
```
![image.png](_assets/Hibernate%20-%20懒加载/1627526715506-f7304833-78c6-48a3-a38a-0277e2f479fe.png)
### 测试代码：未使用Customer信息
```java
public class TestLazy {
    public static void main(String[] args) {
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();

        Order order = session.get(Order.class,1);
        System.out.println(order);
        session.close();
    }
}
```
### 测试结果
查询一次
![image.png](_assets/Hibernate%20-%20懒加载/1627528695172-1fcf750e-e5ed-402c-b050-c00736190a4d.png)

### 测试代码：使用customer信息
`System._out_.println_(_order.getCustomer_())_;`
### 测试结果
可以看到使用了customer信息才会去查询。
![image.png](_assets/Hibernate%20-%20懒加载/1627528789330-67729211-9c28-4e07-ac19-df4bb84bd563.png)
存疑点：出现了三条语句，除了查customer和order，还查多了一次order。
我个人猜：为了关联cusotmer表？还是缓存？？？

## 关闭懒加载 lazy = "false"
```xml
<many-to-one name="customer" class="com.sean.entity.Customer" column="cid" lazy="false">
</many-to-one>
```
### 测试代码：未使用Customer信息
```xml
public class TestLazy {
    public static void main(String[] args) {
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();

        Order order = session.get(Order.class,1);
        System.out.println(order);
        session.close();
    }
}
```
### 测试结果
未使用customer信息也会去查询customer的信息
![image.png](_assets/Hibernate%20-%20懒加载/1627526962201-1c85cdc5-5bec-4cc9-bc6d-61202ae8cb56.png)

## lazy = "no-proxy"
no-proxy与proxy的区别-
[https://www.cnblogs.com/superws/p/5839710.html](https://www.cnblogs.com/superws/p/5839710.html)
[https://blog.csdn.net/iteye_6481/article/details/82271588](https://blog.csdn.net/iteye_6481/article/details/82271588)
# 小结
需要知道懒加载在数据读取中的重要性，知道其lazy各个值代表的意思。
附：蛋疼的问题
![image.png](_assets/Hibernate%20-%20懒加载/1627530656886-be0187b1-6937-4fc6-b497-2aff2db1c95c.png)
