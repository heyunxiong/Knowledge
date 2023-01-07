# 第8章 泛型程序设计
使用泛型机制编写的程序代码要比那些杂乱地使用Object 变量，
## 8.1 为什么要使用泛型程序设计
泛型程序设计（Generic programming) 意味着编写的代码可以被很多不同类型的对象所重用.为一个 ArrayList 类可以聚集任何类型的对象。这是一个泛型程序设计的实例
### 8.1.1 类型参数的好处
```java
public class ArrayList{ // before generic classes
private Object[] elementData;
public Object get(int i) { . . . }
public void add(Object o) { . . . }
}
```

- 问题1：当获取一个值时必须进行强制类型转换。

ArrayList files = new ArrayList( )；
String filename = (String) files.get(0);

- 问题2：如果将 get 的结果强制类型转换为 String 类型， 就会产生一个错误

files.add(new File(". ..");  //（因为加入的是一个File，强制转换成String会出错）


- 解决方案： 类型参数（ type parameters)

ArrayList<String> files = new ArrayList<String>(): //可读性增加，表示这个数组列表中包含的是 String 对象
当调用 get 的时候，不需要进行强制类型转换，编译器就知道返回值类型为 String
编译器还知道 ArrayList<String> 中 add 方法有一个类型为 String 的参数。编译器可以进行检査，避免插人错误类型的对象
files.add(new File(". . .")); // can only add String objects to an ArrayList<String>  //（因为规定只能包含String类型的对象，添加File类型的对象会在编译就报错）
如果只能允许前一个调用， 而不能允许后一个调用呢？ Java语言的设计者发明了一个具有独创性的新概念，通配符类型（ wildcard type)
## 8.2 定义简单泛型类
```java
public class Pair < T > {
    private T first;
    private T second;
    public Pair() {
        first = null;
        second = null;
    }
    public Pairf(T first, T second) {
    this.first = first;
    this.second = second;
}
public T getFirst() {
    return first;
}
public T getSecond() {
    return second;
}
public void setFirst(T newValue) {
    first = newValue;
}
public void setSecond(T newValue) {
    second = newValue;
}
}
```
泛型类可以有多个类型变量：
public class Pair<T, U> { . . . }
类定义中的类型变量指定方法的返回类型以及域和局部变量的类型
private T first; // uses the type variable
用具体的类型替换类型变量就可以实例化泛型类型
Pai r<String>
可以将结果想象成带有构造器的普通类
Pair<String>( )
Pair<String>(String, String)
和方法
String getFirstO
String getSecond()
void setFirst(String)
void setSecond(String)
换句话说，泛型类可看作普通类的工厂
```java
package pair1;
/**
 * @version 1.01 2012-01-26
 * @author Cay Horstmann
 */
public class PairTest1 {
    public static void main(String[] args) {
        String[] words = {"Mary", "had", "a", "little", "lamb"};
        Pair < String > mm = ArrayAlg.minmax(words);
        System.out.println("min = " + mm.getFirst());
        System.out.println("max = " + mm.getSecond());
    }
}
class ArrayAlg {
    /**
     * Gets the minimum and maximum of an array of strings.
     * @param a an array of strings
     * @return a pair with the min and max value, or null if a is null or empty
     */
    public static Pair < String > minmax(String[] a) {
        if(a == null || a.length == 0) return null;
        String min = a[0];
        String max = a[0];
        for(int i = 1; i < a.length; i++) {
            if(min.compareTo(a[i]) > 0) min = a[i];
            if(max.compareTo(a[i]) < 0) max = a[i];
        }
        return new Pair < > (min, max);
    }
}
```
## 8.3 泛型方法
带有类型参数的简单方法
```java
class ArrayAlg{
	public static <T> T getMiddle(T... a) {
		return a[a.length / 2]; 
		} 
}
```
这是一个泛型方法，注意，类型变量放在修饰符（这里是 public static) 的后面，返回类型的前面。
泛型方法可以定义在普通类中，也可以定义在泛型类中
当调用一个泛型方法时，在方法名前的尖括号中放人具体的类型（方法调用中可以省略 <String> 类型参数，编译器会自行推断）
String middle = ArrayAlg.<String>getMiddle("John", "Q.", "Public");
它用 names 的类型（即 String[ ]) 与泛型类型 T[ ]进行匹配并推断出 T 一定是 String。也就是说，可以调用
String middle = ArrayAlg.getMiddle("John", "Q.", "Public");
## 8.4 类型变量的限定
```java
class ArrayAlg
{
 public static <T> T min(T[] a) // almost correct
 {
 if (a == null || a.length == 0) return null;
 T smallest = a[0];
 for (int i = 1; i < a.length; i++)
if (smallest.compareTo(a[i]) > 0) smallest = a[i];
 return smallest;
 }
}
```
T 限制为实现了 Comparable 接口（只含一个方法 compareTo 的标准接口）的类。可以通过对类型变量 T 设置限定（bound) 实现这一点：
public static <T extends Coiparab1e> T a) . . .
实际上 Comparable 接口本身就是一个泛型类型。
现在，泛型的 min方法只能被实现了 Comparable 接口的类（如 String、 LocalDate 等）的数组调用。由于 Rectangle 类没有实现 Comparable 接口， 所以调用 min将会产生一个编译错误。

