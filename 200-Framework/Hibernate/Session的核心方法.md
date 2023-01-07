## session的核心方法
session的对象状态
临时对象
持久化对象
![image.png](_assets/Session的核心方法/1628324698013-2b8b5ecd-256d-4259-bbd7-15b65c9ba87f.png)
![image.png](_assets/Session的核心方法/1628324708125-27ef4235-3da4-4e5d-9f06-89a63435818c.png)
对象的状态转换图
![image.png](_assets/Session的核心方法/1628325131273-da560d1d-b23a-465f-8c55-228ef2dc8ee2.png)


# save方法
![image.png](_assets/Session的核心方法/1628325482817-dd9bd712-2e2b-4fc7-8d1b-b9dd66c0b04a.png)
## persist方法
和save基本相同。也会执行insert操作
与save相比较下，在persist之前设置id会报错

# get方法，立即检索
获取对象
## load方法，延迟检索
与get也是类似的获取对象，
但是如果没有使用对象的话，不会去数据库拿数据，而get方法会立即去拿数据；
如果数据库表没有对应的记录，get返回null，load方法报错
在使用对象之前关闭session的话。get方法没有问题，因为执行get的时候已经去拿数据了。而load方法会懒加载异常
![image.png](_assets/Session的核心方法/1628325938447-5cfac0db-9d45-40c9-994d-1d850772f320.png)
![image.png](_assets/Session的核心方法/1628325920509-06a56f46-27cf-4996-950f-28a5112c03b7.png)

# update方法
![image.png](_assets/Session的核心方法/1628326731976-1079be7e-1037-4512-9a40-028b4482a8d5.png)

# saveOrUpdate方法
![image.png](_assets/Session的核心方法/1628329001144-b0635b99-38a3-467e-8ef8-242a31bae12e.png)
## meger方法
![image.png](_assets/Session的核心方法/1628329154473-d65135d1-d6a2-40ae-b90e-862d548a14d5.png)
## delete 方法
并不是马上删除。
配置 hibernate.use_identifier_rollback 为true，使删除对象后使OID为null
![image.png](_assets/Session的核心方法/1628329264949-37437f7f-24ba-4a59-87f7-d0d0e7af5df1.png)

## evict方法
从session缓存把指定的持久化对象移除

调用存储过程
sessiong.dowork（）

