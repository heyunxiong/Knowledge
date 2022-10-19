java web 之 WebRoot和WebContent目录
http://www.cnblogs.com/jokerjason/p/5727901.html

WebRoot和WebContent都是程序的根文件夹，无本质区别，一下是两者的共同点和不同点：

    共同点：都有一个WEB-INF文件夹，其下文件不可直接访问；

     WEB-INF是安全目录，所谓安全，就是用户客户端无法访问，只有服务器端可以访问。如果想在页面中直接访问，需要通过web.xml对要访问的文件进行映射。

      WEB-INF下除了web.xml，还有一个classes文件夹，放置*.class文件，类库，

      其下还有lib目录；

     不同点：

          WebRoot是MyEclipse中的web project结构，可添加一些开源框架的支持（struts,hibernate等），也就是说，web project是MyEclipse拓展过后的项目；

                              web project具有dynamic web project的特性，并具有一些方便开发的集成功能；

         WebContent是Eclipse下 dynamic web project结构；
         
![](_assets/java%20web%20之%20WebRoot和WebContent目录/image-java%20web%20之%20WebRoot和WebContent目录-20221019-125139695.png)

