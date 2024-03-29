> 摘自「阿里巴巴 Java技术编程规范」

## 一、编程规约
### 命名风格
#### 哈哈。main里面的都被charge了。
![](_assets/Java技术编程规约/1602509103156-bc207eca-8cfe-486a-b660-216fe881ec1d.png)



#### POJO布尔类型不要用is前缀
![](_assets/Java技术编程规约/1602509103170-dab2049f-0575-43bf-8181-0fae5dc7f42a.png)
#### 爸爸和儿子还是要区分一下，增强可读性
![](_assets/Java技术编程规约/1602509103181-67258a9a-32cf-40ae-8d66-e9ff48443b7a.png)
#### 名词在尾
![](_assets/Java技术编程规约/1602509103181-c0800a91-f163-4632-b22d-cd794ccc4b09.png)
#### 接口类中的方法和属性 不要添加修饰符
![](_assets/Java技术编程规约/1602509103218-49f78236-9014-44c7-ae22-66b7fa2cfee5.png)
#### Enum类要大写
![](_assets/Java技术编程规约/1602509103162-88065be2-4a92-4532-bb8f-7ca98fdc11bf.png)
## 二、异常日志
### 异常处理
#### 关于大段地try-catch，需要细分捕获地错误
![](_assets/Java技术编程规约/1602509103242-dffe780e-ce71-46da-aaea-904fc2f64db2.png)
#### 使用Throwable进行拦截
![](_assets/Java技术编程规约/1602509103192-01b82fff-dd22-4133-8bb0-be9dc5ef9211.png)
### 日志规约
#### 日志级别的开闭问题
![](_assets/Java技术编程规约/1602509103192-ebe69470-5e02-48b4-9ff7-b7380be7c6c1.png)
#### 使用占位符
![](_assets/Java技术编程规约/1602509103201-7bf8b05a-a836-4387-9f55-759f2522aeec.png)
## 三、单元测试
### 画圈的是什么意思？概念不同，理解不了。
![](_assets/Java技术编程规约/1602509103198-55fb22ff-401e-468b-9d25-201bae68e326.png)
### 如何理解语句覆盖率？
![](_assets/Java技术编程规约/1602509103230-5e1c2737-79f1-415a-a9f0-923fd710999e.png)
### 哈哈哈，说的就是自己，开始的时候做法
![](_assets/Java技术编程规约/1602509103247-1dd816b5-d639-43b0-b6ec-c2311facc3ca.png)
### 如何理解？需要学习策略模式，状态模式
![](_assets/Java技术编程规约/1602509103270-f1285c04-344e-4331-b83e-77de55056e74.png)
## 四、安全规约
### 什么是反序列化注入？什么是ReDos？![](_assets/Java技术编程规约/1602509103232-6a39b760-4372-460a-9889-9a1c79cadd09.png)
### 什么是CSRF？具体的原理是什么？
![](_assets/Java技术编程规约/1602509103366-db037e52-2dbb-4a14-8949-9e78435667eb.png)
## 五、MySQL数据库
### 建表规约
#### 表名，字段名都只能使用小写，虽然说在Windows上，MySQL大小写不敏感，但是对于Linux来说是敏感的![](_assets/Java技术编程规约/1602509103275-2fc37582-8b7e-4882-847f-0990656ab362.png)
#### 小数的存放类型![](_assets/Java技术编程规约/1602509103237-89571ef4-5a3c-4239-b7ab-f971e4c3aaca.png)
什么时候需要分库分表？![](_assets/Java技术编程规约/1602509103263-fe5f388a-a6ae-48bc-afc9-9c6b46d42df2.png)
#### 字符存储长度
![](_assets/Java技术编程规约/1602509103274-c5716769-a937-4b4f-b8d2-9f76e97a70bb.png)
### 索引规约
#### 这就很强了，是不是说超过三个表的就是慎重考虑join？还是说针对索引而言？
![](_assets/Java技术编程规约/1602509103299-a7066d95-0a61-4802-84f5-4d07397b5602.png)
#### 索引的长度也是有要求的
![](_assets/Java技术编程规约/1602509103285-ac183e4e-42cc-470f-b0fa-0fd85d45db77.png)
#### 不太理解，需要去看下相关的索引的概念和要求
![](_assets/Java技术编程规约/1602509103304-a965e0db-3b9c-4c5e-bd8e-d7d0696ccbae.png)
#### 什么是回表？
![](_assets/Java技术编程规约/1602509103278-c6559b47-e2cc-4c77-8c40-187f3c4bc71f.png)
#### 延迟关联是什么？
![](_assets/Java技术编程规约/1602509103322-7655bfc8-8d4f-4329-b725-afe9a531dfd3.png)
#### 什么是组合索引？
![](_assets/Java技术编程规约/1602509103324-e78a310c-3e9d-41f6-a8b2-1143b9ed8dcc.png)
### SQL语句
#### 开头就暴击，以后不适用select count(1)了，使用 select count(*) 更香！
![](_assets/Java技术编程规约/1602509103304-d230fc0e-1ec4-4864-8f5b-dc31dedfea5b.png)
#### NULL 大佬的就是 有排面
![](_assets/Java技术编程规约/1602509103315-affc5bcc-de8b-4d47-b94b-4f7b0e22cfec.png)
#### 啊？ 存储过程这么没有地位吗？
![](_assets/Java技术编程规约/1602509103375-5cffeeba-9f14-4ae2-9b2a-f7cb49eff16f.png)
#### 为什么要避免 in？ 
![](_assets/Java技术编程规约/1602509103343-f5893d74-ded7-40ad-9e82-f9ebe09ee314.png)
#### 关于Truncate和Delete
![](_assets/Java技术编程规约/1602509103356-27420d51-571a-4e7f-8cb6-8a42df443b99.png)
### ORM映射
#### 什么是resultClass? MyBatis里面的吗？
![](_assets/Java技术编程规约/1602509103353-8a3d72d1-184f-4012-8c7b-cdf4714f8722.png)
#### 关于<isEqual>
![](_assets/Java技术编程规约/1602509107158-01ae83d8-b423-4e3c-8f33-3a2c228a4646.png)
## 八、工程结构
### 各种Object的模型规范
![](_assets/Java技术编程规约/1602509103342-ded11fc1-869a-4dcf-9d37-c41d32ec52da.png)
