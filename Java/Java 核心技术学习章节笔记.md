# 第 7 章异常、断言和曰志

**Author:** Yunxiong  

## 7 . 1 处 理 错 误
异常处理的任务就是将控制权从错误产生的地方转移给能够处理这种情况的错误处理器

在 Java 中， 如果某个方法不能够采用正常的途径完整它的任务，就可以通过另外一个路径退出方法。在这种情况下，方法并不返回任何值， 而是抛出
( throw) 一个封装了错误信息的对象。需要注意的是，这个方法将会立刻退出，并不返回任何值。 此外， 调用这个方法的代码也将无法继续执行，取而代之的是， 异常处理机制开始搜
索能够处理这种异常状况的异常处理器 （exception handler )

## 7.1.1 异常分类
在 Java 程序设计语言中， 异常对象都是派生于 Throwable 类的一个实例  
![](_assets/Java%20核心技术学习章节笔记/image-Java%20核心技术学习章节笔记-20221017-152755348.png)

Error 类层次结构描述了 Java 运行时系统的内部错误和资源耗尽错误。 应用程序不应该抛出这种类型的对象。 如果出现了这样的内部错误， 除了通告给用户，并尽力使程序安全地终止之外， 再也无能为力了。这种情况很少出现。
在设计 Java 程序时， 需要关注 Exception 层次结构。 这个层次结构又分解为两个分支：
一个分支派生于 RuntimeException ; 
另一个分支包含其他异常。

划分两个分支的规则是： 由程序错误导致的异常属于 RuntimeException ; 而程序本身没有问题， 但由于像 I/O 错误这类问题导致的异常属于其他异常:

派生于 RuntimeException 的异常包含下面几种情况：
•错误的类型转换。
•数组访问越界 i
•访问 null 指针

不是派生于 RuntimeException 的异常包括：
•试图在文件尾部后面读取数据。
•试图打开一个不存在的文件。
•试图根据给定的字符串查找 Class 对象， 而这个字符串表示的类并不存在,，

**如果出现 RuntimeException 异常， 那么就一定是你的问题**

Java 语 言 规 范 将 派 生 于 Error 类 或 RuntimeException 类的所有异常称为非受查( unchecked ) 异常， 所有其他的异常称为受查（checked) 异常。
继承Error类和RuntimeException类的就是非受检查异常，像什么i/o异常， FileNotFoundException, EOFException属于受检查异常

方法上声明抛出异常  
```java
public Fi1elnputStream(String name) throws FileNotFoundException
```

什么异常必须使用 throws 子句声明， 需要记住在遇到下面 4 种情况时应该抛出异常：
1 ) 调用一个抛出受査异常的方法， 例如， FilelnputStream 构造器。
2 ) 程序运行过程中发现错误， 并且利用 throw语句抛出一个受查异常
3 ) 程序出现错误， 例如，a[-l]=0 会抛出一个 ArraylndexOutOffloundsException 这样的非受查异常
4 ) Java 虚拟机和运行时库出现的内部错误。

一个方法必须声明所有可能抛出的受查异常， 而非受查异常要么不可控制（ Error),要么就应该避免发生 （ RuntimeException )
如果在子类中覆盖了超类的一个方法， 子类方法中声明的受查异常不能比超类方法中声明的异常更通用，
父类的方法如果是protected级别。那么子类的方法不能是public，只能是protected，private

## 7.1.3 如何抛出异常
- throws 放在方法声明那里
- throw 抛出一个异常实例 

在前面已经看到， 对于一个已经存在的异常类， 将其抛出非常容易 D 在这种情况下：
1 ) 找到一个合适的异常类。
2 ) 创建这个类的一个对象。
3 ) 将对象抛出。
一旦方法抛出了异常， 这个方法就不可能返回到调用者。也就是说， 不必为返回的默认值或错误代码担忧。

## 7.1.4 创建异常类
创建自己的异常类就是一件顺理成章的事情了。我们需要做的只是定义一个派生于Exception 的类，或者派生于 Exception 子类的类。
```java
class FileFormatException extends IOException{
	public FileFormatExceptionO {}
	public FileFormatException(String gripe){
		super(gripe);
	}
}
```

# 7 . 2 捕获异常
7 . 2.1 捕获异常
如果在 try语句块中的任何代码抛出了一个在 catch 子句中说明的异常类， 那么
1 ) 程序将跳过 try语句块的其余代码。
2 ) 程序将执行 catch 子句中的处理器代码
如果在 try 语句块中的代码没有拋出任何异常，那么程序将跳过 catch 子句。
如果方法中的任何代码拋出了一个在 catch 子句中没有声明的异常类型，那么这个方法就会立刻退出

