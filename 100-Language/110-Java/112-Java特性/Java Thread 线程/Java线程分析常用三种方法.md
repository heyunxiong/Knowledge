# 示例代码块
```java
package hyx.ch1_02;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 8/21/2020
 */
public class TestThread02 {
    public static void main(String[] args) {
        for (int i = 0; i < 3; i++) {
            new Thread(){
                @Override
                public void run() {
                    try {
                        System.out.println(Thread.currentThread().getName() + "  正在运行！");
                        Thread.sleep(500000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }.start();
        }
    }
}
```
# 运行结果
![image.png](_assets/Java线程分析常用三种方法/1598016707473-03a6cbc3-8281-48be-8036-bd7583fcb22d-2803249.png)
# 方法一： jps + jstack
![image.png](_assets/Java线程分析常用三种方法/1598016619399-9401cc33-a273-4bef-92f7-299f1fc73192.png)
![image.png](_assets/Java线程分析常用三种方法/1598016589814-d2909f3e-efb6-46f9-bdcb-d660b7184d2e.png)

# 方法二：jmc.exe
在bin目录下找到该可执行文件 D:\Java1.8\bin\jmc.exe
![image.png](_assets/Java线程分析常用三种方法/1598016422033-fc9c199a-8262-436c-9957-c3900c619e59.png)

# 方法三：jvisualvm.exe
同理在bin目录下找到该程序即可。D:\Java1.8\bin\jvisualvm.exe，该可视化工具还能看到jvm内存结构的情况
![image.png](_assets/Java线程分析常用三种方法/1598016542820-714206a6-2f03-4c1f-9c92-0aba485a18d8.png)
