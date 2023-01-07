# ORACLE 伪列伪表
http://www.jianshu.com/writer#/notebooks/12581088/notes/12668082/preview
oracle的伪列以及伪表

oracle系统为了实现完整的关系数据库功能，系统专门提供了一组成为伪列（Pseudocolumn）的数据库列，这些列不是在建立对象时由我们完成的，而是在我们建立时由Oracle完成的。Oracle目前有以下伪列：

一、伪列：

CURRVAL AND NEXTVAL 使用序列号的保留字

LEVEL 查询数据所对应的层级

ROWID 记录的唯一标识

ROWNUM 限制查询结果集的数量

二、伪表

DUAL 表

该表主要目的是为了保证在使用SELECT语句中的语句的完整性而提供的。

一般用于验证函数。例如：

select sysdate,to_char(sysdate,'yyyy-mm-dd HH24:mm:ss') from dual

Oracle伪列RowID

一、什么是伪列RowID？

1、首先是一种数据类型，唯一标识一条记录物理位置的一个id，基于64位编码的18个字符显示。

2、未存储在表中，可以从表中查询，但不支持插入，更新，删除它们的值。

二、RowID的用途

1,在开发中使用频率应该是挺多的，特别在一些update语句中使用更加频繁。所以oracle ERP中大部份的视图都会加入rowid这个字段。

在一些cursor定义时也少不了加入rowid。但往往我们在开发过程中，由于连接的表很多，再加上程序的复制，有时忽略了rowid对应的是那一个表中rowid，所以有时过程出错，

往往花上很多时间去查错，最后查出来既然是update时带的rowid并非此表的rowid,所以在发现很多次的错误时，重视rowid起来了，开发中一定要注意rowid的匹配

2，能以最快的方式访问表中的一行。

3，能显示表的行是如何存储的。

4，作为表中唯一标识。

三，RowID的组成

rowid确定了每条记录是在Oracle中的哪一个数据对象，数据文件、块、行上。

ROWID 的格式如下：

数据对象编号 文件编号 块编号 行编号

OOOOOO FFF BBBBBB RRR

由 data_object_id# + rfile# + block# + row# 组成，占用10个bytes的空间，

32bit的 data_object_id#,

10 bit 的 rfile#,

22bit 的 block#,

16 bit 的 row#.

所以每个表空间不能超过1023个 数据文件。

Oracle 登录
http://www.cnblogs.com/NaughtyBoy/p/3181052.html

[Oracle命令（一）：Oracle登录命令](http://www.cnblogs.com/NaughtyBoy/p/3181052.html)
1、运行SQLPLUS工具

　　C:\Users\wd-pc>sqlplus

2、直接进入SQLPLUS命令提示符

　　C:\Users\wd-pc>sqlplus /nolog

3、以OS身份连接 

　　C:\Users\wd-pc>sqlplus / as sysdba   或

　　SQL>connect / as sysdba

4、普通用户登录

　　C:\Users\wd-pc>sqlplus scott/123456 　或

　　SQL>connect scott/123456  或

　　SQL>connect scott/123456@servername

5、以管理员登录

　　C:\Users\wd-pc>sqlplus sys/123456 as sysdba　或

　　SQL>connect sys/123456 as sysdba

6、切换用户

　　SQL>conn hr/123456 

　　注：conn同connect

 7、退出

　　exit

---
# Oracle

### 查看数据库的SID步骤方法

用sysdba身份登录 比如 conn /as sysdba 匿名管理员登陆

查看SID

1.用sysdba身份登录 比如 conn /as sysdba

2.select instance_name from v$instance;

查看用户名

select * from dba_users; --查看数据库里面所有用户，前提是你是有dba权限的帐号，如sys,system

select * from all_users; --查看你能管理的所有用户！

select * from user_users; --查看当前用户信息 ！