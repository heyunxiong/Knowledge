> Java 基础知识： 接口、抽象类

## 接口
接口的作用：定义方法，不提供具体实现；
使用interface表示一个接口，类通过implements实现某个接口
```java
public interface myInterface{ 
    void talk();
}


public class MyClass implements myInterface{
    
    void talk(){
    // do something....
    }
}
```
接口的特点：

- 是一个完全抽象类，不提供任何方法的实现，只定义方法（但是jdk1.8有默认方法）
- 修饰符要么是 public ，要么是default ，具有包访问权限
- 一个类能实现多个接口，接口之间可以多继承 

`public interface MyInterface extends Iterable, Serializable _{...}_`

- 接口无法被实例化，不能用来创建对象



### 默认方法
接口默认方法，实现该接口的类不需要重新实现，可以用该接口实现类的对象直接使用默认方法

- 使用默认方法：myinterface.speak(); myinterface是实现MyInterface接口的对象变量。
- 使用静态方法：和普通类的静态方法使用一样，接口名.静态方法( ）：MyInterface.callStatic( )
```java
public interface MyInterface {
    void say();
    void talk();
    
    default void speak(){
        System.out.println("speak");
    }
    
    static void callStatic(){
        System.out.println("this is static");
    }
}
```
### 函数式接口
什么是函数式接口：
函数式接口(Functional Interface)就是一个有且仅有一个抽象方法，但是可以有多个非抽象方法的接口（staic或者default）。

使用@FunctionalInterface表示一个函数式接口，接口内不能有两个或多个抽象方法
//Multiple non-overriding abstract methods found in interface com.sean.stream.DefaultInterface 报错信息
```java
@FunctionalInterface 
public interface DefaultInterface {
    void say();
    //void talk(); // 报错，无法编译通过，有多个抽象方法
    
    default void hi(){
     System.out.println("hi"); // 可以，因为有多个default后者static的实现，但是抽象的只能有一个
    }
    
    default void speak(){
        System.out.println("speak");
    }

    static void callStatic(){
        System.out.println("this is static");
    }
    static void call(){
        System.out.println("this is call");
    }
}
```
## 抽象类
抽象类是抽象能力比接口弱一点的类。使用abstract关键字表示一个抽象类
```java
public interface MyInterface{
	void talk();
}

abstract class MyAbstractClass implements MyInterface{

	void talk(){
    // do something..
    }
    
    abstract void sing(); //抽象方法，被继承的时候，继承类需要对此方法进行实现
}


class MyClass extends MyAbstractClass{

	@Override
    void sing(){
    // 实现抽象方法
    }
}
```
抽象类的特点：

- 如果有抽象方法，那么这个类一定是抽象类；需要用abstract修饰
- 用abstract修饰的类，是抽象类，但不一定有抽象方法；
```java
abstract class MyAbstractClass{ //是抽象类，可以没有抽象方法

	void talk(){。。。}
}
```

- 抽象类中可以有具体的方法实现，和普通的方法一样
- 抽象类中可以定义：构造方法，抽象方法，普通属性，方法，静态属性，静态方法
- 抽象类不能被实例化，无法创建对象