请记住， 编译器严格地执行 throws 说明符。 如果调用了一个抛出受查异常的方法，就必须对它进行处理， 或者继续传递。
哪种方法更好呢？ 通常， 应该捕获那些知道如何处理的异常， 而将那些不知道怎样处理的异常继续进行传递
如果想传递一个异常， 就必须在方法的首部添加一个 throws 说明符， 以便告知调用者这个方法可能会抛出异常。

  
```java

InputStream in = new FileInputStream(. . .);

try{

// code that might throw exceptions

}catch (IOException e){

//  show error message

}finally{
	in.doseO；
}
```
  
1 ) 代码没有抛出异常。 在这种情况下， 程序首先执行 try 语句块中的全部代码，然后执行 finally 子句中的代码t 随后， 继续执行 try 语句块之后的第一条语句。也就是说，执行标注的 1、 2、 5、 6 处。
2 ) 抛出一个在 catch 子句中捕获的异常。在上面的示例中就是 IOException 异常。在这种情况下，程序将执行 try语句块中的所有代码，直到发生异常为止。此时，将跳过 try语句块中的剩余代码， 转去执行与该异常匹配的 catch 子句中的代码， 最后执行 finally 子句中的代码。
如果 catch 子句没有抛出异常， 程序将执行 try 语句块之后的第一条语句。在这里，执行标注 1、 3、 4、5、 6 处的语句。
如果 catch 子句抛出了一个异常， 异常将被抛回这个方法的调用者。在这里， 执行标注1、 3、 5 处的语句。
3 ) 代码抛出了一个异常， 但这个异常不是由 catch 子句捕获的。在这种情况下， 程序将执行 try 语句块中的所有语句，直到有异常被抛出为止。此时， 将跳过 try 语句块中的剩余代码， 然后执行 finally子句中的语句， 并将异常抛给这个方法的调用者。在这里， 执行标注 1、
5 处的语句try 语句可以只有 finally 子句，而没有 catch 子句
当 finally 子句包含 return 语句时， 将会出现一种意想不到的结果„ 假设利用 return语句从 try语句块中退出。在方法返回前， finally 子句的内容将被执行。如果 finally 子句中
也有一个 return 语句， 这个返回值将会覆盖原始的返回值。请看一个复杂的例子：

```JAVA
public static int f(int n){
	try{
		int r = n * n;
		return r;
	}finally{
		if (n = 2) return 0;
	}
}
```

如果调用 f(2), 那么 try 语句块的计算结果为 r = 4, 并执行 return 语句然而，在方法真
正返回前，还要执行 finally 子句。finally 子句将使得方法返回 0, 这个返回值覆盖了原始的返回值 4。


7.2.5 带资源的 try 语句
带资源的 try 语句（try-with-resources) 的最简形式为：

try (Resource res = . . .){
work with res
}

try块退出时，会自动调用 res.doseO。

只要需要关闭资源， 就要尽可能使用带资源的 try语句

7.2.6 分析堆栈轨迹元素

堆栈轨迹（ stack trace ) 是一个方法调用过程的列表， 它包含了程序执行过程中方法调用的特定位置

7.3 使用异常机制的技巧
1. 异常处理不能代替简单的测试
2. 不要过分地细化异常
3. 利用异常层次结构
	不要只抛出 RuntimeException 异常。应该寻找更加适当的子类或创建自己的异常类。
	不要只捕获 Thowable 异常， 否则，会使程序代码更难读、 更难维护。
4. 不要压制异常
5. 在检测错误时，“ 苛刻” 要比放任更好
6. 不要羞于传递异常
5和6归结为 ： 早抛出，晚捕获

7.4 使用断言
断言机制允许在测试期间向代码中插入一些检査语句。当代码发布时，这些插人的检测
语句将会被自动地移走
Java 语言引人了关键字 assert。//在开发的过程中用到的，上线就移除了
这个关键字有两种形式：
assert 条件；
assert 条件：表达式；
如果结果为 false, 则抛出一个 AssertionError 异常。

7.4.2 启用和禁用断言
在默认情况下， 断言被禁用。可以在运行程序时用 -enableassertions 或 -ea 选项启用：java -enableassertions MyApp

也可以在某个类或整个包中使用断言， 例如：java -ea:MyClass -eaiconi.inycompany.inylib.. , MyApp

这条命令将开启 MyClass 类以及在 com.mycompany.mylib 包和它的子包中的所有类的断言。选项 -ea 将开启默认包中的所有类的断言
也可以用选项 -disableassertions 或 -da 禁用某个特定类和包的断言：
java -ea:... -da:MyClass MyApp

