> Java 基础知识：多线程

## 示例代码块
```java
package hyx.ch1_03;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/21/2020
 */
public class MyThread extends Thread {
    private int i = 0;

    public MyThread(int i) {
        this.i = i;
    }

    @Override
    public void run() {
        System.out.println("====>"+i);
    }
}

```
```java
package hyx.ch1_03;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/21/2020
 */
public class TestThread {
    public static void main(String[] args) {
        MyThread t01 = new MyThread(1);
        MyThread t02 = new MyThread(2);
        MyThread t03 = new MyThread(3);
        MyThread t04 = new MyThread(4);
        MyThread t05 = new MyThread(5);
        MyThread t06 = new MyThread(6);
        MyThread t07 = new MyThread(7);
        MyThread t08 = new MyThread(8);
        MyThread t09 = new MyThread(9);
        MyThread t10 = new MyThread(10);

        t01.start();
        t02.start();
        t03.start();
        t04.start();
        t05.start();
        t06.start();
        t07.start();
        t08.start();
        t09.start();
        t10.start();
    }
}

```
## 运行结果
![image.png](_assets/线程start()顺序不代表执行run()的顺序/1598018038668-4d3c02d0-becd-47d5-b316-05c4e35ff5b3.png)
