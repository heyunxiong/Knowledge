> Java 基础知识： Java IO ，文件处理

Java IO API 可以实现访问文件与目录，以及用二进制格式和文本格式读写数据
## IO 流
输入输出是相对程序来说的；
![](_assets/Java%20I_O%20输入输出/1636465373753-c0b30ad9-a513-4352-9636-9d1de11550db-2803077.jpeg)

### IO 流的家族概览图
需要明确的是：

- 最基本的四个抽象类：InputStream、OutputStream、Reader、Writer；其他类基本都是基于此。
- 最基本的⽅法是 read() 和 write() 

![](_assets/Java%20I_O%20输入输出/1636520808896-bdfcec54-d095-423a-ba0f-1c35d0e282dc.jpeg)
### IO 类成员介绍
#### 字节流与字符流
字节流一般适合于操作二进制类的文件，比如图片；字符流适合文本，更加高效。
原生的是字节流，字符流是经过处理的。

- 字节流操作的基本单元为字节；字符流操作的基本单元为Unicode码元。
- 字节流默认不使用缓冲区；字符流使用缓冲区。
- 字节流通常用于处理二进制数据，实际上它可以处理任意类型的数据，但它不支持直接写入或读取Unicode码元；字符流通常处理文本数据，它支持写入及读取Unicode码元。

总之一句话：字节流能代替字符流，反之不能；但在某些场景下，字符流更有优势。
#### 字节输入流
#### InputStream 
InputStream是字节输入流顶级抽象类
```java
public abstract class InputStream extends Object implements Closeable
```
InputStream定义的方法（来自API中文文档）

| 方法 | 描述 |
| --- | --- |
| int available()  | 返回从该输入流中可以读取（或跳过）的字节数的估计值，而不会被下一次调用此输入流的方法阻塞 |
| void close()  | 关闭此输入流并释放与流相关联的任何系统资源 |
| void mark(int readlimit)  | 标记此输入流中的当前位置 |
| boolean markSupported()  | 测试这个输入流是否支持 mark和 reset方法 |
| abstract int read()  | 从输入流读取数据的下一个字节 |
| int read(byte[] b)  | 从输入流读取一些字节数，并将它们存储到缓冲区 b  |
| int read(byte[] b, int off, int len)  | 从输入流读取最多 len字节的数据到一个字节数组 |
| void reset()  | 将此流重新定位到上次在此输入流上调用 mark方法时的位置 |
| long skip(long n)  | 跳过并丢弃来自此输入流的 n字节数据  |

#### FileInputStream
FileInputStream用于从文件读取数据，用关键字 new 来创建对象。
```java
// 继承了InputStream
public class FileInputStream extends InputStream{......}

// 直接使用指定文件名创建一个输入流对象来读取文件：
InputStream f = new FileInputStream("C:/java/file_1.txt");

// 通过File类对象，创建InputStream输入流对象
File f = new File("C:/java/file_1.txt");
InputStream in = new FileInputStream(f);
```
FileInputStream 常用的方法：

| 方法 | 描述 |
| --- | --- |
| public void close( )   | 关闭此文件输入流并释放与此流有关的所有系统资源。抛出IOException异常。 |
| protected void finalize( ) | 清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。抛出IOException异常。 |
| public int read(int r) | 从 InputStream 对象读取指定字节的数据。返回为整数值。返回下一字节数据，如果已经到结尾则返回-1。 |
| public int read(byte[] r) | 从输入流读取r.length长度的字节。返回读取的字节数。如果是文件结尾则返回-1。 |
| public int available( ) | 返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取的字节数。返回一个整数值。 |

#### 字节输出流
#### OutputStream
与InputStream相对，是字节输出流顶级抽象类
```java
public abstract class OutputStream extends Object implements Closeable, Flushable
```
OutputStream定义的方法（来自API中文文档）

| 方法 | 描述 |
| --- | --- |
| void close()  | 关闭此输出流并释放与此流相关联的任何系统资源。  |
| void flush()  | 刷新此输出流并强制任何缓冲的输出字节被写出。   |
| void write(byte[] b)  | 将 b.length字节从指定的字节数组写入此输出流。   |
| void write(byte[] b, int off, int len)  | 从指定的字节数组写入 len个字节，从偏移 off开始输出到此输出流。  |
| abstract void write(int b)  | 将指定的字节写入此输出流。  |

