# 第2章 一切都是对象**
> 如果我们说另一种不同的语言，那么我们就会发觉有一个有些不同的世界 -- Luduing Wittgerstein

尽管Java基于C++，但相比之下，Java是一种更**纯粹**的面向对象程序设计语言；Java语言假设我们只进行面向对象的程序设计（OOP）

## 2.1 用引用操纵对象
每种语言都有自己操纵内存中元素的方式：

1. 直接操纵  
2. 基于某种特殊语法的间接表示

Java中，尽管一切都看作是对象了，但操作的标识符实际上是对象的一个引用（reference）。引用可以单独存在，你拥有一个引用，并不一定需要有对象和它关联。
String s;
这里创建了一个引用，并不是对象。如果此时向s发送消息，那么会报运行时错误，因为它实际上并没有和任何对象关联。更加安全的做法是：**创建一个引用的同时便进行初始化**
String good = “good”;
这种创建方式是Java语言的一个特性：字符串可以用带引号的文本初始化；但更通用的方式是用关键字**new**。
## 2.2 必须由你创建所有对象
一个引用被创建了，就希望它能与一个新的对象相关联。通常用**new**操作符来实现这一目的，以new关键字进行对象的初始化，new关键字的意思是：”给我一个新的对象”（上面的例子可以写成）
String good = new String("good");
表示： "给我一个新的字符串"，而且通过提供一个初始字符串，给出了**怎样**产生这个String的信息！
### 2.2.1 对象存储到什么地方
素质三连问：程序运行时，对象是怎么进行放置安排的？内存是怎么样分配的？你个垃圾会吗？

1. 寄存器  最快的存储区

2. 栈   位于通用RAM

3. 堆   通用内存池

4. 常量存储

5. 非RAM存储


（更加详细的内容，参考《深入理解JVM》）
### 2.2.2 特例：基本类型 （由父标题推出：这些对象是Java已经帮你创建好了的）
基本类型之所以要特殊对待，是因为**new**将对象存储在**“堆“**里，故用new创建一个对象——特别是小的，简单的变量，往往不是很有效。因此，不用new创建变量，针对基本变量创建一个并非是引用的”自动“变量，这个变量直接存储”值“，并置于**“栈”**中，因此更加高效。（效率：栈>堆）
Java的基本类型的大小是固定的，这也是可移植性的原因之一！
需要注意的是 boolean 没有确定大小，只有字面值 **true**和**false**
基本类型有着对应的包装类，使得可以在对堆中创建一个非基本对象，用来表示对应的基本类型。
char c = "x";
Character ch = new Character(c);
//或者
Character ch = new Character("x");
Java SE5 有自动装箱和拆箱的功能。
Character ch = "x"; //基本类型转换成包装类型 ，装箱
char c = ch;        //包装类型反向转换基本类型 ，拆箱
**高精度数字** ：以调用方法的形式进行运算，运算速度会比较慢；牺牲速度换取了精度！

1. BigInteger
支持任意精度的整数，不会丢失任何数据

2. BigDecimal
支持任何精度的定点数，例如货币汇率的计算！

