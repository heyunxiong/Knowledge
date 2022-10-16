MySQL中和标准SQL的不同
官方文档：[https://dev.mysql.com/doc/refman/8.0/en/ansi-diff-update.html](https://dev.mysql.com/doc/refman/8.0/en/ansi-diff-update.html)

关于MySQL的Update
更新的时候如果后面的列用到前面需要被修改的数据，那么后面的列会用到最新被更新的数据。
![](Database/_assets/MySQL和标准SQL的Update区别/image-MySQL和标准SQL的Update区别-20221016-162742247.png)

如下面的所示，更新前id=1，id2=3， 更新语句中，id=id+1， 此时id已经是2了， 后面的 id2=id，这个时候引用的是id更新后的数据2， 而不是原本在数据库中id=1。
![](Database/_assets/MySQL和标准SQL的Update区别/image-MySQL和标准SQL的Update区别-20221016-162748811.png)

![](Database/_assets/MySQL和标准SQL的Update区别/image-MySQL和标准SQL的Update区别-20221016-162751935.png)

