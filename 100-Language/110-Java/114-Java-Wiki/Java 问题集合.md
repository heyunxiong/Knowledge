# 问：char类型变量能否保存一个汉字？
能！
**计算机中的数据存储基本单位是字节（byte）。**一个字节byte的范围是 -128~127， 这256个数字范围可以包括字母大小写，数字和基本常用的英语标点符号！（这很真实，侧面体现了谁发明，谁就是标准。这个范围基本满足英文场景下的表达）
而存储一个汉字，需要2个字节，为什么？ 因为汉字远远不止256个，使用Unicode字符集进行编码，可以存储65535个字符，满足汉字场景下的表达。

# float num = 3.14159是否正确？
不正确
java表达浮点数的基本类型有float和double，默认情况下是doule，比如 var = 1.234， 前面没有类型修饰的情况下，var会被当成double类型。如果想表达float类型，需要在后面加f或者F，即系，
float var =1.234f
float var = 1.234F
而float num = 3.14159 ，num会被认为是double，但是由于用float修饰了，又没有强制类型转换，所以不行。

# short和char类型的取值范围
char说过了前面，两个字节，一个字节八位， 2^16 即 0~65535
short是有符号的数据类型，有正负之分；二进制中，最高位充当符号位。short的范围是 -32768~32767

# 局部变量可以定义私有修饰类型吗？
即：方法内部能定义私有private的变量吗？
不能。无法编译通过
方法内部的变量不可以使用private，protected，public修饰
![image.png](_assets/Java%20问题集合/1616230068768-e9fab87b-6c9d-4e13-81c6-50cb6355df16-20230104110227238.png)


# 3-2.6 == 0.4 输出什么？

-的优先级高于==，先算3-2.6 在和0.4进行比较，输出的将会是true 或者false
java中的基本类型的浮点数运算是不精确的，如图所示
![image.png](_assets/Java%20问题集合/1616230289018-9824ebcc-682a-43d4-ad92-9f7fd40f4921-20230104110235885.png)
可以使用BigDecimal类进行浮点数计算
![image.png](_assets/Java%20问题集合/1616230615337-7b7e7f4c-b2ab-4dd8-976b-07d0b2d78352.png)

# & 和 &&两个运算符的区别
&是位运算符，
&&是逻辑运算符，&&是短路运算符，只要第一个为false，就不会继续比较了。
# 能正确编译 short s = 1; s = s + 1; 吗？
不能
默认情况下，java 的整数类型是int
s是short类型，1是int类型，s+1 即系 short 类型+ int 类型，返回的是int才对。需要强制转换才行，即（short） s =s +1;
类似的情况还有 int 与int 相乘，是否正确？ 说白了就是看是不是超出了数据类型的范围。
int * int 赋值给long是否会报错？ 会，如果两个int在相乘时没有超过范围，那么是用int的类型进行运算，结果超过int 的取值范围，出现了溢出情况，但是程序会保留这个溢出结果。

# 9/2 和 9/2.0
9/2是整数之间进行运算，返回的是整数，小数部分直接丢弃，结果为4
9/2.0 是整数和浮点数进行运算，返回结果是浮点数，结果为4.5
# TO-DO:关于位运算
# 判断闰年的条件
判断是否是闰年的两个条件：能被4整除且不能被100整除，另外能被400整除
if (year % 4 == 0 && year % 100 != 0  || year % 400 ==0)
# If语句的小点
在if语句中，如果不使用 { } 将要执行的语句序列括起来，那么将只对if语句后面第一条语句起作用，其他语句将不受if语句的控制
# Switch能替代if吗？
一般情况下是可以的，但要注意switch语句的表达式的参数只能测试byte，short，int，char；遇到判断相等不相等的情况，就不能替代if
# 如何确定使用for循环还是while循环
for循环使用的情况是能明确知道循环的上限次数
while循环则针对那些无限次数的情况，没有明确的上限次数 
# 跳出当前的多重嵌套循环
可以使用label和break语句结合
```java
void function(){
	...
    label:
    for(...){
    	...
        for(...){
            ...
            break label; //跳出循环到label，最外层
        }
    }
}
```
# TO-DO： 常见的排序算法的原理和代码实现

