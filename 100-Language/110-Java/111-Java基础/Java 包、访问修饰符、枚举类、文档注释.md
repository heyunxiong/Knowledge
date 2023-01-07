> Java 基础知识： 包 、访问权限符、枚举类

## 包 package
借助包可以方便的组织代码，包具有一个层次结构，如果硬盘的目录结构一般，多层次嵌套组织。
使用包的主要原因是确保类名的唯一性。 假如有两个Employee类。 只要将这些类放置在不同的包中 ， 就不会产生冲突
com.sean.Employee.java
com.jack.Employee.java
## 访问修饰符
![](_assets/Java%20包、访问修饰符、枚举类、文档注释/1602509994595-b67af621-36b8-4905-8864-4ab95d766927.png)
## 枚举类
如果能穷举的情况下，可以使用枚举类
说实话，我总感觉是一种常量类。
```java
public enum Color {
	RED, GREEN, YELLOW, BLUE；
}

//---使用枚举类
public class Test{
    // 执行输出结果
    public static void main(String[] args)
    {
        Color c1 = Color.RED;
        System.out.println(c1);
    }
}
```
## 文档注释
使用javadoc，能把源文件生成一个html文档，作为接口API文档

- 类注释
```java
/**
 * 这是文档注释
 */


/*
 * 这是一般注释
 */


// 这是一般注释
```
```java

/**
 * Class {@code Object} is the root of the class hierarchy.
 * Every class has {@code Object} as a superclass. All objects,
 * including arrays, implement the methods of this class.
 *
 * @author  unascribed
 * @see     java.lang.Class
 * @since   JDK1.0
 */
public class Object {

}
```
Javadoc标签：[参考标签](https://www.runoob.com/java/java-documentation.html)

| @author | 标识一个类的作者 | @author description |
| --- | --- | --- |
| @deprecated | 指名一个过期的类或成员 | @deprecated description |
| {@docRoot} | 指明当前文档根目录的路径 | Directory Path |
| @exception | 标志一个类抛出的异常 | @exception exception-name explanation |
| {@inheritDoc} | 从直接父类继承的注释 | Inherits a comment from the immediate surperclass. |
| {@link} | 插入一个到另一个主题的链接 | {@link name text} |
| {@linkplain} | 插入一个到另一个主题的链接，但是该链接显示纯文本字体 | Inserts an in-line link to another topic. |
| @param | 说明一个方法的参数 | @param parameter-name explanation |
| @return | 说明返回值类型 | @return explanation |
| @see | 指定一个到另一个主题的链接 | @see anchor |
| @serial | 说明一个序列化属性 | @serial description |
| @serialData | 说明通过writeObject( ) 和 writeExternal( )方法写的数据 | @serialData description |
| @serialField | 说明一个ObjectStreamField组件 | @serialField name type description |
| @since | 标记当引入一个特定的变化时 | @since release |
| @throws | 和 @exception标签一样. | The @throws tag has the same meaning as the @exception tag. |
| {@value} | 显示常量的值，该常量必须是static属性。 | Displays the value of a constant, which must be a static field. |
| @version | 指定类的版本 | @version info |