<T extends BoundingType>
表示 T 应该是绑定类型的子类型 （subtype)。 T 和绑定类型可以是类， 也可以是接口。一个类型变量或通配符可以有多个限定， 例如： T extends Comparable & Serializable（T需要是同时实现（Comparable和Serializable，这两个是接口）的类/接口）
限定类型用“ &” 分隔(即表示要同时满足)，而逗号用来分隔类型变量（即： T extends Comparable, U extends Serializable）。
在 Java 的继承中， 可以根据需要拥有多个接口超类型， 但限定中至多有一个类。如果用一个类作为限定，它必须是限定列表中的第一个。（即： T extends class1 & class2，这么写可以，但是class1才能作为限定，class2失效）
```java
package pair2;
import java.time.*;
/**
 * @version 1.02 2015-06-21
 * @author Cay Horstmann
 */
public class PairTest2 {
    public static void main(String[] args) {
        LocalDate[] birthdays = {
            LocalDate.of(1906, 12, 9), // G. Hopper
                LocalDate.of(1815, 12, 10), // A. Lovelace
                LocalDate.of(1903, 12, 3), // J. von Neumann
                LocalDate.of(1910, 6, 22), // K. Zuse
        };
        Pair < LocalDate > mm = ArrayAlg.minmax(birthdays);
        System.out.println("min = " + mm.getFirst());
        System.out.println("max = " + mm.getSecond());
    }
}
class ArrayAlg {
    /**
    Gets the minimum and maximum of an array of objects of type T.
    @param a an array of objects of type T
    @return a pair with the min and max value, or null if a is 
    null or empty
    */
    public static < T extends Comparable > Pair < T > minmax(T[] a) {
        if(a == null || a.length == 0) return null;
        T min = a[0];
        T max = a[0];
        for(int i = 1; i < a.length; i++) {
            if(min.compareTo(a[i]) > 0) min = a[i];
            if(max.compareTo(a[i]) < 0) max = a[i];
        }
        return new Pair < > (min, max);
    }
}
```
## 8.5 泛型代码和虚拟机
### 8.5.1 类型擦除
无论何时定义一个泛型类型， 都自动提供了一个相应的原始类型 （ raw type )。原始类型的名字就是删去类型参数后的泛型类型名。擦除（ erased）类型变M, 并替换为限定类型（无限定的变量用 Object）。
```java
//Pair<T> 的原始类型如下所示：因为 T 是一个无限定的变量， 所以直接用 Object 替换。
public class Pair{
private Object first;
private Object second;
public Pair(Object first, Object second) {
this,first = first;
this.second = second;
public Object getFirstO { return first; }
public Object getSecondO { return second; }
public void setFirst(Object newValue) { first = newValue; }
public void setSecond(Object newValue) { second = newValue; }
}
```
原始类型用第一个限定的类型变量来替换，假定声明了一个不同的类型。
```java
public class Interval<T extends Comparable & Serializable> implements Serializable
{
 private T lower;
 private T upper;
 . . .
 public Interval(T first, T second)
 {
 if (first.compareTo(second) <= 0) { lower = first; upper = second; }
 else { lower = second; upper = first; }
 }
}

//原始类型 Interval 如下所示：使用了Comparable
public class Interval implements Serializable
{
 private Comparable lower;
 private Comparable upper;
 . . .
 public Interval(Comparable first, Comparable second) { . . . }
}
```
注意：读者可能想要知道切换限定： class Interval<T extends Serializable & Comparable>会发生什么。如果这样做， 原始类型用 Serializable 替换 T, 而编译器在必要时要向Comparable 插入强制类型转换。为了提高效率，应该将标签（tagging) 接口（即没有方法的接口）放在边界列表的末尾。
### 8.5.2 翻译泛型表达式
当程序调用泛型方法时，如果擦除返回类型， 编译器插入强制类型转换
Pair<Employee> buddies = . .
Employee buddy = buddies.getFirst( )；
擦除 getFirst 的返回类型后将返回 Object 类型。编译器自动插人 Employee 的强制类型转换。也就是说，编译器把这个方法调用翻译为两条虚拟机指令： 

