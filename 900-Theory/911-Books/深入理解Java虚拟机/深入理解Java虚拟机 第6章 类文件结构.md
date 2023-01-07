第三部分  虚拟机执行子系统
# 第6章 类文件结构

## Class类文件的结构
是什么？
Class文件是一组**以8个字节为基础单位**的二进制流，严格排列，中间没有任何分隔符；大于8个字节，按照高位在前的方式分割成若干8个字节存储。
类似于C语言结构体的伪结构，只有两种数据类型：无符号数，表
- 无符号数属于基本的数据类型，u1、u2、u4、u8表示1个字节，2个字节，4个字节和8个字节的无符号数；可以是数字、索引引用、数量值或UTF-8编码集中的字符串
- 表是由多个无符号数或者其他表作为数据项构成的复合数据类型，以“\_info" 结尾

Class文件格式，无论是顺序还是数量，都是严格按照顺序限制的，不能改变
![](_assets/深入理解Java虚拟机%20第6章%20类文件结构/image-深入理解Java虚拟机%20第6章%20类文件结构-20221022-154708276.png)
Class文件张什么样？
左边是class字节码，右边是该字节码文件对应的十六进制（Idea使用插件 BinED）
![](_assets/深入理解Java虚拟机%20第6章%20类文件结构/image-深入理解Java虚拟机%20第6章%20类文件结构-20221022-161310738.png)

### 魔数与Class文件的版本
魔数，每个Class文件的头四个字节被称为魔数，magic number；作用就是确定这个文件是否为一个能被虚拟机接受的Class文件。（Gif和Jepg文件头都有魔数）用十六进制表示的：0xCAFEBABE
接着之后的Class文件的版本号，第5、6个字节是次版本号（miner version），第7，8个是主版本号（major version）Java的版本号是从45开始的，jdk向下兼容版本号，但不能执行比版本号高的Class文件。

### 常量池
是什么？
是Class文件结构中与其他项目关联最多的数据，也是占用Class文件空间最大的数据项目之一，是一个表类型的数据项目
入口放置一项u2类型的数据，代表常量池的容量计数值 constan_pool_count。Class文件只有常量池的容量计数是从1开始的。上图十六进制表示的Class文件中，第10个字节16，即十进制的22，表示常量池有21项常量，索引值从1~21。
只要存放两大类变量：字面量literal和符号引用 symbolic references
每种常量类型有各自独立的数据结构

### 访问标志 access_flags
接在常量池后的是用2个字节表示的访问标志，这个访问标志用于识别类或者接口层次的访问信息。
是类还是接口；是否定义为public类型；是否定义为abstract类型；是否被声明为final

### 类索引、父索引、接口索引集合
类索引 this_class 和父索引 super_class 都是u2类型的数据项，而接口索引集合是interfaces是一组u2类型的数据的集合。
Class文件由这三项数据来确定该类型的继承关系。
类索引用于确定这个类的全限定名
父类索引确定这个类的父类的全限定名
接口索引集合用来描述这个类实现了哪些接口

### 字段表集合
字段表 field_info 描述接口或类中声明的变量。包括类级变量和实例级变量，不包括方法内部的局部变量
字段表集合不会列出从父类或者父接口中继承而来的字段

### 方法表集合
和字段表类似的数据结构表示
访问标志、名称索引、描述符索引、属性表集合
如果父类方法在子类中没有被重写override，方法表集合中就不会出现来自父类的方法信息。

### 属性表集合
属性表attribute_info 描述场景的专用信息；如Class文件的属性信息，字段表的属性信息，方法表的属性信息

### 小结
上面每个Class文件的数据项都有复杂严格的结构规范，书中有多个表格对其各自进行总结分析，如果想了解详细的，建议重新看看书，属于是比较“枯燥”的概念和介绍内容。// P215~P250


## 字节码指令简介
java虚拟机的指令由一个字节长度的、代表着某种特定操作含义的数字（操作码，Opcode）以及跟随其后的零至多个代表此操作所需的参数构成（操作数，Operand）// 我顶，一个定义定语搞这么长，把人都绕晕了；我自己理解的：java指令的长度为一个字节，该字节表示操作，后面跟上操作数，比如：add 1 2 表示 1和2相加。

字节码指令的优缺点
缺：操作码的长度只为一个字节（即0~255）操作码总数不能超过256条；操作数长度不对齐，超过一个字节长度的数据，不得不重建出具体的数据结构，损失性能。
优：放弃操作数的长度对齐，可以省略大量的填充和间隔符号

### 字节码与数据类型
大多数指令都包含其操作所对应的数据类型信息。比如：iload指令，用于从局部变量表中加载int类型的数据到操作栈中；fload则表示加载float类型的数据；指令的操作在虚拟机内部可能会由同一段代码实现，但在Class文件中操作码要分开独立表示
常见的：i表示对int的操作，l表示long，s表示short，b表示byte，c表示char，f表示float，d表示double，a表示reference

### 加载和存储指令
加载和存储指令用于将数据在栈帧中的局部变量表和操作数栈之间来回传输。
- 将一个局部变量加载到操作栈：iload、iload_<n>、lload、lload_<n>、fload、fload_<n>、dload、dload_<n>、aload、aload_<n>
- 将一个数值从操作数栈存储到局部变量表：istore、istore_<n>、lstore、lstore_<n>、fstore、fstore_<n>、dstore、dstore_<n>、astore、astore_<n>
- 将一个常量加载到操作数栈：bipush、sipush、ldc、ldc_w、ldc2_w、aconst_null、iconst_m1、iconst_<i>、lconst_<l>、fconst_<f>、dconst_<d>
- 扩充局部变量表的访问索引的指令：wide

