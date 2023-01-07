不共享的情况各自线程计算各自的变量值
# 不共享情况
```java
package hyx.ch1_05;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/22/2020
 */
public class TestThread {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();

        t1.start();
        t2.start();
        t3.start();

    }
}

```
```java
package hyx.ch1_05;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/22/2020
 */
public class MyThread extends Thread {
    private int count = 5;

    @Override
    public void run() {
       while(count > 0){
           count--;
           System.out.println("线程名：" + this.currentThread().getName() + "  count = "+ count);
       }

    }
}

```
![image.png](_assets/Java线程%20共享变量的问题/1598064545970-5ebbda9e-620a-4037-a844-d4267861f3bf.png)
# 共享情况
```java
package hyx.ch1_05;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/22/2020
 */
public class TestThread {
    public static void main(String[] args) throws InterruptedException {
        MyThread myThread = new MyThread();

        MyThread t1 = new MyThread(myThread);
        MyThread t2 = new MyThread(myThread);
        MyThread t3 = new MyThread(myThread);
        MyThread t4 = new MyThread(myThread);
        MyThread t5 = new MyThread(myThread);

        t1.start();
        t2.start();
        t3.start();
        t4.start();
        t5.start();

    }
}

```
```java
package hyx.ch1_05;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/22/2020
 */
public class MyThread extends Thread {
    private int count = 5;

    @Override
    public void run() {
        super.run();
            count--;
            System.out.println("线程名：" + this.currentThread().getName() + "  count = " + count);

    }

    public MyThread(Runnable target) {
        super(target);
    }

    public MyThread() {
        super();
    }
}

```
![image.png](_assets/Java线程%20共享变量的问题/1598065934059-739ff6d8-f2b0-4c20-a84f-8735b7463890.png)
