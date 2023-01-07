> Java 基础知识： 数组

# 数组的概述

1. 数组（Array）是由多个相同类型的数据按一定顺序排列的集合；使用同一个引用并通过编号的方式对这些数据进行统一管理。
2. 数组中的常见概念
   1. 数组名
   2. 元素
   3. 角标、下标、索引
   4. 数组的长度：元素的个数
4. 数组的特点
   1. 数组是有序排列的
   2. 数组属于引用数据类型的变量。数组的元素，既可以是基本数据类型，也可以是引用数据类型
   3. 创建数组对象会在内存中开辟一整块连续的空间
   4. **数组的长度一旦确定，就不能修改。**
5. 数组的分类
   1. 按照维度：一维数组，二维数组。。。。
   2. 按照元素类型：基本数据类型元素的数组，引用数据类型元素的数组
# 一维数组
## 声明和初始化
```java

int num; //声明变量
num = 18; //初始化变量
int id = 161; //声明+初始化 变量

int[] ids; //声明数组
ids = new int[] {101,1082,103,14}; //静态初始化：数组的初始化和数组元素的赋值操作同时进行
String[] names = new String[5]; //动态初始化：数组的初始化和数组元素的赋值操作分开进行
int[] arr4 = {1,2,3,4}; //省略也是正确的写法：类型推断

```
## 下标的使用
如何调用数组的指定位置的元素：通过角标的方式调用。
数组的角标（或索引）从 **0 **开始的，到数组的 **长度-1** 结束。
> 题外charAt() 方法也是定位下标，

## 如何获取数组的长度。
通过数组属性 length
```java
System.out.println(names.length);
System.out.println(ids.length);
```
## 如何遍历数组
```java
//逐个输出显得有点累
System.out.println(names [0]); 
System.out.printin(names [1]);
System.out.println(names [2]);
System.out.println(names [3]);
System.out.println(names [4]);
//通过循环的方式输出，循环的方式有好几种，用自己习惯的就好！
for (int i = 0; i < names.length; i++){
	System.out.println(names[i]);
	}
```
## 数组元素的默认初始化值
数组元素是整型：0
数组元素是浮点型：0.0
数组元素是char型：0或 '\u0000'，而非 '0'，这个是 '0' 表示字符
数组元素是 boolean型：false
数组元素是引用数据类型：null 而不是 "null"
## 数组的内存结构
![image.png](_assets/Java%20数组/1600501680544-9413496c-d2ed-4b81-8eb1-43a545fff18b.png)
![image.png](_assets/Java%20数组/1600504040585-0260ce69-9ef3-485c-b0c7-e11f836e1888.png)

# 二维数组
## 二维数组的声明和初始化
```java
public class ArrayTest2{
	public static void main(String[] args){
	//1.二维数组的声明和初始化
	int[] arr= new int[]{1,2,3}; // 一维数组
	//静态初始化
	int[][]arr1= new int[][]{{1,2,3},{4,5},{6,7,8}};
	//动态初始化
	String[][] arr2 new String[3][2];
	String[][] arr3 new String[3][];
	//其他正确的写法
	int[]arr4[]= new int[]{{1,2,3},{4,5},{6,7,8}]; 
	int[]arr5[]={{1,2,3},{4,5},{6,7,8}};
    }
```
## 调用二维数组的指定元素
```java
//2.如何调用数组的指定位置的元素
System.out.println(arr1[0][1]);//2
System.out.println(arr2[1][1]);//null 
arr3[1]= new String[4];
System.out.println(arr3[1][0]);

```
## 如何获取二维数组的长度
```java
//获取数组的长度
System.out.println(arr4.length);//3 
System.out.println(arr4[0].length);//3
System.out.println(arr4[1].length);//2
```
![image.png](_assets/Java%20数组/1608605533094-191c6dff-de21-49f9-a166-ab60da18d5e6.png)
## 如何遍历二维数组
```java
//双for循环
for(int i = 0; i< arr4.length; i++){
	for(int j = 0; j < arr4[i].length; j++){
		System. out. print(arr4[i][j]+""); 
	}
}
```
## 二维数组的使用
规定：二维数组分为外层数组的元素，内层数组的元素
int [ ][ ] arr =  new int [4][3];
外层元素：arr[0], arr[1] 等
内层元素：arr[0][0]，arr[1][2]等

数组元素的默认初始化值针对于初始化
方式一：比如：int [][] arr= new int [4][3]; 
外层元素的初始化值为：地址值 
内层元素的初始化值为：与一维数组初始化情况相同 针对于初始化
方式二：比如：int [ ][ ] arr= new int [4] [ ]；
外层元素的初始化值为：null
内层元素的初始化值为：不能调用，否则报错
```java
public class ArrayTest3{
    public static void main(String[] args){
		int [][] arr = new int[4][3];
		System.out.printin(arr);//[[I@6de6d69c 地址值
		System.out.println(arr[0][0]);//0
		System.out.println("*****************");
		float[][] arr1 = new float[4][3];
		System.out.print1n(arr1[0]);//地址值
		System.out.println(arr1[0][0]);//0.0
		System.out.println("*****************");
		String[][] arr2 = new String[4][21];
		System.out.print1n(arr2[1]);//地址值
		System.out.println(arr2[1][1]);//null 
		System.out.println("*****************");
		double[][] arr3 = new double[4][];
		System.out.println(arr3[1]);//null 
		System.out.println(arr3[1][]);//0L
	}
}
```
## 二维数组的内存解析
![image.png](_assets/Java%20数组/1600503889336-a45d06ce-6235-40bf-8bfb-ad648738703e.png)
# Arrays工具类的使用
操作数组的工具类，包含各种操作数据的方法。开发过程中可以先去该工具类中查找是否有你要的方法，调用即可，这样就不用自己再去花时间写了。

| 常用方法 | 描述 |
| --- | --- |
| boolean equals （int [ ] a, int [ ] b)  | 判断两个数组是否相等2  |
| String toString  (int [ ] a) | 输出数组信息 |
| void fill ( int [ ] a, int val) | 将指定值填充到数组之中。 |
| void sort (int [ ] a) | 对数组进行排序。 |
| int binarySearch (int [ ] a, int key) | 对排序后的数组进行二分法检索指定的值 |

# 数组中常见的异常

- 数组下标越界的异常：ArrayIndexOutfBoundsException
- 空指针异常：NullPointerException