# 面向对象的特征
面向对象的编程方式具有封装、继承和多态性等特点。封装可以隐藏实现细节，使得代码模块化；继承可以扩展已经存在的代码模块，它们的目的都是为了代码重用；而多态是为了减少代码之间的紧密耦合，增加应用程序的灵活性。

# 什么是多态
多态是指一个类可以具有多种行为。多态性是指定义具有相同名称的方法或属性的多个类，但这些类的同名方法或同名属性具有不同的行为，并且这些类共享相同的基类或接口。
例如，把车看作一个抽象基类，很清楚的一个事实，就是所有的车都有移动的功能。接下来定义一个火车类和一个汽车类，这两个类均继承自“车”这个抽象类。火车和汽车都可以移动，说明两者在这方面可以进行相同的操作。然而，火车和汽车移动的行为是截然不同的，因为火车必须在铁轨上行驶，而汽车在公路上行驶，这就是类多态性的形象比喻。
# 静态语句块有什么作用
{ ... } 构成一个静态语句块
静态语句块通常用于进行必要的初始化操作；静态语句块在使用其所在的类时就被分配了内存并执行语句块中的代码，因此可以在静态语句块中进行初始化操作，如数据库连接、初始化图像等
# 值传递还是引用传递
值传递，
![image.png](_assets/Java%20问题集合/1616660646137-50379e4d-e3aa-4158-b286-cba30c85d16c.png)
引用传递
![image.png](_assets/Java%20问题集合/1616660657579-91623185-19e5-4bb6-b96c-614faa7bedfc.png)
![image.png](_assets/Java%20问题集合/1616660662721-3b735f81-cf24-45d9-aecb-458a07b0111e.png)
在Java语言中，把对象作为参数传递给方法时，方法接收到的是对象的内存引用的地址，而不是对象本身，这个引用地址是对象在内存中的位置，它不可能像对象内容那样被改变。所以Java语言中没有引用传递，只有值传递。

# 接口和抽象类的区别？ 整理一下
# 如何使用clone方法克隆对象？
clone 方法来自Object类，克隆的浅克隆和申克隆
浅克隆，只复制基本类型，无法复制引用类型
深克隆，即可复制基本类型，也可复制引用类型
两种方法实现深克隆
一种是采用序列化的方式实现，另一种是采用依次克隆各个可变的引用类型域的方法实现；
序列化的效率不理想。
# 内部类是否可以被继承
可以~！和普通类一样。
写法：
 class A extend B.C {。。。}   //C是B的内部类

public class B{
。。
 C{
。。}
}

# 匿名内部类
匿名内部类是指乜有指定类名的内部类，当某个类不需要重复使用时，就可以把该类定义为匿名内部类。好惨~ 就是一次性类。
匿名内部类必须继承一个父类或者实现一个接口


# 创建Class对象的三种方式

1. Class.forName( 类完整路径 ) ;  //知道完整类路径使用
2. 类.class属性,  // 知道类
3. 对象.getClass( ) //通过类的对象实例获取该类的Class对象
# 如何通过反射获取类的信息
使用Class类的方法能获取对应类的信息。Class类提供了大量的方法，通过这些方法获取类的基本信息，例如类的构造方法，普通方法，字段等等
# 如何使用反射创建对象

- 使用Class类的newInstance（）方法

new Student( ).getClass( ).newInstance().

- 使用Constructor类实现

