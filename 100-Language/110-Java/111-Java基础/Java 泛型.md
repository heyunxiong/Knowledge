> Java 基础知识： 泛型 Genetic

## 泛型的概念
泛型的核心思想是对参数类型化，限制你添加进集合的类型；
就是规定集合内的类型是同一种。你给我什么类型，那么我这个集合就是什么类型。

我的理解：
首先，理论上来说，集合是可以放各种类型的元素的，比如现实生活中的果篮：可以放苹果，香蕉，橘子等；
但是这里存在一个问题，当取数的时候，不一定能取到类型一致的元素，容易出现java.lang.ClassCastException。
就好像刚才放进了各种水果的果篮，此时，你想吃苹果，你不一定能拿到类型是苹果的水果。
所以，泛型的意义就在这里的了。规定你能放进集合的元素类型，取得时候就不会出现类型转换异常。
## 泛型的类型
### 泛型类
一个泛型类 （ generic class ) 就是具有一个或多个类型变量的类，如下的具有一个类型变量T
```java
public class MyGenetic<T> {
    private T name; //属性name的类型此时在类里面未知，需要由外部指定，用T表示
    
    public T getName() {
        return name;
    }

    public void setName(T name) {
        this.name = name;
    }
}
```
**关于类型变量**
类型变量使用大写形式 ，在 Java 库中 
使用变量 E 表示集合的元素类型 
K 和 V 分别表示表的关键字与值的类型 
T ( 需要时还可以用临近的字母 U 和 S ) 表示 “ 任意类型 ” 

### 泛型接口
```java
public Interface MyGenetic<T> {
    public T getName();
}
```
### 泛型方法
类型变量放在修饰符后面，返回类型前面；即系public后，void前
泛型方法可以在泛型类中定义，也可以在普通类中定义
```java
 public <T> void func1(T t){
      System.out.println(t.getClass().getName());
  }
```
泛型方法使用
```java
public class MyGenetic<T> {

    public static < T > T getMiddle ( T ... a )
    {
        return a [ a.length / 2 ] ;
    }

    public static void main(String[] args) {
        					//调用时，<String> 可以省略，java会通过上下文进行类型推断
        String s = MyGenetic.<String>getMiddle("sean","yx","he"); 
        System.out.println(s);
    }
}
```
### 泛型通配符 ?
上界通配符 :
 <? extends Employee> 该通配符为 Employee的所有⼦类型。它表示的是 ? 都是Employee类型的⼦类。
```java
class Animal{..}

class Cat extends Animal{...}

class Dog extends Animal{...}

class Computer{....}

// 此时如果有 <? extends Animal>  ?可以是 Cat 和 Dog； 但是?不可以为Computer
```

下界通配符：
<? super Employee> 该通配符为 Employee的所有超类型。它表示的是 ? 的⽗类都是 Employee。
## 泛型类型不具有继承关系
一个比较重要的总结： **泛型类型在逻辑上看以看成是多个不同的类型，实际上都是相同的基本类型** 泛型不存在父子类的关系

例如： java.lang.Number 是 java.lang.Integer的父类 ，但是Box<Number> 与Box<Integer> 没有父子关系的还有一点需要注意 泛型的通配符 ？ Box<?> ?现在表示你给我什么类型，就是什么类型的，但是可以对？进行限制。 

例如： 下限 Box<X extends Number> 表示只能是Number类型及其子类的，其他类型不行。 上限Box<X super Number> 表示只能是Number类型及其父类，其他不行。
## 什么时候使用泛型
当类中的操作的引用类型不确定的时候，将运行时问题转移到编译时（运行出错需要debug，编译出错IDE会提示你）