#### FileOutputStream
与FileInputStream相对；用于文件输出操作，即系把内容写出到目标路径下
```java
// 继承了OutputStream
public class FileOutputStream extends OutputStream

// 创建方式，直接使用目标路径的文件名
OutputStream f = new FileOutputStream("C:/java/file_output.txt")

// 通过File类对象作为指定为文件类型创建
File f = new File("C:/java/file_output.txt");
OutputStream fOut = new FileOutputStream(f);
```
FileOutputStream 常用的方法：

| 方法 | 描述 |
| --- | --- |
| public void close( ) | 关闭此文件输入流并释放与此流有关的所有系统资源。抛出IOException异常 |
| protected void finalize( ) | 清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。抛出IOException异常 |
| public void write(int w) | 把指定的字节写到输出流中 |
| public void write(byte[] w) | 把指定数组中w.length长度的字节写到OutputStream中 |

#### 字符输入流
#### Reader
字符输入流的顶级抽象类；用于读取字符流的抽象类。 
子类必须实现的唯一方法是read（char [ ]，int，int)和close( )
```java
public abstract class Reader extends Object implements Readable, Closeable
```
#### FileReader

- 方便读取字符文件，该类的构造函数假定默认字符编码和默认字节缓冲区大小
- FileReader是用于读取字符流
```java
public class FileReader extends InputStreamReader
```
#### 字符输出流
#### Writer
与字符输入流Reader相对，是字符输出流顶级抽象类。用于写入字符流的抽象类。 
子类必须实现的唯一方法是write（char []，int，int），flush（）和close（）
```java
public abstract class Writer extends Object implements Appendable, Closeable, Flushable
```
#### FileWriter

- 方便写字符文件， 该类的构造函数假定默认字符编码和默认字节缓冲区大小
- FileWriter是用于写入字符流
```java
public class FileWriter extends OutputStreamWriter
```
### IO流 Demo
```java
// 输入输出操作：
// 1.字节流 
public void testInput() throws IOException{

        //1.创建FileInputStream
        File file = new File("E:\\test_input.txt");
        InputStream fileInputStream = new FileInputStream(file);
        //2.读取文件
        // a.单个字节读取
        int data = 0;
        while((data = fileInputStream.read()) !=-1 ){ // -1为文件结尾，只要不是文件结尾就一直读取；
            System.out.print(data); // 直接打印出来是的ASCII编码字符集
            System.out.print((char)data); // 打印出字符,如果是中文或者不在ASCII定义的字符，需要进行转换
            System.out.println("");
        }

        // b.以数组形式读，提高读的效率
        // 定义byte[]数组: 准备数据篮子，read时候就会把文件的内容装进去，
        // 但是如果当前读取数据的大小超过篮子, 当次只会存篮子的大小上限内容，超过的内容需要到下一次读取
        // 比如new byte[3]现在一次读3个字节，而文件中的内容长度为6，就需要调用两次read()才能读完
        //int length = fileInputStream2.read(dataArray);// 一次性读取的长度1024个字节,此时文件内容已放入byte数组里面

        InputStream fileInputStream2 = new FileInputStream(file);
        byte dataArray[] = new byte[1024];
        int length = 0;

        while ((length = fileInputStream2.read(dataArray))!= -1){ //一直读到文件结尾，-1代表内容结尾
            System.out.println("文件内容的长度为："+length);
            System.out.println("文件内容: " + new String(dataArray, 0, length));
        }

        //3.关闭流
        fileInputStream.close();
        fileInputStream2.close();
    }

public void testOutput() throws  IOException{

        // 1.输出文件路径
        String targetPath = "E:\\test_output.txt";
        // 创建输出文件字节流
        FileOutputStream fileOutputStream = new FileOutputStream(targetPath);
        // 准备写出到文件的内容
        String content ="hello,sean! 你好";
        
        // 2.获取内容的字节形式，并写出
        byte[] bytes = content.getBytes();
        fileOutputStream.write(content.getBytes()); // 直接写出内容
        fileOutputStream.write(bytes,0,bytes.length); //写出length大小的内容

        // 3.关闭流
        fileOutputStream.close();
    }


public void testInputAndOutput()  throws IOException{
        // 读取test_input后，写到test_output中
    
        // 1.分别定义字节输入流、字节输出流
        String inputFilePath = "E:\\test_input.txt";
        InputStream fis = new FileInputStream(inputFilePath);
        String outputFilePath = "E:\\test_output.txt";
        OutputStream fos = new FileOutputStream(outputFilePath);
    
        // 2.准备数据篮子
        byte data[] = new byte[2];
        int length =0;
        // 3.读取文件
        while ((length = fis.read(data))!=-1) {
        // 4.写出文件
            fos.write(data,0,length);
        }
        // 5.关闭流
        fos.close();
        fis.close();
    }

// 2.字符流 TO-DO 大同小异
```
## File 类
File类是文件和目录路径的抽象表示，能获取和修改文件的属性，但是无法对文件内容进行操作。
```java
public class File extends Object implements Serializable, Comparable<File>
```
### File类 Demo
```java
// 文件操作： 重命名
package com.sean.demo;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.io.File;

public class IOTest {
    private static final Logger LOGGER = LoggerFactory.getLogger(IOTest.class);
    public static void main(String[] args) {
        String path = "E:\\Music\\MV";      // 要遍历的路径
        File file = new File(path);         // 通过文件路径获取其File对象
        new IOTest().rename(file);
    }
    public void rename(File file) {
        LOGGER.info("==> rename() start");
        
        File[] files = file.listFiles();
        for (File f : files) {
            if (f.isDirectory()) {
                LOGGER.info("This is a Directory: "+f.getAbsolutePath());
                rename(f);   // 递归遍历
            } else {
                String fileAbsolutePath = f.getAbsolutePath();
                String filePath = f.getPath();
                String fileName = f.getName();
                String fileParent = f.getParent();
                
                LOGGER.info("fileAbsolutePath: " + fileAbsolutePath);
                LOGGER.info("filePath: " + filePath);
                LOGGER.info("fileName: " + fileName);
                LOGGER.info("fileParent: " + fileParent);
                
                String renamePath = fileParent + "\\" + "_rename_" + fileName;
                f.renameTo(new File(renamePath));
                LOGGER.info("==> rename() done");
            }
        }
    }
}

```
## 关于序列化与反序列化
序列化：把内存对象写出到指定目录下；
反序列化：读取指定文件重构成内存对象
注意事项：