java.lang.reflect.Constructor类有一个参数可变的newInstance(Object ... obj)方法，可以使用该方法创建对象。
应首先获得类的 Class对象，然后再通过Cass对象的方法获得 Constructor类的实例，并通过 Constructor类的实例，调 newInstance（ Object…obj）方法完成对象的创建
# 如何通过反射调用方法
在Java中通过反射可以执行类中的方法，这就需要通过类的Clas对象调用 getMethod（ String name, Class<？x… arameterTypes）方法来获得类的指定方法，该方法返回一个javlang reflect Method对象，也可以调用 getMethodso方法获得类的全部方法，该方法返回个 java. lang reflect Method对象的数组。通过 Class对象获得类的 Method对象后，就可以调用 Method类的 invoke（object obj, object.…obis）方法来执行类中的指定方法
invoke(Object obj, Object ... objs)
# 如何通过反射访问成员变量
和调用方法大同小异，先获取Class对象，调用Class对象的getDeclaredField（String name）来获取类的指定字段，返回一个Filed类的对象，再用getter、setter即可获取和修改
# 关于equals方法的重写
重写equals方法，一般也要重写hashCode（）方法
遵循的约定
自反性
对称性
传递性
一致性
对于任何非空的引用值x。x.equals(null) 都应该返回false
# 如何重写equals和hashcode方法
Object类提供的用于比较对象是否相等的方法 equals，通常只是比较两个引用是否指向内存中的同一个对象。
而通常情况下，我们要比较的是它们逻辑上是否相等，而不是它们是否指向同一个对象，这时就需要重写equals（）方法

![image.png](_assets/Java%20问题集合/1616755395007-0faf43f0-0d59-40bc-a38c-a5a41fa5161b.png)
![image.png](_assets/Java%20问题集合/1616755402029-56daed30-e73e-422d-941f-9f08c1afe479.png)


# "3+5="+3+5 的返回值是什么
3+5=35
这里重点是+符号，既可以是数学上的加法运算符，也可以是字符串连接运算符
当+与字符串连接的时候，任何类型的数据都被转换为字符串进行连接，而不是进行数字运算，“3+5=”这是字符串

# String str= null 和 String str = ""
当一个字符串被赋值为nu时，它并没有被分配任何的内存空间，而只是声明了一个字符串变量。空字符串拥有内存空间，只是其长度为0而已。只有真正理解了空字符串的定义才能避免在使用空字符串过程中出现不必要的问题。
String str=null表示声明了一个 String对象的引用str，但是没有为其分配内存空间，
而 String str="则表示创建了一个长度为0的空字符串，并在内存中为其分配了内存空间。

# 关于字符串常量赋值
java中，如果将同一个字符串常量赋值给多个字符串变量，则这些字符串对象具有相同的内存地址，因为同一个字符串常量在内存中的地址是不变的，所以多个对象共用同一个内存地址。
String str1 = "Hello";
String str2 = "Hello";
String str3 = str2;
![image.png](_assets/Java%20问题集合/1617333716427-1a746a2f-7601-4570-91ff-b81c6e06749e.png)

# 如何判断字符串是否为空
当String str = null时，这个时候没有长度，可以用 if(str == null)
当String str = "" 时，这是长度为0，可以用 if(str.equals("")) 或者 if（str.length( ) == 0）
# 使用String 类进行日期格式化
![image.png](_assets/Java%20问题集合/1617334667081-ec2e8e68-9da3-40b5-8d77-51f01c7ce674.png)
![image.png](_assets/Java%20问题集合/1617334676366-67783443-b2c9-4db2-8378-7308d2dcbc3a.png)

# 如何实现字符串类型和数值类型的转换
int类型对应的包装类为 Integer类，而Java中将字符串也作为对象处理，因此将字符串转换为 Integer类对象即可。 Integer对象的 parselnt（）方法可实现将字符串对象转换为 Integer对象，但是使用该对象时需要注意的是，要求转换的字符串必须全部为数字，如果字符串不是数字，那么在运行时将会抛出 Numberformatexception异常。
# StringTokenizer类，新玩意？
# Java中各种进制之间的转换
重点是用Integer的方法
十进制转其他
toBinaryString(int i)
toHexString(int i)
toOctalString(int i)
其他转十进制
parseInt(String s, int radix). radix是2,816
# 指定字符串的编码格式
String类中提供了将字符串以指定字符序列表示的方法 getbytest0，使用该方法可以创建指定编碣格式的字符串
getbytes（：该方法使用平台的默认字符集将字符串编吗为byte（字节）序列，并将结果存儲到一个新的byte数组中。
getbytes（ charset charset）：使用给定的编玛格式将字符串编吗到byte（字节）序列，并将结果存儲到新的byte数组
String str="Java编程词典" //定义测试字符串
byte [] btuf=str. getbytes（"UTF-8"）//使用指定的字符集将此字符串解吗为字节序列
byte bt=str getbytes（GBK"），
String str2= new String（btut"UTF-8"），/根据解吗后所得的字节数组创建对象
String str3 =new String（bt, "GBK"），