7.4.3 使用断言完成参数检查
在 Java 语言中， 给出了 3 种处理系统错误的机制：
•抛出一个异常
•日志
•使用断言
什么时候应该选择使用断言呢？ 请记住下面几点：
•断言失败是致命的、 不可恢复的错误。
•断言检查只用于开发和测阶段

断言是一种测试和调试阶段所使用的战术性工具

7.5 记录曰志
如果对 com.mycompany 日志记录器设置了日志级别，
它的子记录器也会继承这个级别 ，通常， 有以下 7 个日志记录器级别：
• SEVERE
• WARNING
• INFO
• CONFIG
• FINE
• FINER
• FINEST

# 8.1 为什么要使用泛型程序设计

**Author:** Yunxiong  

8.1 为什么要使用泛型程序设计

泛型程序设计（Generic programming) 意味着编写的代码可以被很多不同类型的对象所重用

类型参数的魅力在于：使得程序具有更好的可读性和安全性

8.1.1 类型参数化

未使用泛型

```JAVA
public class ArrayList // before generic classes

private Object[] elementData;

public Object get(int i) { . . , }

public void add(Object o) { . . . }

}
```

这种方法有两个问题。当获取一个值时必须进行强制类型转换。

ArrayList files = new ArrayListO；

String filename = (String) files.get(O);

此外，这里没有错误检査。可以向数组列表中添加任何类的对象。

files,add(new File(". .

对于这个调用，编译和运行都不会出错。然而在其他地方， 如果将 get 的结果强制类型

转换为 String 类型， 就会产生一个错误。

使用泛型

ArrayList<String> files = new ArrayList<String>()
通配符类型
8.2 泛型类
简单的泛型类
```JAVA
public class Pair<T>
{

private T first;

private T second;

public Pair() { first = null ; second = null ; }

public PairfT first, T second) { this,first = first; this.second = second; }

public T getFirstO { return first; }

public T getSecondO { return second; }

public void setFirst(T newValue) { first = newValue; }

public void setSecond(T newValue) { second = newValue; }

}
```
  

8.3 泛型方法
class ArrayAlg{
public static <T> T getMiddle(T... a){
return a[a.length / 2];
}
}

这个方法是在普通类中定义的， 而不是在泛型类中定义的。然而，这是一个泛型方法，

可以从尖括号和类型变量看出这一点。注意，类型变量放在修饰符（这里是 public static) 的后面，返回类型的前面。
当调用一个泛型方法时’在方法名前的尖括号中放人具体的类型：

String middle = ArrayAlg.<String>getMiddle("]ohnM, "Q.n, "Public");
在这种情况（实际也是大多数情况）下，方法调用中可以省略 <String> 类型参数。编译器有足够的信息能够推断出所调用的方法。
8.5  泛型代码和虚拟机

8.5。1 类型擦除
无论何时定义一个泛型类型， 都自动提供了一个相应的原始类型 （ raw type)。原始类型的名字就是删去类型参数后的泛型类型名。擦除（ erased) 类型变M , 并替换为限定类型
应该将标签（tagging) 接口（即没有方法的接口）放在边界列表的末尾。
8.5.2

当程序调用泛型方法时， 如果擦除返回类型， 编译器插入强制类型转换。例如，下面这个语句序列

Pair<Employee> buddies = . .Employee buddy = buddies.getFirstO；

擦除 getFirst 的返回类型后将返回 Object 类型。编译器自动插人 Employee 的强制类型转换。也就是说，编译器把这个方法调用翻译为两条虚拟机指令：

•对原始方法 Pair.getFirst 的调用。

•将返回的 Object 类型强制转换为 Employee 类型。

当存取一个泛型域时也要插人强制类型转换

8 . 5.3 翻译泛型方法

类型擦除也会出现在泛型方法中。程序员通常认为下述的泛型方法

public static <T extends Comparable〉T nrin(T[] a)

是一个完整的方法族，而擦除类型之后， 只剩下一个方法：

public static Comparable min(Comparable!] a)

注意， 类型参数 T 已经被擦除了， 只留下了限定类型 Comparable。

  

Datelnterval interval = new Datelnterval(. . .);

Pair<Loca1Date> pair = interval; // OK assignment to superclass

pair.setSecond(aDate);

希望对 setSecond 的调用具有多态性， 并调用最合适的那个方法。 由于 pair 引用

Datelnterval 对象，所以应该调用 Datelnterval.setSecond。问题在于类型擦除与多态发生了冲

