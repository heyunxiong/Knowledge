# AWS 云从业者知识

> 云从业者是AWS认证体系中入门级别的定位，即新手

> 视频教程：https://study.163.com/course/courseLearn.htm?courseId=1212155814#/learn/video?lessonId=1283455232&courseId=1212155814

## AWS服务产品

**Basic功能**

compute 计算

storage 存储

network security 网络安全

复杂功能

blockchain 区块链

Machine Learning  机器学习

Artificial Intelligent 人工智能

Robot Development 机器人开发

Video 视频制作

轨道卫星

## AWS 服务器 EC2

Amazon Elastic Compute Cloud （Amazon EC2）

![image-20211127192821875](_assets/AWS%20云从业者知识/image-20211127192821875.png)

换了个马甲，理解成我们普通的服务器即可。

一个EC2实例，对应一台虚拟机

## 按实际使用量付费

不用提前付费，不用担心容量限制

## 什么是云计算

一种通过互联网按需提供IT资源的形式，采用按实际使用量付费的定价方式

按需提供

需要加空间的时候，自己上去点。就像添加菜单一样。

通过网络控制资源

通过按需付费

# AWS的常见产品说明

## EC2

ec2实例对应着一台虚拟机，即系一台物理主机会有多个ec2实例——多租户，在虚拟机之间共享底层硬件



aws构建了数据中心

aws保护了数据中

aws已经购买，安装了服务器

服务器处于联机状态，随时可使用

# Amazon Elastic Load Balance

负载均衡

## Amazon Simple Queue Service

消息队列 Amazon SQS

## Amazon Simple Notification Service

消息通知，订阅主题形式

# 其他服务形式

## Amazon  Lambda

暂时租用aws的服务器，不用管理ec2。

上传一段代码，设置好触发时间，触发事件启动，然后开始执行代码。

针对的是代码层面。

## Amazon Fargate

针对的是基于容器的无服务器serverless

无论是ecs还是eks都可以运行在ec2或者fargate中。fargate就不需要你操心底层操作系统的配置

## Amazon CloudFront

cloundfront，即系cdn，内容分发的作用

## Amazon Outposts 

在自己的数据中心里面使用Amazon云的服务。即系不想把敏感数据放到aws的服务器上的话。

## 与Aws的交互方式

aws console界面

aws cli 命令界面

### aws elastic beanstal 管理工具

- 调整容量

- 负载均衡

- 自动扩展

- 应用程序监控状态

###  Amazon cloudformation 管理工具

- 预先设置配置。监控错误等

# 第五章 联网

## Amazon Virtual Private Cloud

Amazon VPC 虚拟私有云

逻辑隔离

公有ip和私有网络

## Amazon Direct Connet

私有连接通道

![image-20211130220634571](_assets/AWS%20云从业者知识/image-20211130220634571.png)

## Network ACL 网络访问控制列表

network access control list

## Security Group 安全组

![image-20211130221403023](_assets/AWS%20云从业者知识/image-20211130221403023.png)

## Amazon  全球联网 

## Amazon Route53

域名服务 dns

流量路由策略：

- 基于延迟
- 地理位置
- 邻近度
- 加权轮询

## Amazon CloudFront 内容分发

# 第六章 存储和数据库

## Amazon Elastic Block Store

弹性块存储

更新增量

实例存储卷 短暂性 时效性， 重启实例数据消失

- 临时性数据块级存储。实例终止，数据丢失

ebs独立于ec2，可以永久存储

## Amazon Simple Store Service -S3

存储和检索无限量的数据 

![image-20211201125851103](_assets/AWS%20云从业者知识/image-20211201125851103.png)

创建多个存储桶

## Amazon Elastic File Service

EFS 托管文件系统， 感觉上类似于网盘



## Amazon Relational Database Service

RDS 关系数据库服务 ，在你能在AWS 运行关系型数据库

支持 各种主流的数据库 ，mysql。oracle。等

![image-20211203220419493](_assets/AWS%20云从业者知识/image-20211203220419493.png)

## Amazon Aurora

Aurora 是亚马逊推出的一款商业级别的数据库（类似于DB2）

![image-20211203220534929](_assets/AWS%20云从业者知识/image-20211203220534929.png)

## Amazon Dynamo DB

亚马逊推出的一款数据库，无服务器数据库，serverless database

Dynamo DB是NO SQL db 

非关系型数据库

## Amazon Redshift

Redshift ： data warehouse  数据仓库

适用于历史分析： 过去一小时的销售情况等

## Amazon Database Migration Service

DMS： 将现有的数据库简单安全地迁移到亚马逊云上

