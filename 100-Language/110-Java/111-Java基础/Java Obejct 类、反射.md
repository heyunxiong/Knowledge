## Object 类
Object 类是所有java 类的父类，所有类都会默认继承该类，不需要显示继承
```java
package java.lang;

/**
 * Class {@code Object} is the root of the class hierarchy.
 * Every class has {@code Object} as a superclass. All objects,
 * including arrays, implement the methods of this class.
 *
 * @author  unascribed
 * @see     java.lang.Class
 * @since   JDK1.0
 */
public class Object {
//....
}
```
Object类的方法，方法描述来自API 文档，感觉是机器翻译的，好生硬。

| 方法 | 描述 |
| --- | --- |
| protected Object clone()  | 创建并返回此对象的副本。 |
| boolean equals(Object obj)  | 指示一些其他对象是否等于此 |
| protected void finalize()  | 当垃圾收集确定不再有对该对象的引用时，垃圾收集器在对象上调用该对象。   |
| Class <?> getClass()  | 返回此 Object的运行时类。   |
| int hashCode()  | 返回对象的哈希码值。 |
| void notify()  | 唤醒正在等待对象监视器的单个线程。 |
| void notifyAll()  | 唤醒正在等待对象监视器的所有线程。   |
| String toString()  | 返回对象的字符串表示形式。 |
| void wait()  | 导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法。 |
| void wait(long timeout)  | 导致当前线程等待，直到另一个线程调用 notify()方法或该对象的 notifyAll()方法，或者指定的时间已过 |
| void wait(long timeout, int nanos)  | 导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法，或者某些其他线程中断当前线程，或一定量的实时时间 |

### equals方法
equals用于检测一个对象是否等于另一个对象；但这个方法仅仅会判断两个对象是否具有相同的引用，如果两个对象有相同的引用，则两者相等。这种对比没有意义，引用背后完全可能是不同状态的具体对象。
```java
// equals 方法源码
public boolean equals(Object obj) {
    return (this == obj);
}
```
equals方法具有的特性：

1. 自反性：对任何非空引用x，x.equals(x)应该返回true
2. 对称性：对于任何引用 x 和 y , 当且仅当 y.equals(x) 返回 true , x.equals(y) 也应该返回 true
3. 传递性： 对于任何引用 x ,y 和 z , 如果 x.equals(y)返 true, y.equals(z) 返回 true, x.equals(z)也应该返回 true
4. 一致性： 如果 x 和 y 引用的对象没有发生变化, 反复调用x.equals(y) 应该返回同样的结果
5. 对于任意非空引用x，x.equals(null) 应该返回false

**对称性的争议**

1. 如果子类能够拥有自己的相等概念 ，则对称性需求将强制采用 getClass 进行检测
2. 如果由超类决定相等的概念, 那么就可以使用instanceof 进行检测,这样可以在不同子类的对象之间进行相等的比较
### hashCode方法
散列码 （ hash code ) 是由对象导出的一个整型值。 散列码是没有规律的。
如果x 和 y 是两个不同的对象, x.hashCode ( ) 与 y.hashCode ( ) 基本上不会相同。但还是会有相同的情况，如果散列的不够均匀的话
```java
//hashcode 方法源码
public native int hashCode();
```
### 重写 hashCode方法和equals方法


**如果重新定义 equals 方法， 就必须重新定义hashCode 方法**
hashCode 方法应该返回一个整型数值 （ 也可以是负数 )， 并合理地组合实例域的散列码 ,以便能够让各个不同的对象产生的散列码更加均匀

### 重写例子
// to-do [视频：equals, hashcode重写例子](https://www.bilibili.com/video/BV11A411q7UK?from=search&seid=10408192158774005860&spm_id_from=333.337.0.0)
## 反射
反射是非常重要的特性，很多的框架都是基于反射思想，如Spring框架
### 什么是反射
Java 反射机制是在程序的运⾏过程中，对于任何⼀个类，都能够知道它的所有属性和⽅法；对于任意⼀个对象，都能够知道调⽤它的任意属性和⽅法，这种动态获取信息以及动态调⽤对象⽅法的功能称为java语⾔的反射机制
### 反射的功能

