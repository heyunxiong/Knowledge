> Java 基础知识： 集合 Collection

## Java 集合
数组虽然也可以存储对象，但长度是固定的；如果操作的对象是不固定的，或者需要频繁进行操作，可以使用集合
集合类的特点：
集合长度是可变可扩展的，集合可以存储不同类型的对象。

Java Collection家族图 
参考：[Java集合家族图](https://img-blog.csdnimg.cn/20200215163914737.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21vbW81N2w=,size_16,color_FFFFFF,t_70#pic_center)
![image.png](_assets/Java%20集合/1636180920639-0a63f7be-2c8c-42db-a74a-b87c90f19028.png)精简版本，关注常用的几个
![](_assets/Java%20集合/1636183694119-310c7c56-fdb7-4472-9925-77e849e2f40d.jpeg)

![](_assets/Java%20集合/1602509994656-339dd7c0-e001-48b2-8611-1bce4fd8a3a2.png)
## Iterator 接口
Iterator接口，这是一个用于遍历集合中元素的接口；
主要包含hashNext(), next(), remove()三种方法，其中还有一个默认方法：forEachRemaining
## 顶层接口
集合类：Collection，List, Set 和 映射关系：Map
### Collection
Collection 接口是java集合的基础接口， 定义了常用的集合操作。
```java
public interface Collection<E> extends Iterable<E> {
    //....省略.....    
    int size();
    boolean isEmpty();
    boolean contains(Object o);
    boolean add(E e);
    boolean remove(Object o);
	Iterator<E> iterator(); //迭代器，能循环遍历集合中的元素
   							//返回此集合中的元素的迭代器 
    						//没有关于元素返回顺序的保证（除非这个集合是提供保证的某个类的实例）
	//....省略.....
}
```
### List
List 接⼝也是⼀个顶层接⼝，它继承了 Collection 接⼝ ，同时也是 ArrayList、LinkedList 等集合元素的⽗类；
同样的，保留着子类的常用操作，比如添加add，移除remove，判空等方法，让子类去各自实现。
```java
public interface List<E> extends Collection<E> {}
```
### Set
与 List 接⼝同级的层次上，也继承了 Collection 接⼝。
Set 接⼝提供了额外的规定。它对add、equals、hashCode ⽅法提供了额外的标准：比如：不能有重复的元素
```java
public interface Set<E> extends Collection<E> {}
```
### Map
Map是映射关系的顶级接口，和Collection是同等级别的；定义了常用的操作方法。
⽀持 key-value 存储的对象，Map 不能包含重复的 key，每个键最多映射⼀个值
```java
public interface Map<K,V> {
    //......省略.......
    
    V get(Object key);
    V put(K key, V value);
    V remove(Object key);
    
    //......省略.......
}
```
## 集合实现类
### ArrayList
```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable{...}
```
ArrayList的特点：

- ArrayList实现了List接口，底层实现的数据结构是 ：可扩容的动态**数组**
- ArrayList 允许所有的元素，包括空值。
- ArrayList 线程不安全
- ArrayList 有个数组的容量，⽤来存储元素的容量。（加锁或使用Collections.synchronizedList ）
- ArrayList 具有 fail-fast 快速失败机制，能够对 ArrayList 作出失败检测。

当在迭代集合的过程中该集合在结构上发⽣改变的时候，抛出ConcurrentModificationException 异常
### Ventor
和ArrayList基本一致，特有的是**线程安全**特性，方法上都带锁synchronized
### LinkedList
```java
public class LinkedList<E> extends AbstractSequentialList<E>
   					     implements List<E>, Deque<E>, Cloneable, java.io.Serializable{...}
```
LinkedList 是⼀个双向链表，允许存储任何元素(包括 null )。
特性
LinkedList 查询慢，增删快。因为所有的操作都表现为双向性的，索引到链表的操作将遍历从头到尾；
LinkedList 线程不安全
### HashSet
```java
public class HashSet<E>    extends AbstractSet<E>
							implements Set<E>, Cloneable, java.io.Serializable{
    static final long serialVersionUID = -5024744406713321676L;
    private transient HashMap<E,Object> map; // 可以看到这里有个HashMap

....
}
```
HashSet 是 Set 接⼝的实现类，由哈希表⽀持；实际上是借用了Hashmap的实现。
Hash的特点：

- 元素无序，不能保证取出来的元素的顺序
- 允许元素为null
- HashSet线程不安全（加锁或使用 Collections.synchronizedSet() ）
- ⽀持 fail-fast 机制
### TreeSet
```java
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable{
    /**
     * The backing map.
     */
    private transient NavigableMap<E,Object> m;
    .....
}
```
TreeSet 是⼀个基于 TreeMap 的 NavigableSet 实现
TreeSet的特点：

- 元素有序
- TreeSet 线程不安全（加锁或使用：SortedSet s = Collections.synchronizedSortedSet(new TreeSet(...)) ）
- ⽀持 fail-fast 机制
### LinkedHashSet
```java
public class LinkedHashSet<E>    extends HashSet<E>
    implements Set<E>, Cloneable, java.io.Serializable { ...}
```
这个实现不同于 HashSet 的是它维护着⼀个贯穿所有条⽬的双向链表。此链表定义了元素插⼊集合的顺序。
注意：如果元素重新插⼊，则插⼊顺序不会受到影响

- 元素有序
- 选择过⾼的初始容量值的开销要⽐ HashSet ⼩；因为LinkedHashSet 的迭代次数不受容量影响
-  LinkedHashSet 线程不安全的，加锁或使用：Collections.synchronizedSet
- ⽀持fail-fast机制
### HashMap
> 太重要了，遇事不决，HashMap！

```java
public class HashMap<K,V> extends AbstractMap<K,V>
    				implements Map<K,V>, Cloneable, Serializable {
 
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16
    static final int MAXIMUM_CAPACITY = 1 << 30;
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
    static final int TREEIFY_THRESHOLD = 8;
    static final int UNTREEIFY_THRESHOLD = 6;
    static final int MIN_TREEIFY_CAPACITY = 64;
   ...
}
```

- HashMap 是⼀个利⽤哈希表原理来存储元素的集合，并且允许空的 key-value 键值对。
- HashMap 线程不安全的 （使用：ConcurrentHashMap）
- HashMap 也⽀持 fail-fast 机制
- HashMap 的实例有两个参数影响其性能：初始容量 和加载因⼦
### TreeMap
```java
public class TreeMap<K,V>   extends AbstractMap<K,V>
    implements NavigableMap<K,V>, Cloneable, java.io.Serializable{.....}
```
⼀个基于 NavigableMap 实现的红⿊树。

- 这个 map 根据 key ⾃然排序存储，或者通过 Comparator 进⾏定制排序；
- TreeMap 为 containsKey,get,put 和remove⽅法提供了 log(n) 的时间开销。
- TreeMap线程不安全
- 支持fail-fast机制
### LinkedHashMap
```java
public class LinkedHashMap<K,V> extends HashMap<K,V>
								implements Map<K,V>{......}
```
LinkedHashMap 是 Map 接⼝的哈希表和链表的实现；与 HashMap 不同之处在于它维护了⼀个贯穿其所有条⽬的双向链表。

- 允许 null 元素。由于维护链表的额外开销，性能可能会低于HashMap，
- LinkedHashMap 有两个因素影响了它的构成：初始容量和加载因⼦。
- LinkedHashMap线程不安全
- 支持fail-fast机制。
## 特征总结
| **实体集合/映射** | **接口** | **重复项** | **有序/排序** | **线程安全** | **随机访问** | **存储空元素** | **实现类数据结构** | **元素调用方法** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ArrayList | List | 可以重复 | 插入排序 | 不安全 | 随机 | 元素可空 | 可调大小数组 | equals() |
| Vector | List | 可以重复 | 插入排序 | 安全 | 随机 | 元素可空 | 可调大小数组 | equals() |
| LinkedList | List | 可以重复 | 插入排序 | 不安全 | 不随机 | 元素可空 | 双向链表 | equals() |
| HashSet | Set | 元素唯一 | 无顺序 | 不安全 | 不随机 | 元素可空 | Hash表 | equals()、hashCode() |
| TreeSet | SortedSet | 元素唯一 | 排序 | 不安全 | 不随机 | 元素不可空 | 平衡树 | equals()、compareTo() |
| LinkedHashSet | Set | 元素唯一 | 插入排序 | 不安全 | 不随机 | 元素可空 | Hash表和双向链表 | equals()、hashCode() |
| HashMap | Map | 键唯一 | 无顺序 | 不安全 | 随机 | 元素可空 | Hash表 | equals()、hashCode() |
| TreeMap | SortedMap | 键唯一 | 键序排列 | 不安全 | 随机 | 元素不可空 | 平衡树 | equals()、compareTo() |
| LinkedHashMap | Map | 键唯一 | 键插入顺序/条目访问顺序 | 不安全 | 随机 | 元素可空 | Hash表和双向链表 | equals()、hashCode() |

## 工具类
### Collections 类
Collections 不属于 Java 集合框架；它属于单独的分⽀，Collections 是⼀个包装类，它的作⽤就是为集合框架提供某些功能实现；是一个工具类的角色。
```java
/**
中文api的介绍：
此类仅由静态方法组合或返回集合。 它包含对集合进行操作的多态算法，“包装器”，返回由指定集合支持的新集合，以及其他一些可能的和最终的。 
如果提供给它们的集合或类对象为null，则此类的方法都抛出一个NullPointerException 。 
该类中包含的多态算法的文档通常包括实现的简要说明 。 这些描述应被视为实施说明 ，而不是说明书的一部分 。 只要规范本身得到遵守，实现者就可以随意替代其他算法。 （例如，sort使用的算法不一定是一个mergeesort，但它必须是稳定的 。） 
如果集合不支持适当的突变原语，例如set方法，则该类中包含的“破坏性”算法，即修改其操作的集合的算法被指定为抛出UnsupportedOperationException 。 如果调用对集合没有影响，这些算法可能但不是必须抛出此异常。 例如，在已经排序的不可修改列表上调用sort方法可以抛出UnsupportedOperationException 。

**/
public class Collections {
    // Suppresses default constructor, ensuring non-instantiability.
    private Collections() {
    }
.....

	// 给那些不是线程安全的集合类提供了实现同步的方法
	public static Collection synchronizedCollection(Collection c);
	public static Set synchronizedSet(Set s);
	public static List synchronizedList(List list);
	public static <K,V> Map<K,V> synchronizedMap(Map<K,V> m);
	public static SortedSet synchronizedSortedSet(SortedSet s);
	public static <K,V> SortedMap<K,V> synchronizedSortedMap(SortedMap<K,V> m);
    
 ...   
}
```
### Arrays 类
和Collections类一样，是一个为集合提供部分功能的工具类；
```java
/**中文API 的介绍：
该类包含用于操作数组的各种方法（如排序和搜索）。 该类还包含一个静态工厂，可以将数组视为列表。 
如果指定的数组引用为空，则该类中的方法都抛出一个NullPointerException 
**/
public class Arrays {
    private static final int MIN_ARRAY_SORT_GRAN = 1 << 13;
    private Arrays() {}
....
}
```
# 数组和集合之间的转换

- 数组转换成集合类

Arrays类的asList( )方法可以将数组转换成List列表
```java
public class ArrayToList{
	public static void main(String[] args){
    	List<Integer> list = Arrays.asList(1,2,3,4,5);
    }
}
```

- 集合转成数组

Collection接口中的toArray( )方法
```java
public class ListToArray{
	public static void main(String[] args){
        List<Integer> list = new ArrayList<Integer>(); //创建列表
        for(int i=0; i < 5; i++){
        list.add(i);								  // 向列表添加元素
        }
    	Integer[] array  = list.toArray(new Integer[]{}); //将列表转换成数组
    }
}
```
## 遗留的集合
已经过时，不建议使用的集合类

- HashTable 类 			 java.util.HashTable 
- Enumeration 接口		 java.util.Enumeration
- Properties 属性映射	 java.util.Properties
- Stack 栈 				 java.util.Stack
- BitSet 位集			 java.util.BitSet 