# 迭代器Iterator与for
iterator可以用来遍历集合类和删除指定的元素remove
for和for加强版适合用来遍历全部元素

# ListIterator和Iterator的区别
![image.png](_assets/Java%20问题集合/1617347560705-acb8b060-01e7-416f-a221-5174c5652a5c.png)
# ArrayList和LinkedList
Arraylist类相当于数据结构中的线性表，它在底层使用数组来存儲元素，因此透合快
速获得指定位置的元素。但是，在刑除元素时，例如册除第一个元素，则后面的元素必須
全部向前移动一位，昆然开銷很大。向第一个位置増加元素时，效果类似。
Linkedlist类相当于数据结构中的链表，它在底层使用对象来保存元素，因此透合元
素的增加和刪除。但是，要获得指定位置的元素时，需要从头开始遍历，量然开銷很大。

# ArrayList和Ventor
基本一致，Ventor是线程安全的，效率不如ArrayList。
# Queue接口
![image.png](_assets/Java%20问题集合/1617347827767-5c8b7452-73a3-4cd0-9a6b-90eb7b0d6592.png)
# Map常用实现类
Map接口有3个常用的实现类，即 Hashmap、 Treemap和 Linkedhashmap。其中，Hashmap用于快速保存、査找数据。 Treemap支持排序功能。 Linkedhashmap能够保存键值对的添加顺序

# 计算机中的浮点数是连续的吗？
在数学中，浮点数是连续的，即任意两个浮点数之间还存在无限多个浮点数。
但是在计算机中并不是无限多的，相邻的两个浮点数之间的距离叫最小精度单位（Unit of Least Precision）
![image.png](_assets/Java%20问题集合/1617349101597-1e469c84-b8cd-44c7-a8e2-75c5821bc7b4.png)
由于ULP的存在，使得浮点数精度并不理想，因此不透合高精度运算。在Java中，可以使用 Big Decimal类来完成高精度浮点数的运算。

# 数字的舍入模式
![image.png](_assets/Java%20问题集合/1617349465878-d89c8a20-3847-4a82-ae49-5d654118d538.png)
# 如何格式化数字
使用DecimalFormat类进行格式化
# throws 与 throw
throws在方法声明处使用
throw在方法中使用
由于 throw与 throws的拼写非常接近，容易让人产生混淆，但是两者的用法与用途完全没有相似之处。
throw用于抛出一个异常类对象，通常用于处理自定义异常类情况。如thrMyexceptiono。
throws则是在方法声明时告诉调用者该方法需要抛出什么类型的异常，而异常的捕获处理交由调用该方法者去实施。如 int parselnt（ String s） throws Numberformatexception
# 流
说到流，输入输出流，什么字节流，字符流，有点晕有时候看着都。。。特别是什么字节流和字符流的区别，对于字节和字符的区别又开始有点乱了。。。。
记住：字节是单位，就像米，厘米，这种计量单位
字符，就是“ABCD1234中国”这些能被人看懂的符号，
字符需要用字节来衡量大小，比如 中国 这两个中文字符需要用到多少个字节来表示，
对于不同的编码，需要用到的字节数也不同，ASCII码，一个中文汉字为两个字节，UTF-8，一个中文汉字需要用三个字节，
所以中国在ASCII码的编码下需要用到2个字节来表示，在UTF8中要用3个。

**字节和字符的区别**
字节(Byte)是计量单位，表示数据量多少，是计算机信息技术用于计量存储容量的一种计量单位，通常情况下一字节等于八位bit。
字符(Character)计算机中使用的字母、数字、字和符号，比如'A'、'B'、'$'、'&'等。
一般在英文状态下一个字母或字符占用一个字节，一个汉字用两个字节表示。
![](_assets/Java%20问题集合/1617351593806-dc3fa3be-7760-47e5-8abc-01eb6435639b-20230104110430924.jpeg)
**字节与字符：**

