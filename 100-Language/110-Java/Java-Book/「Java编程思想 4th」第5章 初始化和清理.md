# 第5章 初始化和清理
初始化和清理

1. 初始化：程序员在开发过程中忘记初始化,而某些程序必须初始化
2. 清理：使用完成后,忘记回收,会一直占用内存
## 5.1 用构造器确保初始化
在Java中,通过提供构造器,类的设计者可确保每个对象都会得到初始化; Java会在用户有能力操作对象之前自动调用相应的构造器,从而确保出了初始化的进行.
如何命名初始化的方法, 

1. 避免和成员变量冲突

2. 能让编译器知道这是个初始化方法


方案: 采用与类相同的名称
```java
class Rock{
    Rock(){ //这就是一个构造器
        System.out.print("Rock");
    }
}
 
public class SimpleConstructor{
    public static void main(String[] args){
        for(int i=0; i<10; i++){
            new Roock();
        }
    }
}
```
在创建对象:new Rock(); 时,将会为对象分配存储空间,并调用相应的构造器.
> 每个方法首字母小写的 编码风格并不适用于构造器

不接受任何参数的构造器叫做默认构造器, 也叫无参构造器
带参构造器:

```java
class Rock2{
    Rock2(int i){ //带参构造器
         System.out.print("Rock" + i + "");
    }
}
 
public class SimpleConstructor{
    public static void main(String[] args){
        for(int i=0; i<20; i++){
            new Rock(i); //将参数带入到构造器中
        }
    }
}
```
构造器是一种特殊类型的方法,因为它没有返回值.这个void明显不同,因为void尽管方法本身不会返回什么,但仍可选择让它放回别的东西,构造器则不会返回任何东西.
## 5.2 方法重载
> 我看谁还问我 重载和重写的区别。重载：一个构造器的例子扔过去；重写：覆盖的意思，你的方法不行，用我的！

当你创建一个对象的时候,也就给此对象分配到的存储空间取了一个名字.
在日常生活中,相同的词可以表达多种不同的含义---它们被"重载"了.
在Java中,构造器是强制重载方法名的一个重要原因
如果想要用多种方式创建一个对象该怎么处理?
使用不同构造器, **1. 使用默认构造器  2.使用带形式参数的构造器.**
这两个构造器的名字相同,都是类名.为了让**方法名相同而形式参数不同**的构造器同时存在,必须用到方法重载
```java
import static net.mindview.util.Print.*;
 
class Tree{
    int height;
    Tree(){
        print("Planting a seedling");
        height = 0;
    }
     
    Tree(int initialHeight){
        height = initialHeight;
        print("Create new tree that is "+ height +"feet tall");
    }
    void infoo(){
        print("info no param");
    }
    void info(String s){
         print("info with param" + s);
    }
}
 
public class Overloading{
    public static void main(String[] args){
        for(int i = 0; i<5; i++){
            Tree t = new Tree(i);
            t.info();
            t.info("overload method");
        }
        //重载构造器
        new Tree();
    }
}
```
### 5.2.1 区分重载方法
如何让Java知道几个相同名字的方法呢? 
让**每一个重载的方法都必须有一个独一无二的参数类型列表**. 
甚至参数顺序的不同也足以区分两个方法(但不推荐这么做,会让人感到疑惑,维护起来比较麻烦)
有相同的参数,但是顺序不同,可以得以区分~
```java
public class OverloadingOorder{
    static void f(String s, int i){
        print("String "+ s + ", int :" + i);
    }
    static void f(int i, String s){
        print("int "+ i + ", String :" + s);
    }
    public static void main(String[] args){
        f("String first",11);
        f(99,"String second");
    }
}
```
### 5.2.2 涉及基本类型的重载
基本类型能从一个"较小"的类型自动转化成一个"较大"的类型.
如果某个重载方法接受int类型,它就会被调用, 如果传入的数据类型(实际参数类型)小于方法中声明的形式参数类型,实际数据类型就会被提升. char有点例外,char不被直接提升为int.
那如果传入的实际参数大于重载方法声明的形式参数呢?  将会通过类型转换来窄化,不然会报错.
### 以 返回值区分重载方法
**是否可以以返回值区分重载方法呢? **
**不行!**
有时候并不需要去关心返回值,你关注的是调用方法的结果
比如 : **f ( );  仅仅只是一个调用,不关心返回值.**
## 5.3 默认构造器
默认构造器又叫 "无参构造器", 没有形式参数, 作用是创建一个"默认对象". 
没显示的写出默认构造器, 编译器会自动创建一个.
**如果你自己定义了一个构造器,那么,编译器就不会帮你创建默认构造器了**,编译器会认为你已经有了一个构造器了,如果想使用默认构造器
你需要显示的声明,这样就有一个自定义的构造器和默认构造器了
```java
class Bird2{
     Bird2(String name); //自定义构造器
    Bird2(); //显式的声明默认构造器,如果你要使用的话.
}
```
## 5.4 This 关键字
如何才能让两个不同的对象都能调用同一个方法呢?
this 关键字只能在方法内部使用,表示对"调用方法的那个对象"的引用. 
this的用法和一般对象的引用并无不同. 如果在方法内部调用同一个类的另一个方法, 就不必使用this,直接调用即可. 

