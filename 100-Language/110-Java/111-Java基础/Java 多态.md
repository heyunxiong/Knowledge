Java 多态
灵魂的拷问：
Parent p = new  Son();

> 解释下为什么要用 接口变量做子类对象的引用？


[https://blog.csdn.net/summerxiachen/article/details/79733800](https://blog.csdn.net/summerxiachen/article/details/79733800)

···
先把结论丢出来吧

应该优先使用接口而不是类来引用对象，但只有存在适当的接口类型时
也就是说，使用接口类去引用对象是有前提条件的——即实现类中全是接口类的方法的实现，没有自己单独的方法。当实现类存在自己的方法时，使用实现类来声明变量。

···