同构迁移

mysql -> rds for mysql

oracle -> rds for oracle

异构迁移

1.AmazonSchema Conversion Tool 进行转换

2.DMS

## 其他的数据库支持

Amazon Document DB （with MongoDB compatibility）

​	适用于 目录和用户资料管理

Amazon Neptune 图形数据库 

​	适合社交网络和推荐引擎

Amazon Managed Blockchain

​	管理区块链网络，分布式分类账系统

Amazon Quantum Ledger Database - Amazon QLDB

​	完整的历史记录	记录无法删除

Amazon Elastic Cache 支持Redis Memcached

​	数据库加速缓存 

Amazon DynamoDB Accelerator （DAX）

​	 支持DynamoDb的数据库缓存加速

## 安全

![image-20211203232057274](_assets/AWS%20云从业者知识/image-20211203232057274.png)

## 安全性

双方都要负责安全 ， aws和客户

aws负责房子的坚固

客户负责关门保证安全

![image-20211204133902118](_assets/AWS%20云从业者知识/image-20211204133902118.png)

## 用户权限

aws root账户，拥有所有权限

一般要求创建账户账户

使用多重授权 multi-factor authentication - mfa 

### AWS Identity and Access Management 

AWS IAM

在iam 创建user。没有任何权限默认除非授权了

![image-20211204134717869](_assets/AWS%20云从业者知识/image-20211204134717869.png)



## AWS Organization

集中管理多个aws账户

控制访问权限管理。资源访问管理

![image-20211204140038136](_assets/AWS%20云从业者知识/image-20211204140038136.png)

## 合规性

不同地区对于不同的应用服务有不同的法律合规性

aws有各个地区的

### AWS Artifact

管理不同地区合规性的文档

Morgan Wills

![image-20211204140628907](_assets/AWS%20云从业者知识/image-20211204140628907.png)

https://aws.amazon.com/cn/compliance/customer-center/

## 拒绝访问服务 DDoS

ddos 分布式拒绝服务

简单来说就是不断的访问，导致服务器过载奔溃

UDP 泛滥

![image-20211204160506500](_assets/AWS%20云从业者知识/image-20211204160506500.png)

这种借刀杀人的感觉

设定好返回地址为要被攻击的服务器地址。耗尽对方

解决方案：

安全组



HTTP攻击

占用资源，让正常的用户的访问无法得到处理

![image-20211204160635163](_assets/AWS%20云从业者知识/image-20211204160635163.png)

解决方案：

Amazon Shield ：免受DDoS攻击

- Amazon Shield Standard 标准 免费防御DDoS

- Amazon Shield Advanced： 付费高级版本，实时监控恶意流量。还能集成其他AWS的组件服务，如 cloudfront。route53 elb，

Amazon Shield 和Amazon WAF能防御复杂的DDoS攻击。          Amazon Web Application Firewall： Amazon WAF web应用防火墙

slowrios攻击

某个请求故意让请求处理变得很久，让后面等待的请求得不到处理

![image-20211204160742425](_assets/AWS%20云从业者知识/image-20211204160742425.png)

解决方案： ELB 负载均衡

## 其他安全

- 对资源加密

	- 静态加密
	- 传输加密

	AWS Key Management Service ： AWS KMS  进行密钥管理

	SSL 套接

	Amazon Inspector： 进行aws设施的安全评估

	Amazon GuardDuty ： 威胁监测服务 ，异常监测

	# AWS 监控

	

	## Amazon Cloud Watch

	实时监控aws资源和应用程序的情况

	创建条件阈值，发送监控通知

	![image-20211204223113021](_assets/AWS%20云从业者知识/image-20211204223113021.png)

	## Amazon Cloud Trail

	一种全面的API审核工具

	每个请求都会被记录在CouldTrail引擎中  

	## Amazon Trusted Advisory

	顾问工具。评估您的资源

	五个指标

	- 成本优化
	- 性能
	- 安全性
	- 容错能力
	- 服务限制

![image-20211204223938060](_assets/AWS%20云从业者知识/image-20211204223938060.png)

# 定价 和 支持

AWS免费套餐

1.永久免费

AWS Lambda 一个月一百万次的调用，基本上永久免费

2.12个月免费

S3 12个免费实用

3.短期试用

AWS Lightsai 一个月试用

免费套餐：https://aws.amazon.com/cn/free/



账单控制面板

账单 管理 bill management

![image-20211204225941627](_assets/AWS%20云从业者知识/image-20211204225941627.png)



账单整理

使用AWS Orgnazion中的功能。管理公司中各个账号的账单，把各处的账单集中到一个地方



