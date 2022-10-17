由数组支持的有序集合可以快速地随机访问，因此适合使用 List 方法并提供一个

整数索引来访问。与之不同， 链表尽管也是有序的， 但是随机访问很慢，所以最好使用迭代

器来遍历

  为了避免对链表完成随机访问操作，Java SE 1.4 引入了一个标记接口 RandomAccess。

这个接口不包含任何方法， 不过可以用它来测试一个特定的集合是否支持高效的随机访问：

if (c instanceof RandomAccess)

{

use random access algorithm

else

{

use sequential access algorithm

}