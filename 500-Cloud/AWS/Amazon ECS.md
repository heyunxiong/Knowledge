## Amazon ECS

视频地址：https://study.163.com/course/courseMain.htm?courseId=1212144829



什么是ecs

容器管理

![image-20211213142140695](_assets/Amazon%20ECS/image-20211213142140695.png)



容器是一个软件交付单元，自行包含着：打包且可与其他全部依赖项一起执行的软件

容器很不错，但是在管理多个容器和集群的时候，管理容器成为了一项艰难的挑战

管理容器则可以使用ecs了

![image-20211213143029977](_assets/Amazon%20ECS/image-20211213143029977.png)

![image-20211213143920350](_assets/Amazon%20ECS/image-20211213143920350.png)



集成各种aws的其他服务







ecs三个主要组件，

![image-20211213144207326](_assets/Amazon%20ECS/image-20211213144207326.png)

集群：

可用区内的容器

![image-20211213144242586](_assets/Amazon%20ECS/image-20211213144242586.png)





ecs集群是一组分布于多个   运行Amazon ecs容器代理的   可用区的Amazon ec2实例。



管理资源，协调声明周期，并有效制定计划



任务：

![image-20211213145717439](_assets/Amazon%20ECS/image-20211213145717439.png)

![image-20211213144743914](_assets/Amazon%20ECS/image-20211213144743914.png)





demo环节：

![image-20211213145835255](_assets/Amazon%20ECS/image-20211213145835255.png)



创建集群

![image-20211213145902845](_assets/Amazon%20ECS/image-20211213145902845.png)





创建task

![image-20211213152336265](_assets/Amazon%20ECS/image-20211213152336265.png)



把任务添加到集群中



![image-20211213152803978](_assets/Amazon%20ECS/image-20211213152803978.png)



创建服务：

添加任务到service



![image-20211213152906762](_assets/Amazon%20ECS/image-20211213152906762.png)

![image-20211213153105696](_assets/Amazon%20ECS/image-20211213153105696.png)



![image-20211213153118162](_assets/Amazon%20ECS/image-20211213153118162.png)

创建服务，部署应用



问题来了：service 和 task的区别。



ecs非常适合微服务

![image-20211213153522861](_assets/Amazon%20ECS/image-20211213153522861.png)



适合批处理

![image-20211213153717192](_assets/Amazon%20ECS/image-20211213153717192.png)



适合cicd，pipeline

![image-20211213153728640](_assets/Amazon%20ECS/image-20211213153728640.png)



ecs总结

![image-20211213153752666](_assets/Amazon%20ECS/image-20211213153752666.png)

