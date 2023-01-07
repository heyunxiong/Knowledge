> Java 基础知识： 类、对象

## 万物皆对象！
> 如果我们说另一种不同的语言，那么我们就会发觉有一个有些不同的世界
>  ----- Luduing Wittgerstein

## 面向对象
面向对象，与之相对应的是面向过程；面向过程就像流水线一样，先做A, 再做B，最后做C；
而面向对象把事物最为一个整体， 有自己的属性和方法，方法里定义了如何使用属性，如何进行操作。
## 类
Java类是一种模板，它能被实例化，即创建新的对象。
### 创建对象

1. 创建引用，不与具体对象关联（注意会有null，空指针异常）

`Student tom;`

2. 使用关键字 new 

`Student jack = new Student();`
### 属性与方法
Java 类中包含属性和方法；

- 属性

属性又叫字段；属性可以是基本数据类型或引用类型

- 方法

方法也叫函数；方法有构造方法和普通的方法；构造方法用于创建该类的对象
```java
// 普通的java 类
public class Student{
    // 年龄属性
    int age;
    // 姓名属性
	String name;
    
    // 无参构造器方法；使用时： Student jack = new Student();
    public Student (){
    }
    // 有参构造器方法；使用时： Student tom = new Student(18,"Tom");
    public Student (int age, String name){
        this.age = age;
        this.name = name;
    }
    // 普通方法，获取学生信息
    public String getStudentInfo(){
    	return "age: " + age +"; name: "+ name;
    }
    
}
```

- 普通方法的组成：方法名称、方法参数、返回值、以及方法体
   - 方法名称：getStudentIdByName
   - 方法参数：name
   - 返回值：id
   - 方法体 ：{ } 的内容
```java
public int getStudentIdByName(String name){
    //通过名字找id
    int id = getId(name);
	return id;
}
```

- 构造器方法

构造方法，是特殊的方法，也叫构造函数，构造器；Java通过这个构造器，对每个对象进行初始化。
构造方法没有参数和返回值，名字需要和类保持一致
无参构造器是默认的构造器 ： Student jack = new Student( ); 
默认构造器是JVM默认添加的，如果此时手动添加一个任何一个构造器，JVM不提供默认的构造器，如果时候默认无参构造器会报错，需要手动加上！
```java
// 普通的java 类
public class Student{
    int age;
	String name;
    
    // 无参构造器方法；使用时： Student jack = new Student();
    public Student (){
    }
    // 有参构造器方法；使用时： Student tom = new Student(18,"Tom");
    public Student (int age, String name){
        this.age = age;
        this.name = name;
    }
 
    // 有参构造器方法；使用时： Student tom = new Student(18);
    public Student (int age){
        this.age = age;
    }
    // 有参构造器方法；使用时： Student tom = new Student("Tom");
    public Student (String name){
        this.name = name;
    }
}
```
### 方法重载
重载需满足的条件：

- 方法名称必须要相同
- 方法参数列表必须不同 （ 个数不同、类型不同、顺序不同等）
- 方法返回类型不影响，可以相同，可以不同;
- 仅仅是返回类型不同不是方法的重载

上述的多个构造器方法就是方法重载的实现之一
```java
public int getApple(int num){
	return 1;
}

public String getApple(String color){
	return "color";
}
```
### 方法重写
重写需满足的条件：

- 除了方法体不一样（不会管具体的实现），其他都得一样（返回值类型,⽅法名,参数列表）
- 标示符 @Override

除此之外，重写，也是父类和之类之间的描述

- 子类中重写的方法访问权限不能低于父类
```java
class Animal{
    public void play(){
    	System.out.println("Animal's paly()");
    }
}

//--------------------
class Cat extends Animal{
    @Override
    public void play(){
        System.out.println("memmmm~~~");
    	System.out.println("Cat's paly()");
    }
}

```
## 类的初始化
### 初始化顺序

- 静态属性：static 静态属性
- 静态⽅法块： static { }代码块
- 普通属性： ⾮ static 定义的属性
- 普通⽅法块： { } 代码块
- 构造函数： 类名相同的⽅法
- ⽅法： 普通⽅法

静态属性初始化 > 静态⽅法块初始化 > 普通属性初始化 > 普通⽅法块初始化 > 构造函数初始化
```java
public class LifeCycle {
    
	// 静态属性
	private static String staticField = getStaticField();
    
	// 静态⽅法块
	static {
		System.out.println(staticField);
		System.out.println("静态⽅法块初始化");
	}
    
	// 普通属性
	private String field = getField();
	
    // 普通⽅法块
	{
	System.out.println(field);
	}
    
    // 构造函数
	public LifeCycle() {
		System.out.println("构造函数初始化");
    }
	// 静态方法
    public static String getStaticField() {
		String statiFiled = "静态属性初始化";
		System.out.println("静态属性初始化");
		return statiFiled;
	}
    // 静态方法
	public static String getField() {
		String filed = "属性初始化";
		System.out.println("属性初始化");
		return filed;
	}
    
	// 主函数
	public static void main(String[] argc) {
		new LifeCycle();
	}
}
```
## 几个关键字 this、super、static、final
this表示当前对象
super表示父类
static 修饰的属性和方法属于类，使用时直接： 类名.属性 或者 类名.方法
被final修饰的值，在后面的操作中不能够再对它进行修改
