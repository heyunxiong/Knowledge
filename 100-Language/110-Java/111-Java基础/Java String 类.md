> Java 基础知识： String 类

## String
Java 没有内置的字符串类型 ，而是在标准 Java 类库中提供了一个预定义类：**String 类**
所以String属于引用类型，不是基本数据类型
每个用双引号括起来的字符串都是String 类的一个实例 对象， String 类对象称为不可变字符串
`String s = ""; `
`String s2 = "hello";`
```java
public class Main {
         
    public static void main(String[] args) {
        String str1 = "hello world";
        String str2 = new String("hello world");
        String str3 = "hello world";
        String str4 = new String("hello world");
         
        System.out.println(str1==str2); // false
        System.out.println(str1==str3); // true
        System.out.println(str2==str4); // false
    }
}
```
### 子串
String 类的 substring 方法可以从一个较大的字符串提取出一个子串 。 例如 ：
`String greeting = " Hello " ;`
`String s = greeting.substring (0,3);`
### 拼接
String可以和8种基本数据类型变量做运算，但只能是连接运算 “+”
关于+的操作：如果是有String参与的，最终都是String，如果没有，则按照正常加法运算
```java
char c = 'a'; //ASCII 对应着 97
int num = 10;
String str = "Hello";

System.out.println(c + num + str); // 107Hello
System.out.println(c + str + num); // aHello10
System.out.println(c + (num + str)); // a10Hello
System.out.println((c + num) + str); // 107Hello
System.out.println(str + num + c); // Hello10a
```
注意：char 只能是一个字符，多了少了都不行。 char = 'a', char = '中'.      错误示范： char a = 'ab'； 
单引号'' 是字符类型char， 双引号 " "才是字符串
### 判断字符串是否相等
使用equals ( )或者equalsIgnoreCase（）检测两个字符串是否相等；equalsIgnoreCase不区分大小写。
一定不要使用 = 运算符检测两个字符串是否相等 ！
 这个运算符只能够确定两个字串是否放置在同一个位置上 。 当然 ， 如果字符串放置在同一个位置上 ， 它们必然相等。 但是 ，完全有可能将内容相同的多个字符串的拷贝放置在不同的位置上。
### 空串与 Null 串
空串是一个 Java 对象 ， 有自己的串长度 （ 0 ) 和内容 （ 空 ）
空串 " " 是长度为 0 的字符串。 可以调用以下代码检查一个字符串是否为空：
`if (str.length() = 0)`或`if (str.equals(""))`

String变量还可以存放一个特殊的值 ， 名为 null , 这表示目前没有任何对象与该变量关联
有时要检查一个字符串既不是 null 也不为空串， 这种情况下就需要使用以下条件 ：
`if (str != null && str.length() ! = 0)`
## StringBuilder
由于String是不可变的，每次对其进行操作都会新创建一个String对象，如果有多次的操作会很浪费资源，效率低下
于是有了StringBuilder,
创建一个字符构建器：
`StringBuilder builder = new StringBuilder( );`
当每次需要添加一部分内容时 ， 就调用 append 方法 。
`builder.append (ch) ; // appends a single character`
`builder.append (str) ; // appends a string`
在需要构建字符串时就凋用 toString 方法 ， 将可以得到一个 String 对象
`String s = builder.toString();`
## StringBuilder API
StringBuilder () 						构造一个空的字符串构建器
int length ( )							返回构建器或缓冲器中的代码单元数量
StringBuilder append ( String str )			追加一个字符串并返回 this
StringBuilder  insert ( int offset , String str )	在 offset 位置插入一个字符串并返回 this
String toString ( )						返回一个与构建器或缓冲器内容相同的字符串
## StringBuffer
这个类是StringBuilder的前身, 但效率稍有些低，线程安全，可以采用多线程的方式执行添加或删除字符的操作，其API和StringBuilder是一样的
## String，StringBuilder，StringBuffer三者关系

1. 能否修改

String		是字符串常量，一旦创建不能被修改
	StringBuilde	是字符串变量，可以被修改
	StringBuffer	是字符串变量，可以被修改

String源码中，String被final修饰，而且用于保存的是final数组。
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
....
}
```

2. 线程与效率
- 线程安全：
   - StringBuilder	属于非线程安全，用于单线程
   - StringBuffer	属于线程安全，可用于多线程
- 效率：
   - StringBuilder > StringBuffer > String 
```java
// StringBuilder类中的方法没有synchronized 锁
    @Override
    public StringBuilder append(String str) {
        super.append(str);
        return this;
    }

// StringBuffer 类中的方法都有 synchronized 
     @Override
    public synchronized StringBuffer append(String str) {
        toStringCache = null;
        super.append(str);
        return this;
    }
```