突。要解决这个问题， 就需要编译器在 Datelnterval 类中生成一个桥方法 （bridge method):

public void setSecond(Object second) { setSecond((Date) second); J

要想了解它的工作过程， 请仔细地跟踪下列语句的执行：

pair.setSecond(aDate

总之，需要记住有关 Java 泛型转换的事实：

•虚拟机中没有泛型，只有普通的类和方法。

•所有的类型参数都用它们的限定类型替换。

•桥方法被合成来保持多态。

•为保持类型安全性，必要时插人强制类型转换

8.6 约束与局限性
8.6.1 不能用基本类型实例化类型参数

基本类型 ：byte  char short int long float double boolean 

没有 Pair<double>, 只 有 Pair<Double>。 当然,

其原因是类型擦除。擦除之后， Pair 类含有 Object 类型的域， 而 Object 不能存储 double 
8.6.2 运行时类型查询只适用于原始类型

Pair<String> stringPair = . .
Pai「< Employee〉employeePair = . .
if (stringPair.getClassO == employeePair.getClassO) // they are equal
其比较的结果是 true, 这是因为两次调用 getClass 都将返回 Pair.class 。

8.6.3 不能创建参数化类型的数组

不能实例化参数化类型的数组， 例如：

Pair<String>[] table = new Pair<String>[10]; // Error

8.6.4 Varargs 警告

向参数个数可变的方法传递一个泛型类型的实例。
public static <T> void addAll(Collections coll, T... ts)
{
for (t : ts) coll.add⑴；
}

public static <T> void addAll(Collections coll, T... ts)

{

for (t : ts) coll.add⑴；

}

应该记得，实际上参数 ts 是一个数组， 包含提供的所有实参。

现在考虑以下调用：

Col1ection<Pair<String» table = . . .;

Pair<String> pairl = . . .;

Pair<String> pair2 = . .

addAll (table, pairl, pair2);

  

  

为了调用这个方法，Java 虚拟机必须建立一个 Pair<String> 数组， 这就违反了前面的规

则 --不能实例化泛型数组

  

  

  

8.6.5 不能实例化类型变置

不能使用像 new T(...，) newT[...] 或 T.class 这样的表达式中的类型变量。 例如， 下面的

Pair<T> 构造器就是非法的：

public Pair() { first = new T(); second = new T(); } // Error

Class类本身是泛型。 例如，String.daSS 是一个 Class<String> 的实例（事实上，

它是唯一的实例。

  

8.6.6 不能构造泛型数组

  

public static <T extends Comparable〉T[] minmax(T[] a) { T:D 刪 = new T[2]; . . . } // Error

类型擦除会让这个方法永远构造 Comparable[2] 数组。

  

8.6.7 泛型类的静态上下文中类型变量无效

  

不能在静态域或方法中引用类型变量

  

public class Singleton<T>

{

private static T singlelnstance; // Error

public static T getSinglelnstanceO // Error

{

if (singleinstance == null) construct new instance of T

return singlelnstance;

}

}

禁止使用带有类型变量

的静态域和方法

  

8.6.8 不能抛出或捕获泛型类的实例

既不能抛出也不能捕获泛型类对象。实际上， 甚至泛型类扩展 Throwable 都是不合法的。

  

public class Problem<T> extends Exception { /* . . . */ } // Error can't extend Throwable

  

catch 子句中不能使用类型变量

  

public static <T extends Throwable〉 void doWork(Class<T> t)

{

try

{

do work

}

**catch (T e) // Error can't catch type variable**

{

Logger,global.info(...)

}

}

  

不过， 在异常规范中使用类型变量是允许的。以下方法是合法的：

public static <T extends Throwable〉void doWork(T t) throws T // OK

  

  

  

8 . 6.9 可以消除对受查异常的检查

Java 异常处理的一个基本原则是， 必须为所有受查异常提供一个处理器。不过可以利用

泛型消除这个限制

  

通过使用泛型类、 擦除和@SuppressWamings 注解， 就能消除 Java 类型系统的部分基本

限制

  

  

8 . 6.1 0 注意擦除后的冲突

  

当泛型类型被擦除时， 无法创建引发冲突的条件

  

泛型规范说明还提到另外一个原则：“ 要想支持擦除的转换， 就需要强行限制一个类或类

型变量不能同时成为两个接口类型的子类， 而这两个接口是同一接口的不同参数化

  

例如，

下述代码是非法的：

class Employee implements Coinparab1e<Emp1oyee> { . . . }

class Manager extends Employee implements Comparable<Hanager>

{ . . . } // Error

Manager 会实现 Comparable<Employee> 和 Comparable<Manager>, 这是同一接口的不同

参数化。

  

  

  

8.7 泛型类型的继承规则

考虑一个类和一个子类， 如 Employee 和 Manager。Pair<Manager> 是

PaiKEmployee> 的一个子类吗？ 答案是“ 不是”，

无论 S 与 T 有什么联系 （如图 8-1 所示，) 通常， PaiKS> 与 Pair<T> 没有什么联系。

![](_assets/Java%20核心技术学习章节笔记/image-Java%20核心技术学习章节笔记-20221017-153623744.png)
![](_assets/Java%20核心技术学习章节笔记/image-Java%20核心技术学习章节笔记-20221017-153640967.png)

8 . 8 通 配 符 类 型

  

  

直观地讲，带有超类型限定的通配符可以向泛型对象写人，带有子类型限定的通配符可

以从泛型对象读取。

---
# 9.4 视图与包装器

**Author:** Yunxiong  

9.4 视图与包装器  

  

  

Collections 类 ， Collection接口， 

Collections  有个s，说明是class  

  

keySet 方法返回一个实现 Set  
接口的类对象， 这个类的方法对原映射进行操作。这种集合称为视图。  
  

9.4.1  轻量级集合包装器  
  

Arrays.asList()  

Arrays 类的静态方法 asList 将返回一个包装了普通 Java 数组的 List 包装器。这个方法可  
以将数组传递给一个期望得到列表或集合参数的方法。例如：  
Card[] cardOeck = new Card[52];  
List<Card> cardList = Arrays.asList(cardDeck):  
返回的对象不是 ArrayList。它是一个视图对象， 带有访问底层数组的 get 和 set方  
法。改变数组大小的所有方法（例如，与迭代器相关的 add 和 remove 方法）都会抛出一个  
Unsupported OperationException 异常  
  

  

9.4.2 子范围 subrange  

  

List group2 = staff.subList(10, 20) ;   10<=n<20  
  

SortedSet< E> subSet(E from, E to)  
SortedSet< E> headSet(E to)  
SortedSet< E> tail Set(E from)  
这些方法将返回大于等于 from 且小于 to 的所有元素子集。有序映射也有类似的方法：  
SortedMap< K, V> subMap(K from, K to)  
SortedMap<K, V> headMap(K to)  
So「tedMap<K, V> tail Map(K from)  
返回映射视图， 该映射包含键落在指定范围内的所有元素。  
Java SE 6 引人的 NavigableSet 接口赋予子范围操作更多的控制能力。可以指定是否包括  
边界：  
NavigableSet<E> subSet ( E from, boolean fromlnclusive, E to, boolean tolnclusive)  
NavigableSet<E> headSet(E to, boolean tolnclusive)  
Navigab1eSet<E> tail Set(E from, boolean fromlnclusive)  
  

  

9.4.3 不可修改的视图  --- 视图无法修改原本集合的内容，例如add方法，会抛出  
Collections 还有几个方法， 用于产生集合的不可修改视图 （ unmodifiable views)。这些视  
图对现有集合增加了一个运行时的检查。如果发现试图对集合进行修改， 就抛出一个异常UnsupportedOperationException  
  
