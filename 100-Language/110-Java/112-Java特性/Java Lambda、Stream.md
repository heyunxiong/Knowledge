> Java基础知识： Lambda、Stream

Java Lambda和Steam流都是jdk1.8的新特性
## Lambda
为什么引入 lambda 表达式? （摘自核心卷二6.3）
> @me： 个人认为，Java的lambda表达式是一种妥协。

lambda 表达式是一个可传递的代码块，可以在以后执行一次或多次；在其他语言中， 可以直接处理代码块。
Java 设计者很长时间以来一直拒绝增加这个特性 ；毕竟， Java 的强大之处就在于其简单性和一致性 。
如果只要一个特性能够让代码稍简洁一些 ，就把这个特性增加到语言中 ， 这个语言很快就会变得一团糟， 无法管理 。不过 ， 在另外那些语言中，并不只是创建线程或注册按钮点击事件处理器更容易 ； 它们的大部分 API都更简单、更一致而且更强大。
在 Java 中 ， 也可以编写类似的API利用类对象实现特定的功能， 不过这种 API 使用可能很不方便。
就现在来说， 问题已经不是是否增强 Java 来支持函数式编程 ， 而是要如何做到这一点 。设计者们做了多年的尝试， 终于找到一种适合 Java的设计
### Lambda语法
Lambda语法建立在函数式接口上，需要关注函数式接口的参数和返回值
参考：[Lambda 表达式](https://blog.csdn.net/caiqing116/article/details/85147458?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163653020216780264092320%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163653020216780264092320&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-85147458.first_rank_v2_pc_rank_v29&utm_term=lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)
```java
(参数1，参数2) -> {
	方法体
}
```
| 描述 | 语法 |
| --- | --- |
| 无参，无返回值，
Lambda体只需要一条语句 | _( ) -> System.out.println("hello")_ |
| 一个参数，无返回值，
一个参数的情况下，小括号可省 | _args -> System.out.println(args)_ |
| 一个参数，有返回值，
Lambda体只有一条语句是return与大括号可省 | _(args) -> return args_ |
| 两个参数，无返回值，当参数的数据类型可由编译器通过上下文推荐出来时，可省 | _(args1,args2) -> {两个参数处理，无返回值}_
_(args1,args2) -> {System.out.println(args1+args2)}_ |
| 两个参数，有返回值，
Lambda体只有1条语句 | _(args1, args2) -> return args1和args2处理后返回_
_(args1, args2) -> return args1+args2_ |
| 两个参数，有返回值，
Lambda体有多条语句 | _(args1, args2) -> { _
_System.out.println("输入两个参数"); _
_return args1+args2;_
_}_ |

### 函数式接口
一个接口中，要求实现类实现的方法有且只有一个（不包括default方法），这样的接口就是函数式接口；比如：Runnable接口
```java
@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
```
### 判断函数式接口
可以通过@FunctionalInterface在IDE或者编译器中判断编写的接口是不是函数式接口。
```java
//是，有且只有一个实现类需要实现的方法test1
interface Interface1{
	void test1();
}
//不是，有两个实现类需要实现的方法test1，test2
interface Interface2{
	void test1();
    void test2();
}

//不是，没有实现类需要实现的方法
interface Interface3{
}

//是，本身没有定义方法，但是继承了Interface1，Interface1里面有且只有一个需要实现的test1方法
interface Interface4 extends Interface1{
}

//是，default方法不是必须实现的
interface Interface5{
	void test1();
    default void test2(){...};
}

//是，toString是Object类的方法，不需要实现类一定去实现。
interface Interface6{
	void test();
    String toString();
}

//不是，tostring可实现可实现
interface Interface7{
    String toString();
}

//是，只有test1需要被实现类重写
interface Interface8{
	void test1();
    default void test2(){...};
    static void test3(){...};
    String toString();
}
```
### Java内置函数式接口
| 接口类型 | 函数式接口 | 参数类型 | 返回值 | 用途 |
| --- | --- | --- | --- | --- |
| 消费型 | Consumer<T> | T | 无 | 对类型为T的对象应用操作，方法：void accept(T t) |
| 供给型 | Supplier<T> | 无 | T | 返回类型为T的对象，方法：T get() |
| 函数型 | Function<T,R> | T | R | 对类型为T的应用操作，并返回结果。结果是R类型的对象，方法R apply(T t) |
| 断言型 | Predicate<T> | T | boolean | 确定对象T是否满足某个约束条件并返回boolean值，方法boolean test(T t) |

![](_assets/Java%20Lambda、Stream/1602509994702-17241a10-1974-421b-b4cc-7c82e6d0eaa4.png)
### Demo使用
```java
// 准备各类型的函数式接口
// @FunctionalInterface表明该接口是函数式接口，可以不加，但是加了可以在编译帮忙检查

@FunctionalInterface
public interface NoneReturnNoneParameter {
    void test();
}

@FunctionalInterface
public interface NoneReturnSingleParameter {
    void test(int a);
}

@FunctionalInterface
public interface NoneReturnMultipleParameter {
    void test(int a, int b);
}

@FunctionalInterface
public interface SingleReturnNoneParameter {
    int test();
}

@FunctionalInterface
public interface SingleReturnSingleParameter {
    int test(int a);
}

@FunctionalInterface
public interface SingleReturnMultipleParameter {
    int test(int a, int b);
}

```
```java
public class LambdaTest {
    public static void main(String[] args)  {
        // 实现
        NoneReturnNoneParameter noneReturnNoneParameter = () -> System.out.println("无参无返回值函数式接口");

        NoneReturnSingleParameter noneReturnSingleParameter = (int a) -> {
            System.out.println("一个参数，无返回值函数式接口");
            System.out.println("a:"+a);
        };

        NoneReturnMultipleParameter noneReturnMultipleParameter = (int a, int b) -> {
            System.out.println("两个参数，无返回值函数式接口");
            System.out.println("a: " + a + ", b: " + b);
        };

        SingleReturnNoneParameter singleReturnNoneParameter = () ->{
            System.out.println("无参数，有返回值函数式接口");
            return 123;
        };

        SingleReturnSingleParameter singleReturnSingleParameter = (int a) -> {
            System.out.println("一个参数，有返回值函数式接口");
            System.out.println("a: " + a );
            return  a;
        };

        SingleReturnMultipleParameter singleReturnMultipleParameter = (int a, int b) ->{
            System.out.println("两个参数，有返回值函数式接口");
            System.out.println("a: " + a + ", b: " + b);
            return a+b;
        };
        
        // 调用
        noneReturnNoneParameter.test();
        noneReturnSingleParameter.test(123);
        noneReturnMultipleParameter.test(10,20);
        System.out.println("==========");
        System.out.println(singleReturnNoneParameter.test());
        System.out.println(singleReturnSingleParameter.test(10));
        System.out.println(singleReturnMultipleParameter.test(20, 30));
    }
}
```
### 其他说明
简化Lambda表达式的写法，比如：

- 只有一个参数的时候可以省略小括号
- 参数列表的参数类型可以省略，因为方法里面已经定义了；返回类型也是；比如 (a, b) -> a+b;
- 方法体只有一条语句的时候，可以省略大括号

虽然简化能使代码看着更加简洁，但是如果要牺牲可读性的话，那大可不必。
Lambda比较适合用在简短的业务代码中，并不适合用在复杂的系统中，会加大维护成本。

TO-DO：函数引用、静态方法、构造方法等的Lambda使用方法。

---

## Stream 流
流提供了一种让我们可以在比集合更高的概念级别上指定计算的数据视图。通过使用流Stream，可以说明想要完成什么任务，而不是说明如何实现它。
 流在管道中传输， 并且可以在管道的节点上进行处理， 比如筛选， 排序，聚合等

```java
+--------------------+       +------+   +------+   +---+   +-------+
| stream of elements +-----> |filter+-> |sorted+-> |map+-> |collect|
+--------------------+       +------+   +------+   +---+   +-------+
```
### Stream 流的创建

1. Collection中已经有两个方法，意味着其实现类可以通过该方法创建流
- **stream()** 		− 为集合创建串行流。
- **parallelStream()** 	− 为集合创建并行流
2. 使用静态方法 
- **Stream.of(....)**
- **Arrays.stream(...)**

既然可以把集合或者数组转成流，那么也应该有对应的方法，将流转换回去

- collect( ) 方法就满足了这种需求
```java
list.stream().collect(Collectors.joining(", ")).toString();
```
创建stream 流
```java
public class StreamTest {
    public static void main(String[] args) {
        // 数组创建流
        String[] personArray = {"sean", "jack", "tom"};
        Stream<String> stream1 = Arrays.stream(personArray);

        // Stream静态方法
        Stream<String> stream2 = Stream.of("123","456","789");

        // 集合创建流
        List<String> list = new ArrayList<>();
        list.add("sean he");
        list.add("sean pan");
        list.add("jack tan");
        list.add("tom tome");
        list.stream().filter(a -> a.contains("sean")).forEach(System.out::println);
        
        // 创建并行流
        Stream<String> stream4 = list.parallelStream();  
    }
}

```
流的操作可以分为两种类型：
1）中间操作，可以有多个，每次返回一个新的流，可进行链式操作。
2）终端操作，只能有一个，每次执行完，流也就结束了，无法执行下一个操作，因此只能放在最后。
![](_assets/Java%20Lambda、Stream/1636632714498-3c947341-3925-4e44-8d6d-6550fff5347b.jpeg)

### Stream 流的使用
参考：[流的使用](http://www.itwanger.com/life/2020/04/01/java-stream.html)
```java
public class StreamTest {
    public static void main(String[] args) {
        // 数组创建流
        String[] personArray = {"sean", "jack", "tom"};
        Stream<String> stream1 = Arrays.stream(personArray);

        // Stream静态方法
        Stream<String> stream2 = Stream.of("123","456","789");

        // 集合创建
        List<String> list = new ArrayList<>();
        list.add("sean he");
        list.add("sean pan");
        list.add("jack tan");
        list.add("tom tome");

        //过滤
        list.stream().filter(a -> a.contains("sean")).forEach(System.out::println);

        //映射
        // map这里把元素长度作为参数传入，并返回length大小。
        list.stream().map(String::length).forEach(System.out::println);

        //匹配
        boolean anyMatch_jack = list.stream().anyMatch(e -> e.contains("jack"));
        boolean allMatch_tom = list.stream().allMatch(e -> e.contains("tom"));
        boolean noneMatch_sean = list.stream().noneMatch(e -> e.contains("sean"));
        System.out.println(anyMatch_jack);
        System.out.println(allMatch_tom);
        System.out.println(noneMatch_sean);

        //组合
        
        /**
		reduce() 方法的主要作用是把 Stream 中的元素组合起来，
        它有两种用法：
		Optional<T> reduce(BinaryOperator<T> accumulator) 
        	- 没有起始值，只有一个参数，就是运算规则，此时返回 Optional。
		
        T reduce(T identity, BinaryOperator<T> accumulator)
        	- 有起始值，有运算规则，两个参数，此时返回的类型和起始值类型一致。
        **/
        Integer[] ints = {0, 1, 2, 3};
        List<Integer> list_b = Arrays.asList(ints);

        Optional<Integer> optional = list_b.stream().reduce((a, b) -> a + b);
        Optional<Integer> optional1 = list_b.stream().reduce(Integer::sum);
        System.out.println(optional.orElse(0));
        System.out.println(optional1.orElse(0));

        int reduce = list_b.stream().reduce(6, (a, b) -> a + b);
        System.out.println(reduce);
        int reduce1 = list_b.stream().reduce(6, Integer::sum);
        System.out.println(reduce1);


        // 把流转换成集合或者数组
        List<String> list_c = new ArrayList<>();
        list_c.add("sean1");
        list_c.add("jack2");
        list_c.add("tao3");
        list_c.add("klay4");

        String[] strArray = list_c.stream().toArray(String[]::new);
        System.out.println(Arrays.toString(strArray));

        List<Integer> list1 = list_c.stream().map(String::length).collect(Collectors.toList());
        List<String> list2 = list_c.stream().collect(Collectors.toCollection(ArrayList::new));
        System.out.println(list1);
        System.out.println(list2);

        String str = list_c.stream().collect(Collectors.joining(", ")).toString();
        System.out.println(str);

    }
}
```
### Stream流与Collection集合的区别

- Collection主要用来对元素进行管理和访问
- Stream并不支持对其元素进行直接操作和直接访问，而只支持通过声明式操作在其之上进行运算后得到结果；
- Stream不存储值
- 对Stream的操作会产生一个结果，但是Stream并不会改变数据源；
- Stream的操作(filter,map,sort等)都是以惰性的方式实现的
