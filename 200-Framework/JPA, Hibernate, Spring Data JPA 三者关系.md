[@Yunxiong(heyunxiong)](/heyunxiong)： 2021年11月27日 整理

1. JPA是规范，要用JPA，需要搭配实现了该规范的ORM框架，比如Hibernate、Toplink等
2. Hibernate是实现了JPA规范的ORM框架，直接使用Hibernate，完全可以；功能上比JPA定义的更丰富
3. Spring Data JPA也是规范，为了配合Spring家族，所以它也需要一个实现了该规范的框架，只不过Spring Data JPA 就只选择了Hibernate。使用Spring Data JPA只需要定义好Repository接口，完全不需要编写sql即可最数据进行访问操作。

![yuque_diagram.jpg](_assets/JPA,%20Hibernate,%20Spring%20Data%20JPA%20三者关系/1637991203117-7a2c3370-fcf5-453b-b799-39ebaf3bc04a.png)
三者的HelloWorld
[JPA - HelloWorld](https://www.yuque.com/heyunxiong/knowledge/obsvt8?view=doc_embed)
[Hibernate - HelloWorld](https://www.yuque.com/go/doc/49926569?view=doc_embed)
[Spring Data JPA - HelloWorld](https://www.yuque.com/heyunxiong/knowledge/stgiax?view=doc_embed)