- 对原始方法 Pair.getFirst 的调用。 
- 将返回的 Object 类型强制转换为 Employee 类型。

当存取一个泛型域时也要插人强制类型转换。Employee buddy = buddies.first;也会在结果字节码中插人强制类型转换
### 8.5.3 翻译泛型方法
普通的泛型方法
public static <T extends Comparable> T min(T[ ]  a)
擦除后，只剩下Comparable限定类型
public static Comparable min(Comparable[ ] a)

方法的擦除带来的问题：
```java
class DateInterval extends Pair<LocalDate>
{
 public void setSecond(LocalDate second)
 {
 if (second.compareTo(getFirst()) >= 0)
super.setSecond(second);
 }
 . . .
}
//类型擦除后
class DateInterval extends Pair // after erasure
{
 public void setSecond(LocalDate second) { . . . }
 . . .
}
```
在 Pair 内有一个setSecond方法，即public void setSecond(Object second)对于如下执行语句
DateInterval interval = new DateInterval(. . .);
Pair<LocalDate> pair = interval; // OK--assignment to superclass
pair.setSecond(aDate);
这里， 希望对 setSecond 的调用具有多态性， 并调用最合适的那个方法。由于 pair 引用Datelnterval 对象，所以应该调用 Datelnterval.setSecond（父类引用会先调用自己里面没有的，因为 Datelnterval.setSecond的参数LocalDate, Pai自己的是Object参数。）。问题在于类型擦除与多态发生了冲突（调用 Datelnterval.setSecond后擦除了）
Datelnterval 类中生成一个桥方法（bridge method):
public void setSecond(Object second) { setSecond((Date) second); }
对于；pair.setSecond(aDate)变量 pair 已经声明为类型 Pair<LocalDate>, 并且这个类型只有一个简单的方法叫setSecond， 即 setSecond(Object) 。
虚拟机用 pair 引用的对象调用这个方法。这个对象是Datelnterval 类型的， 因而将会调用 Datelnterval.setSecond(Object)方法。这个方法是合成的桥方法。它调用Datelnterval.setSecond(Date)， 这正是我们所期望的操作效果。

有关 Java 泛型转换的事实： 

- 虚拟机中没有泛型，只有普通的类和方法。 
- 所有的类型参数都用它们的限定类型替换。 
- 桥方法被合成来保持多态。 
- 为保持类型安全性，必要时插人强制类型转换。