```java
public class Apriot{
    void pick(){/*...*/}
    void pit(){ pick(); /*...*/} //这里直接调用了同一个类中的另一个方法
}
```
pit()内部你可以写成 this.pick(); 没有必要使用this,当然使用了也不会报错,因为编译器会自动添加这个this
除非你需要指出返回当前对象的引用时, 才需要使用this关键字, 可以在return语句中加上 this.
```java
public class Leaf{
    int i = 0;
    Leaf increment(){
        i++;
        return this;
    }
}
void print(){
    System.out.println("i =" + i);
}
public static void main(String[] args){
    Leaf x = new Leaf();
    x.increment().increment().increment().print();
}
// 输出结果是 : i=3
```
由于increment()通过this关键字返回了当前对象的引用, 进行了几次的操作.
this 关键字对于将当前对象传递给其他方法
### 5.4.1 在构造器中调用构造器
使用this关键字可以在一个构造器中调用另一个构造器,避免代码重复.
this代表的是当前对象或者这个对象,它本身表示对当前对象的引用.
在构造器中,如果this有参数列表,那就有不同的含义了,将产生对符合此参数列表的某个构造器的明确调用.
this 只能调用一个构造器,且必须置于最起始位置,

`this.s = s; //传入的s和成员变量s名字相同, 这样处理可以相除歧义.`
**除了构造器外,其他地方不能调用构造器方法.**
### 5.4.2 static 的含义
**static是属于类级别的.**
_在没有创建对象的情况下,可以直接通过类本身调用static方法,这正是static的主要用途_
static方法就是没有this的方法,在static内部不能调用非静态方法,(非静态方法内可以调用静态方法) 
> 注意: 如果静态方法里面有一个对象引用,而这个引用则可以调用对象非静态方法. 严格意义上来说,也是在静态方法里面调用了非静态方法.

## 5.5 清理: 终结处理和垃圾回收
Java有垃圾回收器负责回收无用对象占据的内存资源.
垃圾回收器只是知道那些new出来的对象空间,但是该怎么回收释放呢?  --- finalize() 方法.
finalize()的原理: 垃圾回收器准备释放占用的存储空间, 首先会调用finalize()方法, 并且在下一次垃圾回收动作发生时,才会真正回收对象占用的空间内存.
Java里的finalize()不是c++中的析构函数 (c++ 销毁对象的函数)
在Java中, 

1. 对象可能不被垃圾回收

2. 垃圾回收并不等于析构

3. 垃圾回收只与内存有关