AWS 预算管理

AWS Budget 

针对不同的场景设定预算

![image-20211204230559279](_assets/AWS%20云从业者知识/image-20211204230559279.png)

## AWS Cost Explorer

 查看和分析AWS 的费用支出情况

![image-20211204232032748](_assets/AWS%20云从业者知识/image-20211204232032748.png)



## AWS  Support 计划

1. 基本支持（免费
2. 开发支持
3. 业务支持
4. 企业支持
5. ![image-20211204232725932](_assets/AWS%20云从业者知识/image-20211204232725932.png)
6. 

AWS免费支持

![image-20211204232322833](_assets/AWS%20云从业者知识/image-20211204232322833.png)



开发支持

- 发邮件

高级Support

![image-20211204232427043](_assets/AWS%20云从业者知识/image-20211204232427043.png)



企业支持计划

## Amazon Marketplace

一种数字目录，包含独立软件供应商提供的上千款软件产品。

有点类似于 应用商店/插件中心。

一键部署

# AWS 迁移 和 创新

## AWS Cloud Adoption Framework  - CAF

云迁移六项关键因素

提供建议 快速。顺利迁移到云上

不同迁移的视角

1. 业务
	1. 财务分析师
2. 人员
	1. HR
3. 监管
	1. 云架构师
4. 平台
5. 安全性
6. 操作技术运维

## 6R 迁移策略

1.re-host 重新托管

直接迁移

2.re-platform 更换平台

修补后迁移

3retire 停用

不再使用的应用不用搬上去云

4retain 保留

暂时不搬上去

5re-phurse 重新购买

6.refactory 重构

# Snow系列

snow系列是一组物理设备

下面几个类别的区别是主要是容量不同

## Amazon Snowcone

坚固安全的小型边缘计算和数据传输设备

2个cpu，4gb内存和8tb存储容量

## Amazon Snowball

- Snowball Edge Storage Optimized

适合大型数据迁移和重复传输，高容量

80tb HDD 存储，用于数据块卷和s3对象存储

1tb 固态存储

40个cpu和80gb内存。 相当于一个独立的C5实例

- Snowball Edge Compute Optimized

适合机器学习，视频分析，分心数据等

42tb hdd ，兼容数据快卷和s3

7.65tb的ssd

52个vCPU。208GB内存 ，运行着Amazon EC2 sbe-c and sbe-g实例 。 相当于独立的C5，M5a，G3和P3实例

## Amazon Snowmobile

一次100PB容量

适合海量数据移动

45英尺场的集装箱。要用牵引车来拉。哇靠~





# 创新领域

## AWS VMware Cloud 

VMware Cloud 虚拟机云?

## Amazon SageMaker

部署机器学习模型

## Amazon Augmented AI 

机器学习平台

## Amazon Lex

语音智能助手

## Amazon Textract

提取文档中的文本

## Amazon Comprehend 

发现文本中的模式

## Amazon Fraud Detector

识别潜在的欺诈性在线活动

## Amazon DeepRacer

机器强化学习

## Amazon ground station

卫星通信



# 云之旅



![image-20211205001735835](_assets/AWS%20云从业者知识/image-20211205001735835.png)

![image-20211205001754492](_assets/AWS%20云从业者知识/image-20211205001754492.png)



## Amazon Well Architected

![image-20211205002654110](_assets/AWS%20云从业者知识/image-20211205002654110.png)

这是一个评估您的架构好不好、完不完善的工具 

五个指标

1. 卓越运营
	1. 监控系统，实现商业价值。进而优化流程和程序
	2. ![image-20211205002321623](_assets/AWS%20云从业者知识/image-20211205002321623.png)

2. 安全性
	1. 数据完整性 和 安全性

3. 可靠性

	恢复规划。db的数据恢复

4. 性能效率
	1. 高效利用IT和计算资源

5. 成本优化
	1. 控制资金方向
		1. EC2使用率等





# AWS 优势

AWS 服务



术语



六大优势

1.将固定费用交易变为可变费用

![image-20211205003145916](_assets/AWS%20云从业者知识/image-20211205003145916.png)

![image-20211205003237206](_assets/AWS%20云从业者知识/image-20211205003237206.png)

2.实现规模经济效益

实现比单独运行数据中心更低的可变成本

3.无需猜测容量

4.提供速度和敏捷性

![image-20211205003546684](_assets/AWS%20云从业者知识/image-20211205003546684.png)

5.不在话费资金来运行和维护数据中心

6.数分钟内实现全球部署

使用AWS CloudFormation 自动完成部署