同时这个集合将保持未修改的状态。  
可以使用下面 8 种方法获得不可修改视图：  
Coll ecti ons. unmodi fi abl eColl ection  
Collections.unmodifiableList  
Collections.unmodifiableSet  
Collections.unmodifiableSortedSet  
Collections.unmodifiableNavigableSet  
Collections.unmodifiableMap  
Collections.unmodifiableSortedMap  
Collections.unmodifiableNavigableMap  
每个方法都定义于一个接口。 例如， Collections.unmodifiableList 与 ArrayList、 LinkedList  
或者任何实现了 List 接口的其他类一起协同工作。  
  

9.4.4 同步视图  

保证多个线程下同时访问集合不会被破坏  

Map<String, Employee〉map = Collections.synchronizedMap(new HashMap<String, Employee>0；)  
  

  

9.4.5 受检查视图  

受査” 视图用来对泛型类型发生问题时提供调试支持  
List<String> safestrings = Collections.checkedList(strings， String,class);  
  

  

9.4.6 关于可选操作的说明  

通常， 视图有一些局限性， 即可能只可以读、 无法改变大小、只支持删除而不支持插入，这些与映射的键视图情况相同。如果试图进行不恰当的操作，受限制的视图就会抛出一个 UnsupportedOperationException。  
  

  

  

  

  

