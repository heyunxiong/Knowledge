# **struts2**

2016年4月13日 20:49:59

1. 环境struts2的开发环境
2. 不需要现实的定义filter，而是使用struts2的配置文件

class的默认值是com.opensymphony.xwork2.ActionSupport

method的默认值是：execute

result的默认值是：success

type:表示结果的类型，默认植是：dispatcher

一个请求一个Action，所以不存在线程安全问题

action的class默认是“com.opensymphony.xwork2.ActionSupport”

<default-class-ref class="com.opensymphony.xwork2.ActionSupport" />

写Action的时候，记得要继承ActionSupport,将会给开发带来方便，避免的了要手工显示错误消息，国际化的繁琐步骤，不然就要自己手动去实现相应的借口

> rerult 详解
>
> result是action的子节点，代表Action方法执行后可能去的目的地，
>
> 一个action可以有多个result子节点
>
> result的name属性对应着Action方法的一个返回值
>
> type表示响应结果的类型（在struts-default.xml找到全部值） 常用的有四个值：dispatcher（默认）,redirect.redirectAction,chain,另外stream这个值常用用于文件下载

> dispatcher （默认）转发，同servlet中的转发
>
> redirect 重定向
>
> redirectAction 重定向到一个Action
>
> chain 转发到一个Action
>
> 不能通过type=dispatcher方式转发到一个Action.

---result也就只用2个属性（name,type）

redirect 可以便捷的实现redirectAction！

动态方法调用

ONGL

在JSP页面上可以利用OGNL（object-graph-navigation-language:对象-图导航语言）访问到值栈（valuestack）里面的对象属性---如何在页面上访问值栈的属性

关于值栈

1. helloworld时，${productName}读取productName值时，实际上该属性并不在request等域，而是从值栈中获取的

- 可以从ActionContext中获取值栈对象
- 值栈氛围两个逻辑部分
- - Map栈：实际上是OgnlContext类型，是个Map，也是对ActionContext的一个引用（里面只有一个OGNL属性），里面保存各种Map（requestMap，sessionMap，applicationMap，parameterMap，attr）
    - 对象栈：实际上是ConpoundRoot类型，是一个使用了Arraylist定义的栈，里面保存这当前Action实例相关的对象，是一个数据结构意义的栈

struts2 的s:property标签+OGNL的表达式用来输出值栈中的一个属性值

<s:property value="[0].message"> //第一个对象的message属性，第二个对象可以这样表示“[1].message”

什么是值栈中的属性值？？

1、对于对象栈：对象栈中的某一个对象的属性值

2、Map栈：request，session，application，的一个属性值或者一个请求参数的值

默认情况下，Action对象会被struts2自动的放到值栈的栈顶。

struts2自动把Action对象放入到值栈中，

》放入的时间点为：strut2最终会调用Action类中的方法，但在调用该方法之前：

--》先创建了一个Strut2ActionProxy对象

--》在创建Strut2ActionProxy之后，对其进行初始化时，把Action对象放入了值栈中

struts标签

property标签：打印值栈里面的属性值；

-----》对于对象栈，打印值栈中对应的属性值

---->对于Map栈，打印request，session，application的某个属性值或者请求参数的值

showpassword="true"//设置表单密码回显

from标签：

1.使用form标签和html表单基本一样

2.strut2的form标签会自动生成一个table，以进行自动排版

3.可以对表单的提交进行回显。：从栈顶对象开始匹配属性，并把匹配的属性值赋到对应标签的value中，若栈顶对象没有对应的属性，则依次向下找到相应的属性。

2016年4月13日 20:49:59

1. 环境struts2的开发环境
2. 不需要现实的定义filter，而是使用struts2的配置文件

class的默认值是com.opensymphony.xwork2.ActionSupport

method的默认值是：execute

result的默认值是：success

type:表示结果的类型，默认植是：dispatcher

一个请求一个Action，所以不存在线程安全问题

action的class默认是“com.opensymphony.xwork2.ActionSupport”

<default-class-ref class="com.opensymphony.xwork2.ActionSupport" />

写Action的时候，记得要继承ActionSupport,将会给开发带来方便，避免的了要手工显示错误消息，国际化的繁琐步骤，不然就要自己手动去实现相应的借口

> rerult 详解
>
> result是action的子节点，代表Action方法执行后可能去的目的地，
>
> 一个action可以有多个result子节点
>
> result的name属性对应着Action方法的一个返回值
>
> type表示响应结果的类型（在struts-default.xml找到全部值） 常用的有四个值：dispatcher（默认）,redirect.redirectAction,chain,另外stream这个值常用用于文件下载

> dispatcher （默认）转发，同servlet中的转发
>
> redirect 重定向
>
> redirectAction 重定向到一个Action
>
> chain 转发到一个Action
>
> 不能通过type=dispatcher方式转发到一个Action.

---result也就只用2个属性（name,type）

redirect 可以便捷的实现redirectAction！

> > > 动态方法调用

ONGL

在JSP页面上可以利用OGNL（object-graph-navigation-language:对象-图导航语言）访问到值栈（valuestack）里面的对象属性---如何在页面上访问值栈的属性

关于值栈

1. helloworld时，${productName}读取productName值时，实际上该属性并不在request等域，而是从值栈中获取的

- 可以从ActionContext中获取值栈对象
- 值栈氛围两个逻辑部分
- - Map栈：实际上是OgnlContext类型，是个Map，也是对ActionContext的一个引用（里面只有一个OGNL属性），里面保存各种Map（requestMap，sessionMap，applicationMap，parameterMap，attr）
    - 对象栈：实际上是ConpoundRoot类型，是一个使用了Arraylist定义的栈，里面保存这当前Action实例相关的对象，是一个数据结构意义的栈

struts2 的s:property标签+OGNL的表达式用来输出值栈中的一个属性值

<s:property value="[0].message"> //第一个对象的message属性，第二个对象可以这样表示“[1].message”

什么是值栈中的属性值？？

1、对于对象栈：对象栈中的某一个对象的属性值

2、Map栈：request，session，application，的一个属性值或者一个请求参数的值

默认情况下，Action对象会被struts2自动的放到值栈的栈顶。

struts2自动把Action对象放入到值栈中，

》放入的时间点为：strut2最终会调用Action类中的方法，但在调用该方法之前：

--》先创建了一个Strut2ActionProxy对象

--》在创建Strut2ActionProxy之后，对其进行初始化时，把Action对象放入了值栈中

struts标签

property标签：打印值栈里面的属性值；

-----》对于对象栈，打印值栈中对应的属性值

---->对于Map栈，打印request，session，application的某个属性值或者请求参数的值

showpassword="true"//设置表单密码回显

from标签：

1.使用form标签和html表单基本一样

2.strut2的form标签会自动生成一个table，以进行自动排版

3.可以对表单的提交进行回显。：从栈顶对象开始匹配属性，并把匹配的属性值赋到对应标签的value中，若栈顶对象没有对应的属性，则依次向下找到相应的属性。



请求在到达目标Action之前，struts2会经过一系列的拦截器，其中有一个拦截器叫：Params拦截器---Parameters拦截器会把表单字段映射到valuestack栈的栈顶对象的各个属性中，如果没有在栈顶匹配到，将会在值栈中寻找下一个对象