- ASCII 码中，一个英文字母（不分大小写）为一个字节，一个中文汉字为两个字节。
- UTF-8 编码中，一个英文字为一个字节，一个中文为三个字节。
- Unicode 编码中，一个英文为一个字节，一个中文为两个字节。
- 符号：英文标点为一个字节，中文标点为两个字节。例如：英文句号 **.** 占1个字节的大小，中文句号 **。**占2个字节的大小。
- UTF-16 编码中，一个英文字母字符或一个汉字字符存储都需要 2 个字节（Unicode 扩展区的一些汉字存储需要 4 个字节）。
- UTF-32 编码中，世界上任何字符的存储都需要 4 个字节。
# Formatter类
Formatter类是一个printf样式格式化字符串的解析器
# 如何使用数据流（基本类型）
DataInputStream、DataOutputStream两个类
![image.png](_assets/Java%20问题集合/1617371104434-43eefc20-bf67-429f-bd2e-c3b33fe80793.png)



# 如何获得对象流（引用类型）
对象流都实现了ObjectInput或ObjectOutput接口
# transient关键字有何作用？
前面的对象流能保存对象的所有信息，但是有没有可能只保存一部分呢？即某些信息不需要保存，也不能保存的呢。如密码？
使用transient关键字修饰的属性，在保存对象的时候，该属性不会被保存。
![image.png](_assets/Java%20问题集合/1617371976968-56346855-dd0e-424d-b914-6ecad7f2c7fb.png)
![image.png](_assets/Java%20问题集合/1617372050415-4cb1171d-a104-4be7-8a7a-394589148625.png)

# SequenceInputStream类
# StreamTokenizer类
用来实现统计文本文件中的单词，字母个数的。
# 如何获取属性文件的值
new Properties( )
# 关于NIO——（New IO，或 Non-blocking IO）
NIO的核心对象有 通道Channel和缓冲区Buffer。
通道Channel和原来IO中的流差不多一个意思，数据的传递通过通道完成
发送给通道的数据需要先放到缓冲区，从通道读取的数据也需要先读到缓冲区

- 缓冲区

在新IO库中，所有的数据都是使用緩冲区（ Buffer）处理的。 Buffer是一个对象，它包含一些刚该出或者要写入的数据。这体现了与原IO的不同。使用流该写数据时，是没有级冲区的。新IO库中包含的级冲区类有 Bytebuffer、 Charbuffer、 Short Buffer、 Intbuffer、Long Buffer、 Float Buffer和 Doublebufifer。

- 通道

通道（ Channel）用来湊写数据，它是双向的，这点与流有明量不同，即不需要定义Inputstream和 Outputstream两个对象即可完成数据该写操作。同时，通道中传递的数据是以块为单位，因此永远不能将字节写入到通道中
# 如何使用NIO读、写、复制数据？
l.使用新IO该数据
使用新IO该入数据主要分为以下3步：
（1）从 Filelnputstrean类中获得 File Channel对象。
（2）创建緩冲区 Buffer。
（3）将数据从 Filechannel该入到 Buffer中。
2.使用新IO写数据
使用新IO写出数据主要分为以下3步：
（1）从 Fileoutputstream类中获得 Filechannel对象。
（2）创建緩冲区Bufr并放入要写出的信息。
（3）将緩冲区 Buffer中的数据使用通道写入到文件中。
3.使用新10复制数据
复制数据可以看作是该和写操作的结合，它也可以分为3步
（1）创建一个级冲区 Buffer
（2）从源文件该取数据到级冲区中
（3）将级冲区内容写入目标文件。
# NIO缓冲区内部是如何实现的？
为了方便理解，可以将緩冲区看作一个数组。在级冲区中，使用3个变量表示其在任意时刻的状态，即 position、 limit和 capacity。对于该入和写出操作，其作用类似。下面将以该入操作为例对其作用进行详细说明。
（1） position
position表示下一个该入的字节将存放在数组中的哪个位置。例如，级冲区该入了3个字节，则 position为3，即下一个该取的字节将保存在数组的第四个元素中
（2） limit
limit表示还有多少空间可用于保存数据， position应该小于等于 limit.。
（3） capacity
capacity表示级存区中最大的数据容量，即底层数组可以保存的元素个数。 limit绝对不能大于 capacity
# 什么是内存映射文件IO
内存映射文件IO是一种该写文件的方式，它比基于流和通道的方式快很多。在现代操作系统中，都提供了将文件映射到内存中的功能。通常映射的部分是实际该取或写入的部分。
# 枚举类不能继承其他的类
因为所有enum类型都继承Enum这个父类，自然无法再继续继承别的类
枚举类中可以增加域和方法
和使用类那样，在枚举中增加域和方法，从而可以完成复杂的操作。
编译器自动为枚举类型增加新方法，
values(),valueOf()
# 枚举类定义域和方法
（1）枚挙元素要写在域和方法前。
（2）编写完枚挙元素需要使用分号分隔域和方法。
（3）如果编写了构造方法，则要在定义枚挙元素时体现。
注意：方法权限修饰符只有private和无修饰符。不能使用构造方法来创建枚举类型对象。
![image.png](_assets/Java%20问题集合/1617421663078-f75b44a1-fc48-4cde-881a-c163ef105189.png)