# 9.3 映射 Map

**Author:** Yunxiong  

  

9.3.1 映射的基本操作  

Java 类库为映射提供了两个通用的实现：HashMap 和 TreeMap 。这两个类都实现了 Map 接口。  
散列映射对键进行散列， 树映射用键的整体顺序对元素进行排序， 并将其组织成搜索  
树。散列或比较函数只能作用于键。与键关联的值不能进行散列或比较。  
应该选择散列映射还是树映射呢？ 与集一样， 散列稍微快一些， 如果不需要按照排列顺  
序访问键， 就最好选择散列

  

  
 键必须是唯一的。不能对同一个键存放两个值。 如果对同一个键两次调用 put 方法，第二个值就会取代第一个值。实际上，put 将返回用这个键参数存储的上一个值  
要迭代处理映射的键和值 ， 最容易的方法是使用 forEach 方法。可以提供一个接收键和值的 lambda 表达式。映射中的每一项会依序调用这个表达式。  
scores•forEach((k, v) ->

     System.out.println("key=" + k + ", value:" + v)) ;  
  

  

9.3.2 更新映射项  
处理映射时的一个难点就是更新映射项。正常情况下， 可以得到与一个键关联的原值，  
完成更新， 再放回更新后的值。不过，必须考虑一个特殊情况， 即键第一次出现。getOrDefault (word, 0), 如果word对应的值不存在，本来默认是返回null，现在指定是0  
  
  

9.3.3 映射视图 keySet，entrySet  

有 3 种视图： 键集、 值集合（不是一个集） 以及键 / 值对集  
  

键集 keySet  

键/值 entrySet  

  

  

  

  

9.3.4 弱散列映射 WeakHashMap  

  

WeakHashMap 使用弱引用 （weak references) 保存键。  
WeakReference 对象将引用保存到另外一个对象中， 在这里， 就是散列键。对于这种类型的  
对象， 垃圾回收器用一种特有的方式进行处理。通常， 如果垃圾回收器发现某个特定的对象  
已经没有他人引用了， 就将其回收。然而， 如果某个对象只能由 WeakReference 引用， 垃圾  
回收器仍然回收它，但要将引用这个对象的弱引用放人队列中。WeakHashMap 将周期性地检  
查队列， 以便找出新添加的弱引用。一个弱引用进人队列意味着这个键不再被他人使用， 并  
且已经被收集起来。于是， WeakHashMap 将删除对应的条目  
  

9.3.5 链接散列集与映射 LinkedHashSet 和 LinkedHashMap  
  

  

9.3.6 枚举集和映射  EmimSet EnumMap  

  

EmimSet 是一个枚举类型元素集的高效实现  
EnumSet 类没有公共的构造器  可以使用静态工厂方法构造这个集：  
enum Weekday { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY };  
EnumSet<Weekday> always = EnumSet.allOf(Weekday.class);  
EnumSet<Weekday> never = EnumSet.noneOf(Weekday.cl ass);  
EnumSet<Weekday> workday = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);  
EnumSet<Weekday> mwf = EnumSet.of(Weekday.MONDAY, Weekday.WEDNESDAY, Weekday.FRIDAY);  
  

  

EnumMap 是一个键类型为枚举类型的映射。它可以直接且高效地用一个值数组实现。在使用时， 需要在构造器中指定键类型：  
EnumMap<Weekday, Employee〉 personlnCharge = new EnumMapo(Weekday.class);  
  

  

9.3.7 标识散列映射 IdentityHashMap  
类 IdentityHashMap 有特殊的作用。在这个类中， 键的散列值不是用 hashCode 函数计算  
的， 而是用 System.identityHashCode 方法计算的。

而且， 在对两个对象进行比较时， IdentityHashMap 类 使用 ==, 而不使用 equals 也就是说， 不同的键对象， 即使内容相同， 也被视为是不同的对象。

---
# 9.2 具体的集合

**Author:** Yunxiong  

// 黑色是普通笔记，红色是重点，蓝色是摘录别处，紫色是了解，灰色的代码，橙色的自己的理解，  

  

9.2.1 链表  

数组和数组列表都有一个重大的缺陷，这就是从数组的中间位置删除一个元素要付出很大的代价，其原因是数组中处于被删除元素之后的所有元素都要向数组的前端移动，在数组中间插入一个元素也是如此 ，链表能解决这个问题  

链表的每个结点都存放着下一个结点的引用，java中，所有链表都是**双向链接**的 - 即每个结点还存放着指向前驱结点的引用  

![](_assets/Java%20核心技术学习章节笔记/image-Java%20核心技术学习章节笔记-20221017-153810818.png)