### 5.5.1 finalize() 用途何在
finalize() 不是作为通用的清理方法, 使用垃圾回收器的唯一原因是 为了回收程序不再使用的内存.
之所以要有finalize(),是由于分配内存时可能采用了类似C语言中的做法,而非Java中的通常做法. 在使用"本地方法"的情况下,本地方法时一种在Java中调用非Java代码的方式,本地方法支持c和c++.
所以简单来说就是, 因为调用了本地方法, 如果要释放本地方法的空间,就需要调用finalize()去清理.
清理非Java代码的方法资源.
### 5.5.2 你必须实施清理
Java中不允许创建局部对象,必须使用 new 创建对象,也没有delete函数. 正式由于垃收集机制的存在,使得Java没有析构函数,但垃圾回收器并不能替代析构函数, 而且不能直接调用finalize().
如果希望释放空间之外的清理工作,还是得明确调用某个恰当的Java方法,这就相当于析构函数了,只是没有析构那么方便.毕竟是在垃圾回收器都不起作用下的请况才选择了具体某个方法.
**无论是"垃圾回收"还是"终结"都不保证一定会发生.**
不要指望使用finalize(), 必须创建其他的清理方式,并且明确的调用它们.
finalize()是 对象终结条件的验证
当对某个对象不再感兴趣的时候,就是它可以被清理了.
下面是使用方式.
所有book对象都应该在checkin()后被销毁,.
system.gc()用于强制进行终结动作.
### 5.5.4 垃圾回收器如何工作 (涉及到JVM的知识,搁置)
## 5.6 成员初始化
Java会确保所有变量都有初始化值. 方法局部变量如果没有初始化,会以编译报错提醒来保证.
在类中,类的每个基本类型数据成员都会有一个初始值,这样就避免了因为没有初始化而报错了.
如果类中有对象的引用,不初始化的话,Java会给它一个特殊值 null
### 5.6.1 指定初始化
基本类型指定初始化
```java
int i = 10;
String s = "goods";
double d  = 10.0;
...
```
非基本类型指定初始化,就是在创建对象引用的时候指定new出来的对象
```java
class Depth{...}
public class Measurement{
 Depth d = new Depth();
}
使用方法指定初始化
//无参
public class MethodInit{
    int i = f();
    int f(){return 11;}
}
//带参
public class MethodInit{
    int i = f();
    int j = g(i);
    int f(){return 11;}
 int g(int n) {return n*10;}
}
```
初始化是有顺序的,不能先使用未初始化的类型,会抛出"向前引用"的异常
## 5.7 构造器初始化
可以使用构造器进行初始化.
注意:构造器初始化无法阻止自动初始化的进行. 什么意思呢?对于所有基本类型和对象引用,Java会先保证其初始值.
```java
public class Counter{
 int i; //这里已经被系统自动初始化了
    Counter(){
        i = 7; //这里的初始化也不过是将原来的i=0变成i=7;
    }
}
```
### 5.7.1 初始化顺序
在类的内部,变量之间定义的先后顺序决定了初始化顺序,
而变量和方法比较,变量会在任何方法被调用前得到初始化,而不是取决于定义顺序.
### 5.7.2 静态数据的初始化 (重要)
无论创建多少个对象,静态数据都占一份存储空间. 
**static关键字不能应用于局部变量,**
static变量的初始化 
1.基本类型      就和普通的一样
2.对象引用就是null
静态初始化只有在必要时刻才会进行. 
上面的例子,如果不创建Table对象,也不引用Table.b1或者Table.b2,那么静态的Bowl b1,b2 将不会被创建.只有在第一个Table对象被创建了,它们才会被初始化,以后静态对象不会被再次初始化.
**初始化的顺序先是 静态对象,然后非静态对象.**
这个例子中, 必须先要加载StitcInitialization类,然后是其静态域的table和cupborad被初始化,因其包含静态的Bowl对象,因此Bowl也会被加载,整个过程中,所有类都在执行main函数被加载了.
### 5.7.3 显式的静态初始化
说白了就是 **静态代码块**
```java
public class Spoon{
    static int i;
    static{
        i = 47;
    }
}
```
这和其他静态初始化动作一样,这段代码只会执行一次: 当首次生成这个类的一个对象时,或首次访问属于那个类的静态数据成员(即使没有创建对象)
### 5.7.4 非静态实例初始化
可以看到, 非静态的对象引用被创建了两次.
总结一下初始化顺序:
**静态 (静态变量和引用> 静态方法)   >非静态 (非静态变量和引用> 非静态方法)**
## 5.8 数组的初始化
什么数组呢?
就是具有相同类型的集合
定义数组引用: 
int[] a1; //Java推荐使用
//或者
int a1[];
此时只是一个引用,没有为它分配任何空间,没有初始化.
//指定长度,数组初始化
int[] a1 = {1,2,3,4,5};
数组下标从0开始,越界会报异常.
如果不确定数组的元素数量怎么办?
可以直接用new在数组里面创建元素.
int[] a = new int[rand.nextInt(20)];//基本类型
Integer[] a1 =new Integer[rand.nextInt(20)];// 这是一个类,里面的都是引用, a1就是一个引用数组.
a1[i] = rand.nextInt(50);//这样才算是给引用初始化元素;
rand.nextInt()返回0-20之间的一个随机值 会自动填充初始值(数字字符都是0, 布尔型是false);
花括号初始化对象数组
### 5.8.1 可变参数列表 //未看

## 5.9枚举类型
```java
//enum关键字
public enum Sepiciness{
 NOT, MILD, MEDIUM, HOT, FLAMING //枚举类一般都是大写的常量
}
//使用
Sepiciness medium = Sepiciness.MEDIUM;
```
创建enum时,编译器会自动添加一些有用的特性,比如toString()方法,方便显示enum实例的名字
会创建ordinal(),表示某个特定enum常量的声明顺序,还有static value()方法.用来按照enum常量的声明顺序,产生由这些常量值构成的数组
enum就是一个类.你可以将它当作其他任何类来处理, 比较常用的时可以结合switch使用.