# 类型参数命名是有哪些要求
使用泛型时，经常需要声明类型参数，请问它有什么命名要求？
类型参数名称通常是一个大写字母。这与普通变量的命名形成了鲜明的对比。其理由是为了明确区分类型变量与类名或者接口名。常见的类型参数名称如下。
E：元素，广泛用于Java集合框架。
K：键
N：数字
T：类型
V：值。
S、U、Ⅴ等：用于第二、三、四个类型变量。
# 泛型中的类型擦除是什么
思考这段代码输出什么？——true
![image.png](_assets/Java%20问题集合/1617613402522-a5d04fe6-2af2-4dc7-b374-b20c229bf8db.png)
泛型中不支持继承的关系，ArrayList<Number>和ArrayList<Integer>不是继承关系。
泛型不支持数组，不能泛化数组。即 T[] arr = new T[0]; 是不行的。

# 什么情况下会导致线程停止
停止的原因

- 执行过程中，出现了InterruptException异常，线程终止
- 调用sleep（）方法，当前线程停止，进入等待
- 另一个高优先级的线程需要执行，当前线程停止，进入等待
# 哪些接口可以创建有返回值的线程？
Thread类和Runnable接口可以实现线程，但是没有返回值；
可以使用Callable接口创建有返回值的线程。结合Future接口使用
# 哪个类可用于创建线程池？
Executor类
newCachedThreadPool（）和newFixedThreadPool（）方法

# 如何停止线程
stop不推荐。
# JDBC分类
JDBC—ODBC桥依靠ODBC驱动器和数据库通信。
本地API
JDBC网络驱动程序
本地协议驱动

# Statement和PreparedStatement的区别
Statement用于执行静态SQL语句。它在执行SQL语句时，必須指定一个事先准备好的SQL语句。
![image.png](_assets/Java%20问题集合/1617695272660-973f393c-a41f-43a5-befb-ed97bce5b4fc.png)
Preparedstatement表示预编译的SQL语句对象。在使用 Preparedstatement对象执行SQL命令时，SQL命令被数据库进行解析和编译，然后被放到命令级冲区。这样每当执行同一个 Preparedstatement对象时就会被再解析一次，而不是被再次编译。在预编译的SQL语句中，可以包含参数“？”。在执行时可以为参数设置参数值。例如：
![image.png](_assets/Java%20问题集合/1617695278665-55524cc4-7725-4f01-986e-699bc47d6aac.png)

# 数据库如何保存图片视频
一般而言，数据不保存图片视频等字节流大文件，一般存放指向实际存放的地址。
但也可以使用，只是会降级数据效率，增加数据库负担。Mysql中可以使用Blob对象
小点：
定义常量记得加final，
final int CONST = 10;
final修饰的类不允许有子类，final修饰的方法不允许被重写，final修饰的参数不允许被修改。

## Java 关键字 volatile

- volatile关键字的两层语义 一旦一个共享变量（类的成员变量、类的静态成员变量）被volatile修饰之后，那么就具备了两层语义：
- 1）保证了不同线程对这个变量进行操作时的可见性，即一个线程修改了某个变量的值，这新值对其他线程来说是立即可见的。
- 2）禁止进行指令重排序。
## Java关键字问题

