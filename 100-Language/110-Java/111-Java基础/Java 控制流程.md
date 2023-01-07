> Java 基础知识： 控制流程

## Java中的控制流程 
if-else; if-elseif-else; while; do-while; for; for-each....
控制流程主要是进行条件判断，重复性操作等
## 条件语句
主要是使用if 和 switch 进行条件判断
### if 条件语句
单独判断
```java
int age = 20;
if(age > 10){
    System.out.println("age > 10, your age: " + age);
    return true; 
}
return false;
```
### if-else 条件语句
两种情况判断，满足则进行某种处理，否则进行另一种处理
```java
int age = 20;
if(age > 10){
    System.out.println("age > 10, your age: " + age); 
}else{
    System.out.println("age < 10, your age: " + age);
}
```
### if-elseif-else 条件语句
多支判断条件
```java
int age = 20;
if(age > 30){
    System.out.println("age > 30, your age: " + age);
}else if (age > 15){
	System.out.println("age > 15, your age: " + age);
}else{
    System.out.println(" your age: " + age);
}
```
### switch 多分支语句
多支判断switch 形式
case 标签可以是 ：

- 类型为 char 、 byte、 short或 int 的常量表达式
- 枚举常量
- 字符串字面量
```java
switch (week) {
	case 1:
		System.out.println("周一");
		break;
	case 2:
		System.out.println("周二");
		break;
	case 3:
		System.out.println("周三");
		break;
	case 4:
		System.out.println("周四");
		break;
	case 5:
		System.out.println("周五");
		break;
	case 6:
		System.out.println("周六");
		break;
	case 7:
		System.out.println("周日");
		break;
	default:
		System.out.println("无");
		break;
}
```
## 循环语句
while , do-while, for， for-each
### while 循环语句
_while(condition){ statement }_
当 (布尔值) 为 true 的时候，执⾏下⾯的表达式，布尔值为 false 的时候，结束循环
```java
int a = 10;
while(a > 5){
	a--;
}
```
### do-while 循环语句
while 与 do...while 循环的唯⼀区别是 do...while 语句⾄少执⾏⼀次，即使第⼀次的表达式为 false。
⽽在 while 循环中，如果第⼀次条件为 false，那么其中的语句不会执⾏。
```java
int b = 20;
// do···while循环语句
do {
System.out.println("b == " + b);
b--;
} while(b == 5);
```
### for 循环语句
确定循环次数的话，可以使用for循环；
for（初始化；布尔表达式；步进操作）{ 执行语句。。。}
```java
// 循环打印i的值
for(int i =0; i < 10 ; i++){
	System.out.println("i = "+i);
}
```
### for-each 语句
jdk1.5 简洁遍历方式， 方便对数组和集合进行操作
```java
int array[] = {1,2,3,4,5,6,7,8,9};

for (int e : array) {
	System.out.println(e);
}

```
## 跳转语句
中断控制流程
### break 语句
它是⽤于终⽌循环的操作， break 语句在for、while、do···while循环语句中，表示强⾏退出当前循环
```java
for(int i = 0;i < 10;i++){
	if(i == 5){
		break; // 只要i等于5，就跳出循环，剩下的i =6,7,8，9都会不执行了
	}
    System.out.println("i = "+i)
}
```
### continue 语句
continue 也可以放在循环语句中，它与 break 语句具有相反的效果，它的作⽤是⽤于执⾏下⼀次循环，
⽽不是退出当前循环
```java
for(int i = 0;i < 10;i++){
	if(i == 5){
	System.out.printl("continue ... ");  //i等于5，跳出此次循环，进入下一次
    continue;  						//下面的打印就不会出现 "i=5", 但是后续的 i6,7,8会继续打印
	}
    System.out.printl(" i = " + i );
}
```
### return 语句
return 语句表示返回，并把控制权交给调⽤它的语句
```java
public String say(){
	return "hello";
}
```
