# Java 泛型入门 —— 理解及使用

https://www.bilibili.com/read/cv2845561



早在JDK1.4版本之前是没有泛型这个概念的，当时我们使用集合是这样的：

List list = new ArrayList();

list.add("www.woniuxy.com");

list.add(23);

String name = (String)list.get(0);

Integer number = (Integer)list.get(1);

我们声明一个集合，这个集合里面可以存储各种各样的数据，在取出来的时候进行强制类型转换。但是这样子写是有一定的隐患的，时间长了我们就会忘记我们存放在list里面的第一个，第二个，第N个数据分别都是什么类型，就会出现以下情况：

public void listDemo(){

    List list = new ArrayList();  

    list.add("www.woniuxy.com");  

    list.add(23);  

    String name = (String)list.get(0);  

    String number = (String)list.get(1); //ClassCastException

}

上面的代码就是我们在取出数据时进行了强制的类型转换，但是这个代码如果运行的话是会发生类型转换异常的，这是因为我们村粗的第二个数据明明是int型，但是取出来是时候我们却将他强转为String。

# 泛型的诞生

Sun 公司为了让我们的Java语言更加的安全可靠，并且减少运行时发生异常，于是在JDK1.5版本推出了泛型的概念。所以在这个版本之后我们写集合就可以这样写了：

List<String> list = new ArrayList();

list.add("www.woniuxy.com");

list.add("www.woniuxy.com/train");

String cnBlogs = list.get(0);

String myWebSite = list.get(1);

所谓的泛型就是将类型参数化，只有在编译的时候采取确定具体的参数，在上面这个例子中我们具体的类型就是String，我们可以看到在创建List集合的时候我们就指定了集合的数据为String类型，这意味着我们不能往这个list里面放除了String以外的其他参数类型。但是有一点好的是我们在去数据的时候不需要进行强制的类型转换了，这样极大的减少了发生强制类型转换异常的风险。

上面我们通过这两个相当简单的例子简单的认识了泛型以及为什么要有泛型和泛型最简单的使用，下面我们就通过例子看看泛型的本质。

# 泛型的本质

ArrayList<String> a = new ArrayList<String>();

ArrayList<Integer> b = new ArrayList<Integer>();

Class c1 = a.getClass();

Class c2 = b.getClass();

System.out.println(c1 == c2);

在继续往下阅读之前你先想一想这几行代码的输出结果是什么？

true or false？

答案是true，因为无论是对于ArrayList<String>还是 ArrayList<Integer>，他们的Class类型是一致的，都是ArrayList.class。

那么他们明明有指定类型的差异，这个差异到底体现在哪里呢？

答案是体现在类编译的时候，当JVM进行类编译的时候会进行泛型检查，如果说一个List被声明为String类型，那么他往该集合存取数据的时候就会对数据进行判断，从而就避免了存入或取出错误的数据。

这也就是说，泛型只存在于编译阶段，而不存在于运行阶段。在编译后的class文件中是没有泛型这个概念的。上面我们只是说了泛型在集合中的使用方式，但其实泛型的应用范围不仅仅只是集合，还包括类、方法、Map 接口等等。

泛型的应用还广泛存在于下面几种情形：泛型类、泛型方法、泛型集合。

# 泛型类

泛型类一般使用字母 T 作为泛型的标志。

public class GenericClass<T> {

    private T object;    

    public T getObject() {         

        return object;   

      }     

    public void setObject(T object) {     

        this.object = object;    

     }

}

使用

public static void main(String[] args) {     

    GenericClass<Integer> integerGenericClass = new GenericClass<>(100);    

    integerGenericClass.showType(); 

    GenericClass<String> stringGenericClass = new GenericClass<>("www.woniuxy.com/train");

    stringGenericClass.showType();

}

# 泛型方法

泛型方法一般使用字母 T 作为泛型的标志。

public class GenericMethod {

    public static <T> T getObject(Class<T> clz) throws InstantiationException,IllegalAccessException{

         T t = clz.newInstance();

         return t;

    }

}

使用：

public static void main(String[] args) throws Exception{

     GenericMethod genericMethod = getObject(GenericMethod.class);

     System.out.println("Class:" + genericMethod.getClass().getName());

}

# 泛型集合

除了使用 T 作为泛型类的标志之外，在需要使用 Map 的类中，通常使用 K V 两个字母表示 Key Value 对应的类型。

public class GenericMap<K, V> {

     private K key;     private V value;

     public void put(K key, V value) {

         this.key = key;

         this.value = value;

     }

}

使用：

public static void main(String[] args) {

         GenericMap<Integer, String> team = new GenericMap<>();

         team.put(1, "aotedan");

         team.put(2, "Me");

         GenericMap<String, Integer> score = new GenericMap<>();

         score.put("aotedan", 88);

         score.put("Me", 80);     

}