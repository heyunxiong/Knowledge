> Java 基础知识： 多线程

## Thread 概述
说实话，线程能说的简直太多了，先简单的把基本使用弄明白，深入理解线程太费精力了；如果线程玩得好，代码质量能上一个台阶。
多线程是多任务的一种特别的形式，但多线程使用了更小的资源开销。（支线任务）
**线程与进程**

- 一个进程包括由操作系统分配的内存空间，包含一个或多个线程。
- 一个线程不能独立的存在，它必须是进程的一部分。
- 一个进程一直运行，直到所有的非守护线程都结束运行后才能结束。

**并发与并行**

- 并发：单核cpu运行多线程，cpu时间片不断进行切换，轮流执行线程
- 并行：多核cpu运行多线程，真正意义上的同一时刻运行

![](_assets/Java%20Thread%20线程/1636953824786-dca31afd-7344-4501-828d-a7c680d5221f.jpeg)
## Thread Lifecycle 线程生命周期
![](_assets/Java%20Thread%20线程/1636948675851-df77da78-89c3-4b57-be21-2b734040615d.jpeg)

- **New 新建状态**

创建Thread对象后，该线程对象处于新建状态

- **Runnable 就绪状态**

新建状态的对象调用start( )方法后，进入此状态，此时等待cpu的调度

- **Running 运行状态**

就绪状态的线程对象获取到了cpu的资源，执行run( )方法

- **Dead 结束状态**

线程完成后，或者其他条件发生导致线程终止，线程则进入终止状态

- **Blocked 阻塞状态**

进入Blocked状态的情况有好几种，但是需要明确的是，都是从Running状态切换到Blocked的。

   1. 等待阻塞

运行状态中的线程执行wait 方法

   2. 同步阻塞

线程获取synchronized同步锁失败，或同步锁被其他线程占用，进入同步阻塞状态

   3. 其他阻塞

通过调用线程的 sleep() 或 join() 发出了 I/O 请求时，线程就会进入到阻塞状态。当sleep() 状态超时，join() 等待线程终止或超时，或者 I/O 处理完毕，线程重新转入就绪状态
## Thread Priority 线程优先级
当操作系统有资源准备调度线程时，会根据线程的优先级决定调用顺序
优先级为整数 1 - 10； 1最低**（Thread.MIN_PRIORITY）**，10最高**（Thread.MAX_PRIORITY）**
**优先级高的先被调用**
## Thread 创建
### 实现Runnable接口
Runnable接口是一个函数式接口，啥事不干，就是为了run
```java
@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
```
```java
public class MyThread implements Runnable{

    @Override
    public void run() {
        try {
            Thread.sleep(3000);
            System.out.println("实现Runnable接口");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        System.out.println("==> Start Main ");
        new Thread(new MyThread()).start();
        System.out.println("==> End Main ");
    }
}
// 结果
==> Start Main 
==> End Main 
实现Runnable接口
```
### 继承Thread类
继承类必须重写 run() 方法，但是本质上也是实现了 Runnable 接口的一个实例，因为Thread也实现了Runnable接口
```java
public class Thread implements Runnable {...}
```
```java
public class MyThread2 extends Thread {
    @Override
    public void run() {
        try {
            Thread.sleep(3000);
            System.out.println("继承Thread方法，创建线程");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        System.out.println("==> Start Main ");
        new MyThread2().start();
        System.out.println("==> End Main ");
    }
}

// 结果
==> Start Main 
==> End Main 
继承Thread方法，创建线程

```
从结果可以看出，主线程不受新的子线程影响，继续执行；而新创建的线程会自行执行run方法内的程序（这里手动执行sleep 3秒的操作）
![](_assets/Java%20Thread%20线程/1636964631445-910ae9c3-b7a3-4af0-bcde-a304fa194582.jpeg)

### 实现Callable和使用FutureTask
最主要的是有返回值
1. 创建 Callable 接口的实现类，并实现 call() 方法，该 call() 方法将作为线程执行体，并且有返回值。
2. 创建 Callable 实现类的实例，使用 FutureTask 类来包装 Callable 对象，该 FutureTask 对象封装了该 Callable 对象的 call() 方法的返回值。
3. 使用 FutureTask 对象作为 Thread 对象的 target 创建并启动新线程。
4. 调用 FutureTask 对象的 get() 方法来获得子线程执行结束后的返回值。
```java
@FunctionalInterface
public interface Callable<V> {
    V call() throws Exception;
}
```
```java
public class FutureTask<V> implements RunnableFuture<V>{ ... }

//RunnableFuture继承自Future接口
public interface RunnableFuture<V> extends Runnable, Future<V>{
        void run();
}
```
```java
public interface Future<V> {
    boolean cancel(boolean mayInterruptIfRunning);
    boolean isCancelled();
    boolean isDone();
    V get() throws InterruptedException, ExecutionException;
    V get(long timeout, TimeUnit unit) throws InterruptedException
        						, ExecutionException, TimeoutException;
}
```
实例代码：[实例代码参考](https://segmentfault.com/a/1190000012291442)
```java
// 使用Callable、Future
public class MyThread3 {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newCachedThreadPool();
        Task task = new Task();
        Future<Integer> future = executorService.submit(task);
        executorService.shutdown();

        System.out.println("主线程在执行任务...");
        try {
            Thread.sleep(2000);
        } catch(InterruptedException ex) {
            ex.printStackTrace();
        }

        try {
            System.out.println("task运行结果:"+future.get());
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        } catch (ExecutionException ex) {
            ex.printStackTrace();
        }
        System.out.println("所有任务执行完毕");
    }
}
class Task implements Callable<Integer>{
    @Override
    public Integer call() throws Exception {
        System.out.println("子线程在执行任务...");
        //模拟任务耗时
        Thread.sleep(5000);
        return 1000;
    }
}
```
```java
// 使用Callable、FutureTask
public class Test {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newCachedThreadPool();
        Task task = new Task();
        FutureTask<Integer> futureTask = new FutureTask<Integer>(task);
        executorService.submit(futureTask);
        executorService.shutdown();

        System.out.println("主线程在执行任务...");
        try {
            Thread.sleep(2000);
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        }

        try {
            System.out.println("task运行结果:"+futureTask.get());
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        } catch (ExecutionException ex) {
            ex.printStackTrace();
        }

        System.out.println("所有任务执行完毕");
    }
}
class Task implements Callable<Integer>{
    @Override
    public Integer call() throws Exception {
        System.out.println("子线程在执行任务...");
        //模拟任务耗时
        Thread.sleep(5000);
        return 1000;
    }
}
```
## Thread 的run( )和start( )

- public void start( ) --**启动线程**

使该线程开始执行；Java 虚拟机调用该线程的 run 方法。

- public void run( )

如果该线程是使用独立的 Runnable 运行对象构造的，则调用该 Runnable 对象的 run 方法；否则，该方法不执行任何操作并返回。

