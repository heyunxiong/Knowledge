> Java 基础知识： Java 继承、多态、封装

Java 三大特性能说的东西很多，这里只先简单的整理下，后续有深度的分析再补上。
## 封装
封装，简单来说就是自己管理好自己的属性和方法，独立于别人。
把有相关的信息作为一个整体，易于管理的同时又能组织关系
不受别人干扰，可以通过修饰符控制谁能动我的属性和方法

比如散落字段的name，age，address，phone，可以封装成 Person 类，有person进行管理
## 继承
> 叫爸爸环节

- Object类的地位

Java所有类都会默认继承Object类，Object类是所有类的父类，祖师爷。
使用关键字 extends 声明类之间的继承关系
```java
public class Father{
    void method1(){system.out.println("father method1"}
    void method2(){system.out.println("father method2"}
}

public class Son extends Father{
    @Override
      void method2(){system.out.println("son method2")}
}
// ----------test-----------
public class Test{
	public static void main(String [] args){
    	Son s = new Son();
        s.method1(); //会使用父类的
        s.method2(); //会使用自己重写的
    }	
}
```

- 继承的特性

和现实中的继承大差不差的意思，子类能继承父类的方法，子类没有该方法时候，会使用父类的；如果子类有了该方法，则说明重写了父类的方法，会使用自己重写的。
java只支持单继承
## 多态
指⼀个类实例（对象）的相同⽅法在不同情形下具有不同表现形式；（同一个动作，不同的人有不同的反应）

- **多态的充要条件**
   - 继承	
   - 重写⽗类⽅法
   - ⽗类引⽤指向⼦类对象
```java
//------------------Fruit.java-------------------
public class Fruit {
    int num;
    public void eat(){
        System.out.println("eat Fruit");
    }
}

//------------------Apple.java-------------------
public class Apple extends Fruit {
    @Override
    public void eat() {
        super.num = 10;
        System.out.println("eat " + num + " Apple");
    }
}

//------------------Orange.java-------------------
public class Orange extends Fruit {
    @Override
    public void eat() {
        super.num = 11;
        System.out.println("eat " + num + " Orange");
    }
}

//------------------MainTest.java-------------------
public class MainTest {

        public static void main(String[] args) {
            Fruit fruit = new Apple();
            fruit.eat();
            fruit = new Orange();
            fruit.eat();
        }
}

//------------------Run Result-------------------
eat 10 Apple
eat 11 Orange

Process finished with exit code 0
```
同一个方法，在不同的情形下（这里指不同子类引用）表现出不同的形式;
即：都是eat方法，在Apple对象和Orange对象的引用下，Fruit类的对象表现出不同的结构。
## 向上转型、向下转型
向上转型、向下转型代表了⽗类与⼦类之间的关系，它们的转型后的范围不⼀样

- 向上转型（扩大范围）

通过⼦类对象(⼩范围)转化为⽗类对象(⼤范围)，这种转换是⾃动完成的，不⽤强制。

- 向下转型（缩小范围）

 通过⽗类对象(⼤范围)实例化⼦类对象(⼩范围)，这种转换不是⾃动完成的，需要强制指定。
文章参考：[多态：向上、向下转型](https://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484902&idx=1&sn=aebf8fcfedf9182f30348a86926e6a3b&chksm=ebd63acadca1b3dc184dad42f865b482ba9958f3fa9a070ccda0ac51a53bca55235ca4fc6b48&mpshare=1&scene=1&srcid=0212CU0jufrWdFIlna5FOTeo#rd)
## 类之间的关系
类之间的关系除了“继承”，还有如下关系：

- **依赖 （uses-a）dependency**

如果一个类的方法操纵另一个类的对象，我们就说一个类依赖于另一个类
	例子： 电风扇，电。 电风扇要依赖电

- **聚合（ has-a）aggregation **

是一种具体且易于理解的关系。聚合关系意味着类 A 的对象包含类 B 的对象
	例子：篮子，苹果。 苹果都聚合在篮子里

- **继承（ is-a）inheritance **
是一种用于表示特殊与一般关系的。
例子： 猫 extends 动物