链 表 是 一 个 有 序 集 合（orderedcollection), 每个对象的位置十分重要  

如果链表有 n 个元素，有 n+1 个位置可以添加新元素。这些位置与迭代器的 n+1 个可能的位置相对应  
  

  

链表的弊端  

链表不支持快速地随机访问。 如果要查看链表中第《个元素，就必须从头开始， 越过个元素。没有捷径可走  

LinkedList对象根本不做任何缓存位置信息的操作  

![](_assets/Java%20核心技术学习章节笔记/image-Java%20核心技术学习章节笔记-20221017-153833368.png)


  

  

从概念上讲， 由于Java 迭代器指向两个元素之间的位置  
  

为什么要优先使用链表呢？

使用链表的唯一理由是尽可能地减少在列表中间插人或删除元素所付出的代价。 如果列表只有少数几个元素， 就完全可以使用 ArrayList。  
我们建议避免使用以整数索引表示链表中位置的所有方法。 如果需要对集合进行随机访问， 就使用数组或 ArrayList, 而不要使用链表。  
  

  

Iterator和ListIterator主要区别有： // 简单来说，就是ListIterator更加强大  
  
一、ListIterator有add()方法，可以向List中添加对象，而Iterator不能。  
  
二、ListIterator和Iterator都有hasNext()和next()方法，可以实现顺序向后遍历。但是ListIterator有hasPrevious()和previous()方法，可以实现逆向（顺序向前）遍历。Iterator就不可以。  
  
三、ListIterator可以定位当前的索引位置，nextIndex()和previousIndex()可以实现。Iterator 没有此功能。  
  
四、都可实现删除对象，但是ListIterator可以实现对象的修改，set()方法可以实现。Iterator仅能遍历，不能修改。因为ListIterator的这些功能，可以实现对LinkedList等List数据结构的操作  
————————————————  
版权声明：本文为CSDN博主「a597926661」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。  
原文链接：https://blog.csdn.net/a597926661/article/details/7679765  

  
  

  

9.2.2 数组列表 —— ArrayList ， 用数组实现  

有两种访问元素的协议：一种是用迭代器， 另一种是用 get 和 set 方法随机地访问每个元素。后者不适用于链表， 但对数组却很有  
用

ArrayList 封装了一个动态再分配的对象数组  
  

对于一个经验丰富的 Java 程序员来说， 在需要动态数组时， 可能会使用 Vector 类。  
为什么要用 ArrayList 取代 Vector 呢？ 原因很简单：Vector 类的所有方法都是同步的。

可以由两个线程安全地访问一个 Vector 对象。

但是， 如果由一个线程访问 Vector, 代码要在同步操作上耗费大量的时间。这种情况还是很常见的。

而 ArrayList 方法不是同步的，因此，建议在不需要同步时使用 ArrayList, 而不要使用 Vector。  
  

9.2.3 散列表 —— HashSet 用散列表实现  

如果不在意元素的顺序， 可以有几种能够快速査找元素的数据结构 ，散列表就是其中一种数据结构，在java中，散列表用链表数组实现  
  

散列表为每个对象计算一个整数， 称为散列码（hashcode)。散列码是由对象的实例域产生的一个整数。更准确地说， 具有不同数据域的对象将产生不同的散列码  
![](_assets/Java%20核心技术学习章节笔记/image-Java%20核心技术学习章节笔记-20221017-153910389.png)



自己实现的 hashCode方法应该与 equals 方法兼容，即如果 a.equals(b) 为 true, a 与 b 必须具有相同的散列码  
  

在 JavaSE 8 中， 桶满时会从链表变为平衡二叉树  
  

 HashSet 类，它实现了基于散列表的集

9.2.4 树集 —— TreeSet 用红黑二叉树实现  

TreeSet 类与散列集十分类似， 不过， 它比散列集有所改进。树集是一个有序集合( sorted collection) o 可以以任意顺序将元素插入到集合中。

在对集合进行遍历时， 每个值将自动地按照排序后的顺序呈现。正如 TreeSet 类名所示， 排序是用树结构完成的（当前实现使用的是红黑树（red-black tree。) 每次将一个元素添加到树中时，都被放置在正确的排序位置上。因此，迭代器总是以排好序的顺序访问每个元素。  
  
将一个元素添加到树中要比添加到散列表中慢， 参见表 9-3 中的比较，但是，与检查数组或链表中的重复元素相比还是快很多。  
  

  

老生长谈的问题： hashCode(), equals()的联系 参考：https://www.cnblogs.com/keyi/p/7119825.html  