### 2.2.3 Java中的数组
Java中的数组需要被初始化，而且不能超出数据的范围，这种范围检查需要以少量的内存开销和运行时的下表检查为代价的！但由此换来了安全性和效率的提高，小小的内存开销可以说很值得了！
当创建一个数组对象时，就是创建了一个引用数组，并且引用都会自动被初始化为一个特定值，该值拥有自己的关键字**null**！一旦Java看到了null，就知道这个引用还没有指向某个对象，在使用任何引用时，都要为其指定一个对象！ （ 关于数组更详细的内容，见后面章节！）
## 2.3 永远不要销毁对象 （对应着JVM的垃圾回收机制）
### 2.3.1 作用域
作用域决定了在其内定义的变量名的**可见性和生命周期**！
注意代码
//这是c++，较大的作用域的变量可以”隐藏”！
{
    int x = 12;
    {
        int x = 24; //在Java中，非法的，x在之前已经被使用了
    }
}
### 2.3.2 对象的作用域
Java对象不具备和基本类型的生命周期。当用new创建了一个Java对象时，它可以存活于作用域之外。
{
    String s = new String("a String");
}//end of scope
此时，引用s在作用域就是花括号内，超过该区域无法再访问这个对象，但是s指向的String对象仍继续占据内存空间。
问题素质三连问：如何防止这些超过了作用域却依旧存活在内存空间的对象撑爆你的内存，让你的程序终止呢？ 
Java有垃圾回收器（GC，garbige collector），用来监视用new创建的所有对象，那些不再被引用的对象的内存空间将会被释放掉，以便给新对象使用！ 
吹一波Java的垃圾回收机制：**在一定程度上来说，不需要关心对象的销毁，消除了内存泄漏的顾虑！**
## 2.4 创建新的数据类型 ：类
用class 关键字来声明类
class ATypeClass {   /*class body*/     }
用new来创建这个类型的对象
ATypeClass a = new ATypeClass();
### 2.4.1 字段和方法
类中有两种元素： **1.字段（也叫数据类型）和 2.方法（也叫成员函数）**
字段可以是任意类型的对象，可以通过其引用与其进行通信，也可以是基本类型的一种。
如果字段是某个对象的引用，那必须初始化该引用（就是用new一下）
每个对象都有其字段空间；普通字段不能在对象间共享。
//定义一个类
class DataOnly{
    int i;
    double d;
    boolean b;
}
//创建对象
DataOnly dataOnly = new DataOnly();
给字段赋值
dataOnly.i = 47;
dataOnly.d = 40.0;
dataOnly.b = false;
给对象字段赋值
myPlane.leftTank.capacity = 100;
基本成员默认值
如果类的某个成员是基本数据类型，即使没有初始化（既没有new一下）Java也会自动给它一个默认值。

| 基本类型 | 默认值 |
| --- | --- |
| boolean | false |
| chat | '\\u0000'(null) |
| byte | (byte)0 |
| short | (short)0 |
| int | 0 |
| long | 0.L |
| float | 0.0f |
| double | 0.0d |

Java会自动帮你初始化这些基本类型的成员变量，但是这种方法并不适用于局部变量（几并非某个类的字段）。如果某个方法中定义了：
int x;
那么变量x得到的可能是任意值，而不会被自动初始化为0，Java在编译时会返回一个错误，告诉你这个局部变量没有初始化
## 2.5 方法，参数和返回值
**方法的基本组成：名称，参数，返回值，方法体**
ReturnType methodName( /* Argument list*/) {
    /*Method body*/
}
返回类型：调用方法之后从方法返回的值
参数列表：要传给方法的信息类型和名称
**_方法签名=方法名+参数列表 ，它唯一地标识出某个方法_**
方法是类的一部分，只能通过对象调用（当然也有直接类调用的，static方法就是针对类调用的，后详解 见2.6.3）
方法调用方法：
objectName.methodName(arg1,arg2);

int x = a.f(); //向对象发送消息
返回值的类型必须要和x的类型兼容！
### 2.5.1 参数列表
方法的参数列表指定要传递给方法什么样的信息，采用的都是对象的形式。在列表中指定对象的类型和名字，但这里实际上传递的是对象的引用。
例子：接受String为参数，返回该字符串长度的两倍
int storage(String s){
    return s.length()*2;
}
这里s一旦传递给此方法，就可以把他当作其他对象一样进行处理。如果不想返回任何值，
void nothing(){
 	/****/
}
## 2.6 构建一个Java程序
### 2.6.1 名字可见性
Java使用包名来解决文件名字冲突的问题，创建名字空间来唯一确定一个类的位置
net.mindview.utility.fobiles
com.sean.Intruduce.class
### 2.6.2 运用其他构件（导入其他包内的类）
使用import关键字
import Java.util.ArrayList; //导入指定某个类
import Java.util.* //导入指定某个包下的所有类
### 2.6.3 static关键字
static 出现的两种原因：

1. **_只想为某特定域分配单一存储空间_**

2. **_即使没创建对象，也能调用这个方法_**


在字段前加上 static 就定义了一个静态变量
class StaticTest{
    static int i = 47;
}
StaticTest st1 = new StaticTest();
StaticTest st2 = new StaticTest();
这里的 st1.i和st2.i指向同一个存储空间，具有相同的值47.`//为什么是48，看了英文版，是47，估计是译者写错了`
static的引用方法

