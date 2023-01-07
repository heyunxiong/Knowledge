> 来源：[rhino - 博客园](http://www.cnblogs.com/happyPawpaw)，[转载文章链接](https://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247485099&idx=1&sn=a5c7bb2709c26e842aa70deb055cbdff&chksm=ebd63987dca1b0916a297ff096751f45c773999bade77d95b80cf3385f66f780b3aa38d55fdf&mpshare=1&scene=1&srcid=0327TqKWRbnMEmsp1KkcKS2W#rd)

- **PO：**persistant object （持久化对象），可以看成是与数据库中的表相映射的java对象。最简单的PO就是对应数据库中某个表中的一条记录，多个记录可以用PO的集合。PO中应该不包含任何对数据库的操作。
- **VO：**value object （值对象）。通常用于业务层之间的数据传递，和PO一样也是仅仅包含数据而已。但应是抽象出的业务对象，可以和表对应,也可以不,这根据业务的需要.个人觉得同DTO(数据传输对象)，在web上传递。
- **DAO：**data access object （数据访问对象），此对象用于访问数据库。通常和PO结合使用，DAO中包含了各种数据库的操作方法。通过它的方法结合PO对数据库进行相关的操作。
- **BO：**business object （业务对象），封装业务逻辑的java对象，通过调用DAO方法,结合PO、VO进行业务操作。
- **POJO：**plain old java object （简单无规则java对象），我个人觉得它和其他不是一个层面上的东西，VO和PO应该都属于它。

---

**加深理解**
**PO：**
persistant object  持久化对象
最形象的理解就是一个PO就是数据库中的一条记录。
好处是可以把一条记录作为一个对象处理，可以方便的转为其它对象。
**BO：**
business object  业务对象
主要作用是把业务逻辑封装为一个对象。这个对象可以包括一个或多个其它的对象。
比如一个简历，有教育经历、工作经历、  关系等等，我们可以把教育经历对应一个PO，工作经历对应一个PO，  关系对应一个PO。建立一个对应简历的BO对象处理简历，每个BO包含这些PO。这样处理业务逻辑时，我们就可以针对BO去处理。
**VO ：**
value object  值对象
ViewObject表现层对象主要对应界面显示的数据对象。对于一个WEB页面，或者SWT、SWING的一个界面，用一个VO对象对应整个界面的值。
**DTO ：**
Data Transfer Object  数据传输对象
主要用于远程调用等需要大量传输对象的地方。
比如我们一张表有100个字段，那么对应的PO就有100个属性。但是我们界面上只要显示10个字段，客户端用WEB service来获取数据，没有必要把整个PO对象传递到客户端，这时我们就可以用只有这10个属性的DTO来传递结果到客户端，这样也不会暴露服务端表结构。到达客户端以后，如果用这个对象来对应界面显示，那此时它的身份就转为VO
**POJO ：**
plain old java object  简单java对象
个人感觉POJO是最常见最多变的对象，是一个中间对象，也是我们最常打交道的对象。一个POJO持久化以后就是PO、直接用它传递、传递过程中就是DTO、直接用来对应表示层就是VO。
**DAO：**
data access object  数据访问对象
这个大家最熟悉，和上面几个O区别最大，基本没有互相转化的可能性和必要.
主要用来封装对数据库的访问。通过它可以把POJO持久化为PO，用PO组装出来VO、DTO