### 8.5.4 调用遗留代码
设计 Java 泛型类型时，主要目标是允许泛型代码和遗留代码之间能够互操作
## 8.6 约束与局限性
### 8.6.1 不能用基本类型实例化类型参数
不能用类型参数代替基本类型。因此， 没有 Pair<double>, 只 有 Pair<Double>。
### 8.6.2 运行时类型查询只适用于原始类型
虚拟机中的对象总有一个特定的非泛型类型。因此，所有的类型查询只产生原始类型。
测试 obj 是否是任意类型的一个 Pair
if (obj instanceof Pair<String>) // Error
if (obj instanceof Pair<T>) // Error
或强制类型转换：
Pair<String> p = (Pair<String>) obj; // Warning-can only test that obj is a  Pair
试图查询一个对象是否属于某个泛型类型时，倘若使用 instanceof 会得到一个编译器错误， 如果使用强制类型转换会得到一个警告
getClass 方法总是返回原始类型
Pair<String> stringPair = . .
Pair <Employee> employeePair = . .
if (stringPair.getClass( ) == employeePair.getClass( ) ) // they are equal
其比较的结果是 true, 这是因为两次调用 getClass 都将返回 Pair.class。
### 8.6.3 不能创建参数化类型的数组
不能实例化参数化类型的数组，
Pair<String>[ ] table = new Pair<String>[10]; // Error
类型擦除后为 Pair[ ] table = new Pair[10];可以把它转换为 Object[ ] :
Object[ ] objarray = table;
数组会记住它的元素类型， 如果试图存储其他类型的元素， 就会抛出一个 ArrayStoreException 异常：
objarray [0] = "Hello"; // Error component type is Pair
声明类型为 Pair<String>[ ] 的变量仍是合法的。不过不能用 new Pair<String>[10] 初始化这个变量
### 8.6.4 Varargs 警告
向参数个数可变的方法传递一个泛型类型的实例，实际上参数 **ts **是一个数组， 包含提供的所有实参。
```java
public static <T> void addAll(Collection<T> coll, T... ts){
 	for (t : ts) coll.add(t);
}
//调用
Collection<Pair<String>> table = . . .;
Pair<String> pair1 = . . .;
Pair<String> pair2 = . . .;
addAll(table, pair1, pair2);
```
为了调用这个方法，Java 虚拟机必须建立一个 Pair<String> 数组， 这就违反了前面的规则（传入了两个 Pair对象，而不是数组）
只会得到一个警告，而不是错误。可以采用两种方法来抑制这个警告。
一种方法是为包含 addAll 调用的方法增加注解 @SuppressWamings("unchecked") 
或者在 Java SE 7中， 还 可 以 用@SafeVarargs 直 接 标 注addAll 方法：
`@SafeVarargs`
`public static <T> void addAll(Collection<T> coll, T... ts)`
### 8.6.5 不能实例化类型变量
不能使用像 new T(...) newT[...] 或 T.class 这样的表达式中的类型变量
public static <T extends Comparable> T[] minmax(T[] a) { T[] mm = new T[2]; . . . } // Error
### 8.6.6 不能构造泛型数组
就像不能实例化一个泛型实例一样， 也不能实例化数组。
public static <T extends Comparable> T[] minmax(T[] a) { T[] mm = new T[2]; . . . } // Error
### 8.6.7 泛型类的静态上下文中类型变量无效
不能在静态域或方法中引用类型变量
```java
public class Singleton<T>
{
 private static T singleInstance; // Error
 public static T getSingleInstance() // Error
 {
 if (singleInstance == null) // construct new instance of T
 return singleInstance;
 }
}
```
### 8.6.8 不能抛出或捕获泛型类的实例
既不能抛出也不能捕获泛型类对象。实际上， 甚至泛型类扩展 **Throwable **都是不合法的
public class Problem<T> extends Exception { /* . . . */ } // Error--can't extend Throwable
### 8.6.9 可以消除对受查异常的检查
Java 异常处理的一个基本原则是， 必须为所有受查异常提供一个处理器。不过可以利用泛型消除这个限制
```java
@SuppressWarnings("unchecked")
public static <T extends Throwable> void throwAs(Throwable e) throws T 
{
 throw (T) e;
}
```
### 8.6.10 注意擦除后的冲突
当泛型类型被擦除时， 无法创建引发冲突的条件
## **8.7 **泛型类型的继承规则
考虑一个类和一个子类， 如 **Employee **和 **Manager**。
**Pair**<**Manager**> 是**PaiKEmployee**> 的一个子类吗？不是！
![image.png](_assets/「Java核心技术」第8章%20泛型程序设计/1600500001120-4c706566-e950-4fe2-8089-d3db821946f0.png)

## 8.8 通配符类型
### 8.8.1 通配符概念
通配符类型Pair<? extends Employee>表示任何泛型 Pair 类型， 它的类型参数是 Employee 的子类， 如 Pair<Manager>， 但不是Pair<String>
public static void printBuddies(Pair<? extends Eiployee> p)类型 Pair<Manager> 是 Pair<? extends Employee> 的子类型
![image.png](_assets/「Java核心技术」第8章%20泛型程序设计/1600500144601-dc566eb7-27cd-462e-9373-9796726295d7.png)

### 8.8.2 通配符的超类型限定
超类限定符：` ? super Manager`  这个通配符限制为 Manager 的所有超类型
直观地讲，带有超类型限定的通配符可以向泛型对象写人，带有子类型限定的通配符可
以从泛型对象读取。
### 8.8.3 无限定通配符
使用无限定的通配符， 例如，**Pair**<?>。这好像与原始的 **Pair **类型一样。
Pari<?> 方法
? getFirst()
void setFirst(?)
区别：可以用任意 **Object **对象调用原始 **Pair **类的 **setObject**方法。

### 8.8.4 通配符捕获
编写一个交换成对元素的方法：public static void swap(Pair<?> p)
通配符不是类型变量， 因此， 不能在编写代码中使用“ ？” 作为一种类型。 也就是说， 下述代码是非法的：
```java
? t = p.getFirst(); // Error
p.setFirst(p.getSecond());
p.setSecond(t);
```