hashCode() 只是负责生成散列码  

equals() 确保散列值一样，并且内容一样  

  

public boolean **equals**(Object othe 「Object){  
     if (this = othe 「Object) return true;  
     if (otherObject == null) return false;  
     if (getClassO != otherObject.getGass0) return false;  
     Item other = (Item) otherObject;  
     return Objects,equals(description, other.description) && partNumber == other.partNumber;  

}  

public int hashCode ( ) {  
     return Objects,hash(description, partNumber);  
}  

  

  

9.2.5 队列与双端队列 —— Queue & Deque  用数组实现  

队列可以让人们有效地在尾部添加一个元素， 在头部删除一个元  
素。有两个端头的队列， 即双端队列， 可以让人们有效地在头部和尾部同时添加或删除元  
素。不支持在队列中间添加元素  

在 Java SE 6 中引人了 Deque 接口， 并由 ArrayDeque 和  
LinkedList 类实现。这两个类都提供了双端队列，而且在必要时可以增加队列的长度  
  

  

9.2.6 优先级队列 —— priority queue 用堆实现  

  

优先级队列（priority queue) 中的元素可以按照任意的顺序插人，却总是按照排序的顺序  
进行检索。也就是说，无论何时调用 remove 方法，总会获得当前优先级队列中最小的元素。  
然而，优先级队列并没有对所有的元素进行排序。如果用迭代的方式处理这些元素，并不需  
要对它们进行排序。优先级队列使用了一个优雅且高效的数据结构，称为堆（heap)。堆是一  
个可以自我调整的二叉树，对树执行添加 （add) 和删除（remore) 操作， 可以让最小的元素  
移动到根，而不必花费时间对元素进行排序  
  

使用优先级队列的典型示例是任务调度 每一个任务有一个优先级，任务以随机顺序添  
加到队列中。每当启动一个新的任务时，都将优先级最高的任务从队列中删除（由于习惯上  
将 1 设为“ 最高” 优先级，所以会将最小的元素删除  
  
  

  

  

  

  

  

  

  

  

  

  

  

  

  
  

  

# 9.2.1 链表

**Author:** Yunxiong  

9.2.1 链表  

数组和数组列表都有一个重大的缺陷，这就是从数组的中间位置删除一个元素要付出很大的代价，其原因是数组中处于被删除元素之后的所有元素都要向数组的前端移动，在数组中间插入一个元素也是如此 ，链表能解决这个问题  

链表的每个结点都存放着下一个结点的引用，java中，所有链表都是**双向链接**的 - 即每个结点还存放着指向前驱结点的引用  

![](《Java 核心技术》学习章节笔记_files/Snipaste_2020-01-30_00-10-54 [1].png)

链 表 是 一 个 有 序 集 合（orderedcollection), 每个对象的位置十分重要  

如果链表有 n 个元素，有 n+1 个位置可以添加新元素。这些位置与迭代器的 n+1 个可能的位置相对应  
  

  

链表的弊端  

链表不支持快速地随机访问。 如果要查看链表中第《个元素，就必须从头开始， 越过个元素。没有捷径可走  

LinkedList对象根本不做任何缓存位置信息的操作  

  

![](《Java 核心技术》学习章节笔记_files/Snipaste_2020-01-30_00-25-33 [1].png)

  

  

  

从概念上讲， 由于Java 迭代器指向两个元素之间的位置  
  

为什么要优先使用链表呢？

使用链表的唯一理由是尽可能地减少在列表中间插人或删除元素所付出的代价。 如果列表只有少数几个元素， 就完全可以使用 ArrayList。  
我们建议避免使用以整数索引表示链表中位置的所有方法。 如果需要对集合进行随机访问， 就使用数组或 ArrayList, 而不要使用链表。  
  

  

Iterator和ListIterator主要区别有： // 简单来说，就是ListIterator更加强大  
  
一、ListIterator有add()方法，可以向List中添加对象，而Iterator不能。  
  
二、ListIterator和Iterator都有hasNext()和next()方法，可以实现顺序向后遍历。但是ListIterator有hasPrevious()和previous()方法，可以实现逆向（顺序向前）遍历。Iterator就不可以。  
  
三、ListIterator可以定位当前的索引位置，nextIndex()和previousIndex()可以实现。Iterator 没有此功能。  
  
四、都可实现删除对象，但是ListIterator可以实现对象的修改，set()方法可以实现。Iterator仅能遍历，不能修改。因为ListIterator的这些功能，可以实现对LinkedList等List数据结构的操作  
————————————————  
  