- 在运行过程中，能够判断该对象所属的类
- 在运行过程中，能查看对象的属性和方法，并且调用方法
- 在运行过程中，创建类的对象
- 在运行过程中，查看类的成员变量和方法
### Class 类
通过反射机制可以获取到一个类的完整信息，例如：所有（包含private修饰）属性和方法，包信息等。
而要想拿到这些信息，需要用到Class 类；换句话说，Class本身表示一个类的本身，通过Class可以完整获取一个类中的完整结构，包含此类中的方法定义，属性定义等。
每次编译后，会⽣成的 .class ⽂件，就会产⽣⼀个 Class 对象，这个 Class 对象⽤于表示这个类的类型信息

**获取 Class 对象的三种方式**

- 对象.getClass()  			thread.getClass()
- 类名.Class				Thread.class
- Class.forName( 类的包名 )	Class.forName(java.lang.Thread)
```java
//-----------Apple.java---------------
public class Apple extends Fruit implements Food{

    private String name;

    public int price;

    @Override
    public void eat() {
        super.num = 10;
        System.out.println("eat " + num + " Apple");
    }

    @Override
    public void eatFood() {
        System.out.println("eatFood : Apple");
    }
}
//-----------ReflectTest.java---------------
public class ReflectTest {
    public static void main(String[] args) throws ClassNotFoundException {
        Class<?> appleClass = Class.forName("com.sean.demo.Apple");
        String name = appleClass.getName();
        System.out.println(name);
        Field[] declaredFields = appleClass.getDeclaredFields();
        for (Field declaredField : declaredFields) {
            System.out.println("declaredField:" +declaredField);
        }
        Method[] methods = appleClass.getMethods();
        for (Method method : methods) {
            System.out.println("method: "+method);
        }
    }
}

// 打印结果
com.sean.demo.Apple
declaredField:private java.lang.String com.sean.demo.Apple.name
declaredField:public int com.sean.demo.Apple.price
method: public void com.sean.demo.Apple.eat()
method: public void com.sean.demo.Apple.eatFood()
method: public final void java.lang.Object.wait() throws java.lang.InterruptedException
method: public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
method: public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
method: public boolean java.lang.Object.equals(java.lang.Object)
method: public java.lang.String java.lang.Object.toString()
method: public native int java.lang.Object.hashCode()
method: public final native java.lang.Class java.lang.Object.getClass()
method: public final native void java.lang.Object.notify()
method: public final native void java.lang.Object.notifyAll()
```
Class 常用API: [官方api文档：https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/)

| 方法 | 描述 | 例子 |
| --- | --- | --- |
| getName()  | 返回类的权限定名称 | 如果是引⽤类型
String.class.getName() -> java.lang.String
如果是基本数据类型
byte.class.getName() -> byte
如果是数组类型
new Object[3]).getClass().getName() -> [Ljava.lang.Object |
| forName() | 根据类名获得⼀个 Class 对象的引⽤ | Class.forName(java.lang.Thread) |
| newInstance() | 创建⼀个类的实例，代表着这个类的对象 |  |
| getClassLoader() | 获取类加载器对象 |  |
| getTypeParameters() | 按照声明的顺序获取对象的参数类型信息。 |  |
| getConstructor(Class...<?> parameterTypes) | 获得该类中与参数类型匹配的公有构造⽅法 |  |
| getConstructors(） | 获得该类的所有公有构造⽅法 |  |

### ClassLoader类
![](_assets/Java%20Obejct%20类、反射/1636198472873-a2fa8995-83fd-4bc0-841e-25ad5602dabc.jpeg)