- 序列化需要实现Serializable接口，该接口仅仅是表示对象能够进行序列化
- 如果类中有对象属性，那么要求该对象也需要实现Serializable接口（比如 Student类中有 Address类对象，Address也需要实现Serializable接口）
- serivalVersionUID， 能保证序列化和反序列化类是同一个类
- 使用transient修饰的属性，该属性不会被序列化 
- 静态属性无法序列化
```java
//---------Student.java----------
package com.sean.demo;
import lombok.AllArgsConstructor;
import lombok.Data;
import java.io.Serializable;

/**
 * @author Yunxiong
 */
@Data
@AllArgsConstructor
public class Student implements Serializable {

    private static final long serialVersionUID = 100L;

    private String name;
    private transient int age; // transient 修饰的属性不会被序列化/反序列化
    private Address address;
}

//---------Address.java----------
package com.sean.demo;
import lombok.AllArgsConstructor;
import lombok.Data;
import java.io.Serializable;

/**
 * @author Yunxiong
 */
@Data
@AllArgsConstructor
public class Address implements Serializable {

    private static final long serialVersionUID = 200L;

    private String address;
}

//---------Test.java----------

public void testSerializable() throws IOException, ClassNotFoundException {
        // 序列化对象， 既写出对象，到二进制文件中
        OutputStream outputStream = new FileOutputStream(new File("E:\\stu.bin"));
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(outputStream);

        Student student = new Student("sean",10,new Address("guangzhou"));

        objectOutputStream.writeObject(student);
        System.out.println("序列化成功");

        // 反序列化对象, 即系读取
        InputStream intputStream = new FileInputStream("E:\\stu.bin");
        ObjectInputStream objectInputStream = new ObjectInputStream(intputStream);
        Student student1 = (Student)objectInputStream.readObject();

        System.out.println("反序列化成功");
        System.out.println(student1.toString());


        //关闭流
        objectInputStream.close();
        intputStream.close();
        objectOutputStream.close();
        outputStream.close();
    }
```

如果序列号版本ID不一致会抛出异常：InvalidClassException
```java
Exception in thread "main" java.io.InvalidClassException: com.sean.demo.Student; local class incompatible: stream classdesc serialVersionUID = -6053982940036532652, local class serialVersionUID = 100
	at java.io.ObjectStreamClass.initNonProxy(ObjectStreamClass.java:699)
	at java.io.ObjectInputStream.readNonProxyDesc(ObjectInputStream.java:1939)
	at java.io.ObjectInputStream.readClassDesc(ObjectInputStream.java:1805)
	at java.io.ObjectInputStream.readOrdinaryObject(ObjectInputStream.java:2096)
	at java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1624)
	at java.io.ObjectInputStream.readObject(ObjectInputStream.java:464)
	at java.io.ObjectInputStream.readObject(ObjectInputStream.java:422)
```
