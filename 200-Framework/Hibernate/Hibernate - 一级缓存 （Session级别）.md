# 尝试缓存
测试缓存的demo代码
```java
void testCache(){
	//获取配置信息
	Configuration configuration = new Configuration().configure();
	//获取SessionFacoty
	SessionFactory sessionFactory = configuration.buildSessionFactory();
	Session session = sessionFactory.openSession();
	
	News news = session.get(News.class, 1);
	//News news2 = session.get(News.class, 1);
	System.out.println(news);
	//System.out.println(news2);
	
	session.close();
}
```
去数据库查询一次News对象，并打印News对象信息
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1627909760917-c6217263-92c9-4217-8cf5-f83991cc9f21.png)
接着放开注释，获取数据库中同一条数据，赋值给另一个引用news2。

```java
	News news = session.get(News.class, 1);
	News news2 = session.get(News.class, 1);
	System.out.println(news);
	System.out.println(news2);
```
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1627909439311-2f96cfff-b616-4028-822b-986320b3542e.png)
从打印结果可以看到，只向数据库发了一条select，因为有缓存的存在；
Session生命周期结束前，缓存没有被清理，那么缓存对象也不会结束生命周期，这里的两次获取同一条数据库中的信息，视为同一个对象。
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628493198233-0afaeac5-a192-4b64-af6b-74e0ccb02944.png)

# 操作Session缓存
主要的缓存操作方法
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628492610146-6ba54b54-b3ea-47fd-9eff-d5960520ce75.png)

## flush( )方法
flush方法的介绍
使数据表和Session缓存对象的状态保持一致（方向是缓存--->数据表）
```java
void testCache(){{
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();
    
        News news = session.get(News.class, 1);
        System.out.println(news);
        news.setAuthor("Sean-flush");
        Transaction transaction = session.beginTransaction();
    
        session.flush(); // 这里打个断点
    
        System.out.println(news);
        transaction.commit();
        session.close();

    }
}
```
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1627910220612-d3db5c2c-9e5d-4b76-8705-ce399a6a9500.png)
观察断点前后控制台的输出情况和数据库表更新；
执行之前没有控制台打印update语句，执行之后，打印update语句；数据库中的数据并没有发生变化，因为事务还未提交。

缓存中的数据和数据库中的数据不一致时，flush会发送update语句，到那时不会提交事务
transaction.commit的时候才会提交flush的结果，默认情况下事务提交会在先flush在update（这里是显示调用flush）
注意点：

1. 遇到QBC或者HQL查询得时候，会提前flush，需要查询到最新的记录
2. commit( )会先调用flush( )，并且提交事务；flush( )不会提交事务
## refresh( )方法
refresh方法的介绍
使Session缓存对象和数据库表的状态保持一致（方向是数据表--->缓存）
```java
 void testRefresh(){
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();
     
        News news = session.get(News.class, 1);
        System.out.println(news);
       
     	//使用refresh，再第二次打印之前手动修改数据库的内容，refresh方法需要获取数据库最新的内容
        session.refresh(news); //打个断点
        System.out.println(news);
     
        session.close();
    }
```

- 未修改数据库信息前，控制台和数据表的信息

![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628323078511-98b18cb7-5b79-4ec8-b7c8-0f7abbcb6677.png)
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628323095808-41237130-bb9d-4557-9fd3-fd8ea1057b81.png)

- 手动修改数据库的信息

![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628323177746-847b5540-696b-4f65-8d3e-4cabbcca813e.png)

- 继续执行，可以看到refresh会从数据库中获取最新的内容，并且更新缓存数据

![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628323210528-ebc90546-4d21-4c1b-9733-733168409bca.png)
注意点：如果没有refresh成功，需要查看是否是mysql的事务隔离级别设置不对，往这个方向去查。

## clear( ) 方法（翻车）
clear方法的介绍
清理session缓存中的对象
The Session.clear() method is used to remove all cached objects associated with the session.
不知道为什么clear不生效
```java
void testClear(){
    
        //获取配置信息
        Configuration configuration = new Configuration().configure();
        //获取SessionFacoty
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();
    	Transaction transaction = session.beginTransaction();

        News news = session.get(News.class, 1);
        News news2 = session.get(News.class, 1);
        System.out.println(news.getAuthor());
        //使用clear，再第二次打印之前清理缓存，第二次打印对象的时候需要重新select（通过之前的测试知道，连续打印两个对象是不需要重复拿的）
        session.clear();
        System.out.println(news2.getAuthor());
    	transaction.commit();
        session.close();
}
```
未加clear打印同一个对象是有缓存的
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628323979576-47809fd4-cb4d-43d5-b213-f58914f04a00.png)
放开 session.clear( )方法，结果居然还是一样？？有点翻车。
![image.png](_assets/Hibernate%20-%20一级缓存%20（Session级别）/1628324387490-51fca173-ed25-479a-99f3-adef6b379f9c.png)
需要查一下原因 SO的链接  [Stackoverflow- How does session.clear() work in Hibernate](https://stackoverflow.com/questions/42969763/how-does-session-clear-work-in-hibernate)， 
示例用法： [示例代码使用clear方法](https://www.javaguides.net/2019/12/hibernate-sessionclear-method-example.html)