- java关键字和保留字

![](_assets/Java%20问题集合/1602509994639-2c953d54-6700-4f07-952f-2faf073aeac6-20230104110544225.png)

- 1）比较少见/少用的
   - assert 断言，用来进行程序调试，用来查找内部的程序错误
   - goto 保留关键字，没有具体含义
   - instanceof 用来测试一个对象是否是指定类型的实例对象
   - native 有宿主系统实现的一个方法，用来声明一个方法是由与计算机相关的语言（如C/C++/FORTRAN语言）实现的
   - strictfp 对浮点数计算使用严格的规则，用来声明FP_strict（单精度或双精度浮点数）表达式遵循IEEE 754算术规范
   - synchronized 对线程而言是原子的方法或代码块
   - throw 抛出一个异常
   - throws 一个方法中可能抛出的异常
   - transient 标志非永久性的数据
   - volatile 确保一个字段可以由多个线程访问
- 2）2个保留字（现在没用以后可能用到作为关键字）：
   - goto、const。它们不是关键字
- 3）3个特殊直接量：
   - true、false、null 它们不是关键字
## JDK12安装与环境变量(Win)

   - 从JDK 9开始发生重大变化 - - - “之前类和资源文件存储在lib/rt.jar，lib/tools.jar，
   - JDK 9版本开始 lib/dt.jar和其他各种内部JAR文件都存储在一个更有效的格式在实现特定的文件lib目录。
   - 所以不需要配置CLASSPASTH变量。
## synchronized关键字

   - synchronized是不能继承的，也就是说，基类的方法synchronized f(){} 在继承类中并不自动是synchronized f( ){ }，而是变成了f( ){ }。继承类需要你显式的指定它的某个方法为synchronized方法
## 多进程与多线程有哪些区别呢？ 

   - 本质的区别在于每个进程拥有自己的一整套变量， 而线程则共享数据, 与进程相比较， 线程更“ 轻量级”， 创建、撤销一个线程比启动新进程的开销要小得多。
## Java instanceof Keyword
![](_assets/Java%20问题集合/1602509994649-e25168e0-5429-4948-914b-81563ccac640-20230104110553857.png)
## 数组扩容

- JKD1.6中实现是，如果通过无参构造的话，初始数组容量为10，每次通过copeOf的方式扩容后容量为原来的1.5倍，以上就是动态扩容的原理
## 数组/链表 访问

- 由数组支持的有序集合可以快速地随机访问，因此适合使用 List 方法并提供一个整数索引来访问。与之不同， 链表尽管也是有序的， 但是随机访问很慢，所以最好使用迭代器来遍历
- 为了避免对链表完成随机访问操作，Java SE 1.4 引入了一个标记接口 RandomAccess。这个接口不包含任何A方法， 不过可以用它来测试一个特定的集合是否支持高效的随机访问：
if (c instanceof RandomAccess){
    use random access algorithm
else{
use sequential access algorithm
}
## Apache POI

- 在 POI 中，Workbook代表着一个 Excel 文件（工作簿），Sheet代表着 Workbook 中的一个表格，Row 代表 Sheet 中的一行，而 Cell 代表着一个单元格。
- HSSFWorkbook对应的就是一个 .xls 文件，兼容 Office97-2003 版本。
- XSSFWorkbook对应的是一个 .xlsx 文件，兼容 Office2007 及以上版本。
- 在 HSSFWorkbook 中，Sheet接口 的实现类为 HSSFSheet，Row接口 的实现类为HSSFRow，Cell 接口的实现类为 HSSFCell。
- XSSFWorkbook 中实现类的命名方式类似，在 Sheet、Row、Cell 前加 XSSF 前缀即可。（XSSFSheet、XSSFRow、XSSFCell）
# Java 内部类
> 概念：顾名思义，就是定义在另外一个类里面的类。

好处有三：
内部类方法可以访问该类定义所在的作用域中的数据,包括私有的数据.
内部类可以对同一个包中的其他类隐藏起来
当想要定义一个回调函数且不想编写大量代码时,使用匿名( anonymous)内部类比较便捷.
