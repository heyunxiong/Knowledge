# Redis 笔记
## NoSQL - Not Only SQL
No SQL 出现的原因
1.解决高并发，访问量大的问题
2.处理数据的效率

No SQL的相关数据库
1.基于内存 Redis，Memcached；区别于Redis，Memcached一般不会去弄持久化，专注于使用内存，效率高
2.基于文档 MongoDB
3.基于列 HBase

## 什么是Redis
Redis 是一个高性能的No SQL的数据库，遵行BSD规则，Redis是一个简单高效，分布式，基于内存的缓存工具数据库

**Redis的特点**
-   redis 单个key存入512M大小
-   redis 支持多种类型的数据结构，string、list、hash、set、zset
-   redis 是单线程的，具有原子性操作
-   redis 可以持久化，使用了RDB和AOF机制（这两个是什么机制？）
-   redis 支持集群 支持0-15共16个库
-   redis 可以做消息队列

## 主从模式下的问题

![](Database/_assets/Redis笔记/image-Redis笔记-20221016-162558850.png)

## redis与memcached区别

1.  redis 有多种数据类型，memcached只有字符串
2.  redis可做持久化，memcached一般不做持久化，只负责内存操作（也可以做）
3.  redis 单线程+多路IO复用， memcached 多线程+锁

## 多路IO复用：有多个端口监视

![](Database/_assets/Redis笔记/image-Redis笔记-20221016-162612072.png)

