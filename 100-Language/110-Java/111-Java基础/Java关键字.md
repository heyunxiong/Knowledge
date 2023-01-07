比较陌生的Java关键字

1)java关键字和保留字
```java
abstract class extends implements null strictfp true

assert const false import package super try

boolean continue final instanceof private switch void

break default finally int protected synchronized volatile

byte do float interface public this while

case double for long return throw

catch else goto native short throws

char enum if new static transient

```
  
assert  断言，用来进行程序调试，用来查找内部的程序错误

goto     保留关键字，没有具体含义

instanceof      用来测试一个对象是否是指定类型的实例对象

native   有宿主系统实现的一个方法，用来声明一个方法是由与计算机相关的语言（如C/C++/FORTRAN语言）实现的

strictfp  对浮点数计算使用严格的规则，用来声明FP_strict（单精度或双精度浮点数）表达式遵循IEEE 754算术规范

synchronized   对线程而言是原子的方法或代码块

throw   抛出一个异常

throws      一个方法中可能抛出的异常

transient 标志非永久性的数据

volatile   确保一个字段可以由多个线程访问

  

2）2个保留字（现在没用以后可能用到作为关键字）：goto、const。它们不是关键字

3）3个特殊直接量：true、false、null。它们不是关键字。