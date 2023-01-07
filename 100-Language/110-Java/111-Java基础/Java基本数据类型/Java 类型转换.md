> Java 基础知识： 类型转换

Java 中的类型转换主要包括 ： 

- 自动类型转换
- 强制类型转换
# 自动类型转换 
本数据类型之间的运算规则：7种基本数据类型变量间的运算，不包含 boolean类型

- 自动类型提升结论：

**当容量小的数据类型的变量与容量大的数据类型的变量做运算时，结果自动提升为容量大的数据类型。**
**即：小转大，加容量。 **容量大小指的是，表示数的范围的大和小。
byte、char、 short -- > int --> long -- > float --> double
比如：float容量要大于long的容量, float 4个字节，long 8个字节；
long 和 float 做运算是等于float。
byte、char、 short 这三个类型之间做运算都是都等于int，包括同类型之间也是int，比如 byte+byte = int
```java
// TO-DO 
public void testTransClass(){

//....
}
```
# 强制类型转换
强制类型转换：自动类型提升运算的逆运算。
1.使用强转符：（）
如 ： Object obj = new Object( );
  String s = (String) obj;
2.注意点：强制类型转换，可能导致精度损失。
```java
class Test3{
	public static void main(String args[]){
		double d1=13.9； 
		int i1 = (int)d1；//截断操作
		System.out.println(i1); 
		long l1=123；
		short s2=（short）11；
	}
}
```