### 运算指令
算术指令，对操作数栈上的两个值进行某种特定运算，并把结果重新存入到操作栈顶。无论哪种算术指令，都是用java虚拟机的算术类型来进行计算的，对于不支持算术指令的byte、short、char和boolean类型应该使用操作int类型的指令代替。
算术指令有如下：
- 加法：iadd、ladd、fadd、dadd
- 减法：isub、lsub、fsub、dsub
- 乘法：imul、lmul、fmul、dmul
- 除法：idiv、ldiv、fdiv、ddiv
- 求余：irem、lrem、frem、drem
- 取反：ineg、lneg、fneg、dneg
- 位移：ishl、ishr、iushr、lshl、lshr、lushr
- 按位或：ior、lor
- 按位与：iand、land
- 按位异或：ixor、lxor
- 局部变量：iinc
- 比较：dcmpg、dcmpl、fcmpg、fcmpl、lcmp

问题注意：精度控制，向上取整、向下取整问题

### 类型转换指令
类型转换指令可以将两种不同的数值类型相互转换，一般用于用户代码中的显式类型转换操作；
java虚拟机直接支持（即无须显式的转换指令）：widening numberic conversion 即小范围类型向大范围类型的安全转换
int --> long, float, doblue;
long --> float, double;
float --> double
相反的，窄化类型转换 narroing numberic conversion，就必须显式地使用转换指令来完成；窄化类型转换可能会导致转换结果产生不同地正负号，不同地数量级，精度丢失等情况
操作指令有：i2b, i2c, i2s, l2i, f2i, f2l, d2i, d2l和d2f

### 对象创建与访问指令
java虚拟机对类实例和数组地创建与操作使用了不同的字节码指令
- 创建类实例的指令：new
- 创建数组的指令newarray、anewarray、multianewarray
- 访问类字段（static字段，或者称为类变量）和实例字段（非static字段，或者称为实例变量）的指令：getfield、putfield、getstatic、putstatic
- 把一个数组元素加载到操作数栈的指令：baload、caload、saload、iaload、laload、faload、daload、aaload
- 将一个操作数栈的值存到数组元素中的指令：bastore、castore、sastore、iastore、fastore、dastore、aastore
- 取数组长度的指令：arraylength
- 检查类实例类型的指令：instanceof、checkcast


### 操作数栈管理指令
直接操作操作数栈的指令：
- 将栈顶的一个元素或者两个元素出栈指令：pop、pop2
- 复制栈顶一个或者两个数值并将复制值或者双份复制值重新压入栈顶：dup、dup2、dup_x1、dup2_x1、dup_x2、dup2_x2
- 将栈顶两个元素互换 swap

### 控制转移指令
控制转移指令可以让java虚拟机有条件或者无条件地从指定位置指令的下一条指令继续执行程序，即修改程序计数器（pc寄存器）的值
- 条件分支：ifeq、iflt、ifle、ifne、ifgt、ifge、ifnull、ifnonnull、if_icmpeq、if_icmpne、if_icmplt、if_icmpgt、if_icmple、if_icmpge、if_acmpe和if_acmpne
- 复合条件分支：tableswitch、lookupswitch
- 无条件分支：goto、goto_w、jsr、jsr_w、ret

### 方法调用和返回指令
- invokevirtual指令：用于调用对象的实例方法，根据对象的实际类型进行分派（虚拟机分派）；最常见的分派方式
- invokeinterface指令：用于调用接口方法，它会在运行时搜索一个实现了这个接口方法的对象，找出适合的方法进行调用。
- invokespecial指令：用于调用一些需要特殊处理的实例方法，包括实例初始化方法、私有方法、父类方法
- invokestatic指令：用于调用类静态方法（static方法）
- invokedynamic指令：用于在运行时动态解析出调用点限定符所引用的方法。并执行该方法。前面几条调用指令的分派逻辑都固化在Java虚拟机内部，用户无改变，而invokedynamic指令是由用户所设定的引导方法决定的

方法调用指令和数据类型无关，而方法返回指令是根据返回值地类型区分的 ireturn （返回的是 boolean，byte，short，char，int），lreturn返回long，freturn返回float，dreturn返回double，areturn返回reference，


### 异常处理指令
java程序中显式地抛出异常操作throw语句，由**athrow指令**来实现


### 同步指令
方法级别的同步和方法内部的同步都有”锁“实现，也叫管程Monitor。

方法级别的同步是隐式的，无须通过字节码指令控制，它实现在方法调用和方法返回操作中。

虚拟机从方法常量池中的方法表结构中的ACC_SYNCHRONIZED访问标志得知方法是否被声明为同步方法。当方法被调用时，如果设置了该标志，执行线程就要求先成功持有管程（锁），然后执行方法，最后当方法完成（不管正常还是不是正常）释放管程（锁）

java用synchronized语句块来表示同步，java虚拟机对应的指令是：**monitorenter和monitorexit**来支持该关键字的语义




 
2022年10月22日
Yunxiong