1. **通过一个对象去定位它  st1.i;**

2. **通过类名直接引用  StaticTest.i;**


对于方法而言，也是类似的。
class Person{
    staic void hello( ... );
}
引用方法：
//通过对象来调用静态方法
Person p = new Person();
p.hello();
//类名直接调用静态方法
Person.hello();
## 2.7 第一个Java程序
//HelloDate.Java
import Java.util.*;
public class HelloDate{
    public static void main(String[] args){
        System.out.print("Hello. It's:");
        System.out.print(new Ddate());
    }
}

import关键字声明要使用的包, Java.lang是默认导入到每个Java文件中的,所以他的类可以直接被使用.但是这里Java.lang里面没有Date类,所以得导入有Date类的包. 也可以具体的显示导入哪个类
import Java.util.Date
### 2.7.1编译和运行
//编译Java文件
Javac HelloDate.Java
//运行
Java HelloDate
## 2.8注释和嵌入式文档
```java
// 这是单行注释

/*
这是多行注释...
这是多行注释...
*/

/**
这是文档注释,开头多了一个*号.
*/
```
### 2.8.1 注释文档
使用**Javadoc** 来提取注释以及特殊的标签,并把相邻的类和方法都抽取出来,输出一个HTML文件,形成一份说明文档
### 2.8.2 语法
Javadoc的两种方式

1. **嵌入HTML**

2. **文档标签**


独立文档标签是用@开头的命令,并且是在行首, 行内的@ 需要用花括号内,才能视为标签
注释文档的三种类型

1. 类 位于类定义之前

2. 域 域定义之前 (感觉叫变量注释比较容易理解)

3. 方法 方法定义之前


例子
```java
/**这是类注释*/
public class Documents{
    /**这是域注释*/
    int i;
    /**这是方法注释*/
    public void f(){.....}
}
```
需要注意的是:Javadoc只能对public和protected成员进行文档注释, private和包内访问成员的注释会被忽略掉 (不过可以使用 **-private** 进行标记,达到被输出的效果)
### 2.8.3 嵌入HTML
可以对注释文档加上html标签进行格式上的优化,因为Javadoc输出的就是HTML文件格式
例如:
/**
*<pre>
*System.out,print(new Date());
*</pre>
*
*here is the list:
*<ol>
*<li> item one
*<li> item two
*</ol>
*/

不需要自己加标题 (h1,hr)之类的标签,Javadoc自己会生成标题.不然会冲突
### 2.8.4 文档标签
1. @see	引用其他类
    格式:
    @see classname
    @see fuuly-qualified-classname
    @see fully-qualified-classname#method-name
2. {@link package.class#member label} 和@see类似, 用于行内,且用label作为超链接文本.
3. {@docRoot}  生成到根目录的相对路径
4. {@inheritDoc}  从当前这个类的最直接父类中继承相关文档到当前的文档注释中
5. @version 版本信息
    格式: @version version-information 
6. @author 作者信息
7. @since  最早的版本
8. @param  用于方法中
    格式: @param parameter-name description
9. @return 
    格式: @return description ,用于描述返回值的含义
10. @throws 抛出异常
11. @deprecated  表示过期
## 2.8.5 注释文档示例
```java
//: object/HelloDate.java 
import java.util.*; 
/** The first Thinking in Java example program. 
 * Displays a string and today’s date. 
 * @author Bruce Eckel 
 * @author www.MindView.net 
 * @version 4.0 
*/ 
public class HelloDate { 
 /** Entry point to class & application. 
 * @param args array of string arguments 
 * @throws exceptions No exceptions thrown 
 */ 
 public static void main(String[] args) { 
 System.out.println("Hello, it’s: "); 
 System.out.println(new Date()); 
 } 
} /* Output: (55% match) 
Hello, it’s: 
Wed Oct 05 14:39:36 MDT 2005 
*///:~
```
## 2.9 编码风格

1. 类名的首字母要大写,如果几个单词组成,把它们合在一起（**驼峰法**）
`class AllTheColorsOfTheRainbow{....}`
2. 字段以及对象引用名称等,第一个字母采用小写
```java
class AllTheColorsOfTheRainbow{
 	int anIntegerRepresentRainboow;
	void changeTheValue(int newValue){....}
}
```

