> AWS：Amazon Web Service
> 基础知识，常用服务及其相关概念

## 什么是云计算
个人理解是：对IT资源的整合，简化和节省前期业务的开展，能借用云计算的优势快速搭建环境；
具体表现在：不需要购买硬件设施，无需安排人员搭建环境；使用云计算能做到按需付费。
[云计算知识](https://www.yuque.com/heyunxiong/knowledge/bm7ndh?view=doc_embed)
## AWS 概述

- 市场占有率高，不同领域的技术解决方案成熟
- 按实际使用量付费
- 不用提前付费，不用担心容量限制
- 服务器处于联机状态，随时可使用
## AWS 服务架构
架构参考 >>>  [https://aws.amazon.com/cn/architecture/compute-hpc](https://aws.amazon.com/cn/architecture/compute-hpc)

- **案例1**

![https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/automatically-build-ci-cd-pipelines-and-amazon-ecs-clusters-for-microservices-using-aws-cdk.html?did=pg_card&trk=pg_card](_assets/AWS%20基础服务/1638779243076-27f8185e-1039-4b80-a3bd-70999c780ccb.png)

- **案例2**

![https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/deploy-java-microservices-on-amazon-ecs-using-amazon-ecr-and-aws-fargate.html?did=pg_card&trk=pg_card](_assets/AWS%20基础服务/1638779369587-fee17004-4fbf-447b-bb5c-986e9ec36022.png)
## AWS 产品服务
### EC2 - Amazon Elastic Compute Cloud
Amazon Elastic Compute Cloud（Amazon EC2 云服务器）是一种 Web 云服务，能在云中提供安全且可调整大小的计算能力。（简单理解成是aws提供的一台带有操作系统的虚拟机服务器）
支持自动扩容
![Amazon-EC2.png](_assets/AWS%20基础服务/1638684082037-a490b585-357c-463e-a45d-00ce6f86b1f8.png)

### ELB - Amazon Elastic Load Balancing
Elastic Load Balancing (ELB)  负责负载均衡，在多个目标和一个或多个可用区 (AZ) 中的虚拟设备之间，自动分配传入的应用程序流量
![Elastic-Load-Balancing-ELB.png](_assets/AWS%20基础服务/1638684311709-e2c4f407-8c7d-4845-b784-c305670a3bc1.png)
ELB可以应用在不同的场景中，应用内做负载均衡、网关、网络
有三种负载均衡情况
**应用负载均衡 application load balancer**
![image.png](_assets/AWS%20基础服务/1638685002570-61ab024e-464c-468a-b21c-8d562aa1772f.png)
**网关负载均衡 gateway load balancer**
![image.png](_assets/AWS%20基础服务/1638685033193-64ccecf6-4dee-4ba6-907d-8a843f3352b3.png)
**网络负载均衡 network load balancer**
![image.png](_assets/AWS%20基础服务/1638685046149-320addaf-bd4c-4b15-bddf-1aa5dd79c88d.png)

### SQS - Amazon Simple Queue Service
Amazon Simple Queue Service (SQS) 是一种完全托管的**消息队列服务**，可让您分离和扩展微服务、分布式系统和无服务器应用程序。
![SQS](_assets/AWS%20基础服务/1638685418848-f6e36dc7-035e-4b55-875a-5556ea7c7583-20230104131850713.png)

### SNS - Amazon Simple Notification Service
消息通知，订阅主题形式，通过订阅获取相关主题的通知信息。
![SNS](https://cdn.nlark.com/yuque/0/2021/svg/1587784/1638690362768-2c6845d4-0e3b-4616-87e7-9028db4019de.svg#clientId=ub74f670f-40ea-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u494d26be&originHeight=150&originWidth=150&originalType=url&ratio=1&rotation=0&showTitle=true&status=done&style=stroke&taskId=u356f2030-efc1-40bc-a94a-53e04532049&title=SNS "SNS")
Amazon Simple Notification Service (Amazon SNS) 是一项用于应用与应用之间 (A2A) 以及应用与人之间 (A2P) 通信的完全托管型消息收发服务
通过短信/邮件/应用程序发送通知
## 其他服务
### AWS Lambda
AWS Lambda 是一项无服务器事件驱动型计算服务，该服务使您可以运行几乎任何类型的应用程序或后端服务的代码，而无需预置或管理服务器
![AWS-Lambda.png](_assets/AWS%20基础服务/1638690444396-8ce3529b-72ba-4b0e-8da9-f1d835c2813d.png)
个人理解：暂时租用aws的服务器，不需要管理创建EC2，已经有相关的环境，上去跑代码即可。
上传一段代码，设置好触发时间，触发事件启动，然后开始执行代码，针对的是代码层面
比如：文件处理，图片处理。

### AWS Fargate
适用于容器的无服务器
AWS Fargate 是一种无服务器、随用随付的计算引擎，可让您专注于构建应用程序，而无需管理服务器。AWS Fargate 与 Amazon Elastic Container Service (ECS) 和 Amazon Elastic Kubernetes Service (EKS) 兼容
![AWS-Fargate.png](_assets/AWS%20基础服务/1638690501875-12216a9d-d700-481e-948d-b7863b6a7ad4.png)
个人理解：同样的有相关的环境，只不过是针对基于容器（相较于Lambda针对代码，Fargate针对容器)
对于容器本身，既可以运行在EC2和Fargate上，但是EC2需要自己去创建管理，而使用Fargate，因为已经有了相关的支持容器的环境，可以把基于容器的应用放在Fargate上运行。

### AWS CloudFront
CDN 内容分发的作用
Amazon CloudFront 是一种内容分发网络 (CDN) 服务
![Amazon-CloudFront.png](_assets/AWS%20基础服务/1638690596531-c1a2ff17-57e0-4556-8d28-69480327dffb.png)
内容分发：即系用户访问的服务端的时候，由于地理位置距离太远，响应延迟太大，则向距离该用户较近的数据中心中分发内容，保证响应速度。（比如位于广东的用户请求欧洲的服务器，该服务器能在HK有CDN的数据，实际上访问的是HK服务器的内容）
![image.png](_assets/AWS%20基础服务/1638686980510-4bc8179b-7874-491f-83a3-a657a8eb6349.png)

### AWS Outposts 
AWS Outposts 是一项完全托管的服务，可提供相同的 AWS 基础设施、AWS 服务、API 和工具到几乎任何数据中心、主机托管空间或本地设施，以实现真正一致的混合体验
![AWS-Outposts.png](_assets/AWS%20基础服务/1638690649125-212289ff-a01e-4c2e-b400-0eeade1bec2d.png)
运行本地 AWS 基础设施和服务，在自己的数据中心里面使用Amazon云的服务；即系不想把敏感数据放到aws的服务器上
[AWS Outposts](https://aws.amazon.com/cn/outposts/?nc2=type_a)

## AWS 基础设施的可靠性
AWS的区域
选择区域要考虑的指标

- 遵守当地的数据治理和法律要求
- 与目标客户的距离
- 区域的可用服务
- 定价

可用区：一个区域内的单个数据中心或者一组数据中心，可用区相隔数十英里
![image.png](_assets/AWS%20基础服务/1638688384037-8a1bcf90-b536-4c8d-8639-70243535258b.png)

## 与 AWS 交互
手动设置管理： 

- AWS管理控制台 -  浏览器进入，可视化
- 命令行界面CLI - 终端

![AWS-Command-Line-Interface.png](_assets/AWS%20基础服务/1638691046247-3015b3a8-2918-4e59-a4f2-7b8f9086bd0d.png)

- 软件工具包SDK - 使用编程语言和AWS的资源交互，调用API

预置资源操作：Amazon Elastic Beanstalk、Amazon CloudFormation工具
### AWS Elastic Beanstalk
AWS Elastic Beanstalk 是一项易于使用的服务，用于在熟悉的服务器（如 Apache 、Nginx和 IIS ）上部署和扩展使用 Java、.NET、PHP 和 Docker 开发的 Web 应用程序和服务
![AWS-Elastic-Beanstalk.png](_assets/AWS%20基础服务/1638690718640-5089aca5-6109-413c-8a5e-49af3d5ba9bd.png)
准备代码和配置设置信息后，Elastic Beanstalk 会负责部署执行

- 调整容量
- 负载均衡
- 自动扩展
- 应用程序运行状况监控
### AWS CloudFormation
AWS CloudFormation 允许您通过将基础设施视为代码来建模、预置和管理 AWS 和第三方资源
![AWS-CloudFormation.png](_assets/AWS%20基础服务/1638690747800-34bb15a6-a9fb-4dc3-a3a6-47ffad005038.png)
通过代码的形式进行基础设施的制定，比如代码配置中写好要什么类型的EC2，数据库要什么等等。
![image.png](_assets/AWS%20基础服务/1638687597450-0d2676ba-eefb-467f-bd12-50d2bcc36f33.png)

## AWS Networking 联网
### VPC - Amazon Virtual Private Cloud 
Amazon Virtual Private Cloud (VPC) 让您能够全面地控制自己的虚拟网络环境，包括资源放置、连接性和安全性
![Amazon-VPC.png](_assets/AWS%20基础服务/1638690951357-1010d50a-1a83-493d-8ab3-5329cb0f5b5d.png)
虚拟私有云， 逻辑隔离

每个区域内的两个 VPC 之间共享网络流量
![image.png](_assets/AWS%20基础服务/1638688903338-f00522a5-129f-4492-a92d-8d5ea729b16a.png)

### Amazon Direct Connet
AWS Direct Connect 是一种云服务，可将您的网络直接链接到 AWS，绕过互联网，以获得更一致、更低延迟的性能。 即系私有专用连接通道
![AWS-Direct-Connect.png](_assets/AWS%20基础服务/1638690973936-9d56f80a-5457-4547-bb7c-7aefeeecbdfe.png)
![image.png](_assets/AWS%20基础服务/1638689096843-7b96cb92-9246-41a1-b249-6a78c9ef621f.png)
**Network ACL - Access Control List**
网络访问控制列表
是一种虚拟防火墙，用于在子网级别控制入站和出站流量
默认下，允许所有入站和出站流量
检查数据包的目标访问地址在不在列表中，在则放行，否则拒绝；不会检查数据包的内容，也不会记住状态。

**Security Group 安全组**
是一种虚拟防火墙，用于控制EC2实例的入站和出站流量
默认下，拒绝所有入站访问，允许所有出站流量

**Security group 和 ACL 的对比较**
Security group 是有状态的，ACL 没有
![image.png](_assets/AWS%20基础服务/1638688815620-aa6cd8ce-a7dc-46f8-8c91-41479be94365.png)

### Amazon Route 53
Amazon Route 53 是一种可用性高、可扩展性强的云域名系统 (DNS) Web 服务
![Amazon-Route-53.png](_assets/AWS%20基础服务/1638691002161-1ab05021-11b4-495f-b709-3372deb97f18.png)
提供域名服务 DNS
流量路由功能策略

- 基于延迟
- 地理位置
- 邻近度
- 加权轮询
### Amazon CloudFront - CDN
内容分发
## AWS 存储和数据库
### EBS - Amazon Elastic Block Store
Amazon Elastic Block Store (Amazon EBS) 是一种易于使用且可扩展的高性能数据块存储服务，适合用于 Amazon Elastic Compute Cloud (Amazon EC2)
![Arch_Amazon-Elastic-Block-Store_64@5x.png](_assets/AWS%20基础服务/1638759163252-daa58456-f200-4621-be39-237a9fcc6e6a.png)
挂载到EC2后，可在这些卷上创建文件系统、运行数据库，或以任何其他块储存设备使用方式使用这些卷。
即系相当于一个盘
EBS是增量存储的，独立于EC2，所以能挂载，数据永久存储。
相对的，实例存储卷：暂时的，时效的，实例终止，数据丢失。
![image.png](_assets/AWS%20基础服务/1638761288095-fbc8f5d2-1de6-4b55-9c02-26e86c969dac.png)
[EBS介绍](https://aws.amazon.com/cn/ebs/features/)

### S3 - Amazon Simple Store Service -S3
Amazon Simple Storage Service (Amazon S3) 是一种对象存储服务，提供行业领先的可扩展性、数据可用性、安全性和性能。
![Arch_Amazon-Simple-Storage-Service_64@5x.png](_assets/AWS%20基础服务/1638759233407-ead0a0ef-a0d3-4fff-865b-ab01f83f8a92.png)
注重检索，能高效快速查询对象 ：任意位置检索任意数量的数据
S3存储全量数据，将数据存储为对象，最大可上传对象为5TB，有版本控制，能创建多个存储桶
分类：

- S3标准

适合频繁访问的数据，数据存在至少三个可用区中

- S3标准 - 不频繁访问（S3标准 - IA）

适合不频繁访问的数据存储，同样在至少三个可用区中

- S3单区 - 不频繁访问（S3单区 - IA）

S3标准 - IA 的青春版，节省存储费用

- S3智能分区

适合存储访问模式未知的（既不知道频繁与否）或者不断变化的数据
30天为一个时间节点。30天内未访问自动移动到 S3标准-不频繁；如果访问了超过30天数据，会从不频繁自动到S3标准区域

- S3 Glacier

低成本存储，适合数据存档，即系Archive的资料，几分钟内能检索到数据文件

- S3 Deep Glacier Archive

和Glacier在于检索速度差异，这种需要12个小时内才能完成对象检索，速度较慢，但是存储价格低

**EBS和S3的使用选取**

- 偶尔修改，存储完整对象 ，选S3
- 经常进行复杂修改，读写操作，选EBS
### EFS - Amazon Elastic File System
Amazon Elastic File System (Amazon EFS) 可随着您添加和删除文件自动增大或收缩，无需管理或预置
![Arch_Amazon-Elastic-File-System_64@5x.png](_assets/AWS%20基础服务/1638759290897-6d1d2f5b-1177-49b5-9d88-71f07a1f776e.png)
简单的设置即用式无服务器弹性文件系统
有简易操作系统的网盘。
**EBS 和 EFS**
![image.png](_assets/AWS%20基础服务/1638761932010-89ca0f3f-92f4-44d8-94b6-f48d4fc80a22.png)

### RDS - Amazon Relational Database Service
Amazon Relational Database Service (Amazon RDS) 让您能够在云中轻松设置、操作和扩展关系数据库
![Arch_Amazon-RDS_64@5x.png](_assets/AWS%20基础服务/1638759411515-017e0ebc-48ed-43eb-9a4c-ea906fc37c0c.png)
RDS 关系数据库服务 ，在你能在AWS 运行关系型数据库
支持各种主流的数据库，包括 Amazon Aurora、PostgreSQL、MySQL、MariaDB、Oracle Database 和 SQL Server
RDS 具备 自动修补、备份、冗余存储、故障转移、灾难数据恢复 等功能

### Amazon Aurora
Amazon Aurora 是一种与 MySQL 和 PostgreSQL 兼容的关系数据库，专为云而打造，
既具有传统企业数据库的性能和可用性，又具有开源数据库的简单性和成本效益
![Arch_Amazon-Aurora_64@5x.png](_assets/AWS%20基础服务/1638759440974-643ac0d4-6577-4765-8843-ce59a87e181c.png)
Aurora 是亚马逊推出的一款商业级别的数据库（类似于DB2，收钱的)

### Amazon Dynamo DB
Amazon DynamoDB 是一种完全托管式、无服务器的 **NoSQL 键值数据库**
![Arch_Amazon-DynamoDB_64@5x.png](_assets/AWS%20基础服务/1638759486556-0f36bd58-fcc3-4df1-9e68-5437327302fb.png)
亚马逊推出的一款数据库，无服务器数据库，serverless database
Dynamo DB是NO SQL db，非关系型数据库
无服务器的特性说明，可以直接使用。

### Amazon Redshift
Redshift是Amazon推出的数据仓库 data warehouse，能分析多个数据源数据。
![Arch_Amazon-Redshift_64@5x.png](_assets/AWS%20基础服务/1638760785437-d08928ff-e669-4330-85ec-920faedabdd4.png)
Amazon Redshift 使用 SQL 在数据仓库、运营数据库和数据湖间分析结构化和半结构化数据
适用于历史分析： 过去一小时的销售情况等

### DMS - Amazon Database Migration Service
AWS Database Migration Service (AWS DMS) 可帮助您快速并安全地将数据库迁移至 AWS。源数据库在迁移过程中可继续正常运行，从而最大程度地减少依赖该数据库的应用程序的停机时间。AWS Database Migration Service 可以在广泛使用的开源商业数据库之间迁移您的数据。
![Arch_AWS-Database-Migration-Service_64@5x.png](_assets/AWS%20基础服务/1638760852741-b9fb77a9-9512-4668-914e-d31709ceb213.png)
DMS： 将现有的数据库简单安全地迁移到亚马逊云上
同构迁移，相同结构的数据库直接可以直接迁移
mysql -> rds for mysql ， 直接迁移
oracle -> rds for oracle 
异构迁移，不同数据库之间，需要先进行结构转换操作
1.AmazonSchema Conversion Tool 进行转换
2.DMS 	

### 其他的数据服务支持
Amazon Document DB （with MongoDB compatibility）   文档数据库，适用于目录和用户资料管理
Amazon Neptune 									图形数据库 ，适合社交网络和推荐引擎
Amazon Managed Blockchain						管理区块链网络，分布式分类账系统
Amazon Quantum Ledger Database - Amazon QLDB		完整的历史记录	记录无法删除
Amazon Elastic Cache 								数据库加速缓存，支持Redis Memcached
Amazon DynamoDB Accelerator （DAX）	 			支持DynamoDb的数据库缓存加速
## AWS 安全性
AWS的安全模式为：责任共担模式。即Amazon负责云的安全，设施，场地等，而客户自己负责云里面的安全，资源访问隔离，流量入站出站控制等
Amazon就像是房屋建造者，负责房子本身的安全可靠；而客户需要负责房子门窗关闭，以保证安全。
![image.png](_assets/AWS%20基础服务/1638761074565-9a6debfc-240a-470e-8b09-c8a3582cbbb0.png)

### IAM - AWS Identity and Access Management 
AWS Identity and Access Management (IAM) 提供涵盖整个 AWS 的精细访问控制。使用 IAM，您可以指定谁以及在哪些条件下可以访问哪些服务和资源。使用 IAM 策略，您可以管理对员工和系统的权限，确保实现最小权限
![Arch_AWS-Identity-and-Access-Management_64@5x.png](_assets/AWS%20基础服务/1638771085435-dba8309c-740f-4a5d-87ae-c145a6f01466.png)
**根用户**
首次创建亚马逊云账户是，会有一个root账户，拥有所有权限
不要用root用户进行日常操作，以免带来不可逆的操作，
通常会用root账户创建一个IAM用户，IAM用户有创建其他用户的权限，和少量的root权限
**IAM用户**
与AWS服务和资源交互的人员或应用程序。由名称和凭证组成。
**IAM策略**
以文档形式写好该IAM用户的权限范围
![image.png](_assets/AWS%20基础服务/1638762626794-7693d2bd-6334-4f65-b5ee-a693a471392a.png)
**IAM组**
IAM用户的集合，group可以统一用户的权限范围
**IAM角色**
理解成状态变换的用户，在某段时间内具有某种权限，权限是临时的。
比如说，员工A早上过来进行开发，此时是的角色是开发者，下午开发好了，需要去到服务器进行部署，此时是运维者，此时权限变更为运维，而开发相关的权限会被移除。
![image.png](_assets/AWS%20基础服务/1638762945446-6f61be52-3545-4e63-a29d-c6039e7ff1ee.png)
**MFA - Multi-Factor Authentication**
MFA多重验证， 验证码

### AWS Organization
组织单位
将账户分组到组织单位OU中，便于管理具有类似业务或安全性要求的账户
![Arch_AWS-Organizations_64@5x.png](_assets/AWS%20基础服务/1638771229427-ec8c5cd4-6852-4825-a2d5-feb2ae8e49a3.png)
集中管理多个aws账户，控制访问权限管理。资源访问管理
![image.png](_assets/AWS%20基础服务/1638771348486-81c6e35f-32f3-47ce-87e6-031247559498.png)

### AWS Artifact - 合规性
AWS的业务遍布全球，由于不同地区对于不同的应用服务有不同的法律合规性
可以使用Artifact管理不同地区合规性的文档
[Artifact 不同地区合规性文档](https://aws.amazon.com/cn/compliance/customer-center/)
![Arch_AWS-Artifact_64@5x.png](_assets/AWS%20基础服务/1638772548290-cf25a96b-86ba-4ade-9d0b-8dcd0f29d06a.png)

### DDoS 防护
ddos 分布式拒绝服务，简单来说就是不断的访问，导致服务器过载奔溃
**UDP泛洪**
![image.png](_assets/AWS%20基础服务/1638772891669-797e630c-8a29-4cd3-b935-21023ed05961.png)
借刀杀人的套路，设定好返回地址为要攻击的服务器地址，耗尽资源
解决方案：使用安全组

**HTTP 攻击**
直接攻击服务器，占用资源，让正常的用户的访问无法得到处理
![image.png](_assets/AWS%20基础服务/1638772982031-368dfe01-2264-4c1c-bcfe-0fa21d6172c8.png)
解决方案：
使用Amazon Shield 免受DDoS攻击

- Amazon Shield Standard 标准 免费防御DDoS
- Amazon Shield Advanced： 付费高级版本，实时监控恶意流量。还能集成其他AWS的组件服务，如 cloudfront。route53 elb，

Amazon Shield 和Amazon WAF能防御复杂的DDoS攻击。          Amazon Web Application Firewall： Amazon WAF web应用防火墙

**Slowloris攻击**
某个请求故意让请求处理变得很久，让后面等待的请求得不到处理
解决方案：使用ELB负载均衡
![image.png](_assets/AWS%20基础服务/1638773046955-c0255baf-0e32-4df2-8918-16db630dd504.png)

### 其他安全
**对资源加密**
静态加密
传输加密
SSL 套接
AWS Key Management Service ： AWS KMS  进行密钥管理
![Arch_AWS-Key-Management-Service_64@5x.png](_assets/AWS%20基础服务/1638773274667-cf4ec240-6b15-4b88-97b0-303b16316091.png)
Amazon Inspector： 	进行aws设施的安全评估
![Arch_Amazon-Inspector_64@5x.png](_assets/AWS%20基础服务/1638773301698-803124d2-27b3-4c8d-ab49-fb1da9d213a1.png)
Amazon GuardDuty ： 	威胁监测服务 ，异常监测
![Arch_Amazon-GuardDuty_64@5x.png](_assets/AWS%20基础服务/1638773315160-3596b43a-9fe5-44f5-ac96-5ea80530ecbb.png)

## AWS 监控
### Amazon Cloud Watch
实时监控aws资源和应用程序的情况，创建条件阈值，发送监控通知。
![image.png](_assets/AWS%20基础服务/1638773549369-3a85316c-ee10-487d-9ff3-f1d52973cde8.png)

### Amazon Cloud Trail
一种全面的API审核工具，每个请求都会被记录在CouldTrail引擎中。有点类似于日志操作记录，每个操作都会被记录下来
### Amazon Trusted Advisory
一款顾问工具。评估您的资源状态情况，给出优化建议。
五个指标

- 成本优化
- 性能
- 安全性
- 容错能力
- 服务限制

![image.png](_assets/AWS%20基础服务/1638773646165-ff20473d-8174-4e6f-b75d-1a52c6c240a8.png)
## AWS 的定价策略和支持
### AWS 免费套餐
[https://aws.amazon.com/cn/free/](https://aws.amazon.com/cn/free/)

1. 永久免费

如：AWS Lambda 一个月一百万次的调用，基本上永久免费

2. 12个月免费

如：S3 12个免费实用

3. 短期试用

如：AWS Lightsai 一个月试用
### AWS Bill 账单管理
账单管理 bill management
![image.png](_assets/AWS%20基础服务/1638773924286-36f568ef-2e2b-4c89-b721-9baaa410309e.png)
账单整理
使用AWS Orgnazion中的功能。管理公司中各个账号的账单，把各处的账单集中到一个地方。

### AWS Budget 预算管理
AWS Budget  针对不同的场景设定预算
![image.png](_assets/AWS%20基础服务/1638777641351-3cdb56bf-5f5d-4998-b73c-80b658c89f89.png)

### AWS Cost Explorer
查看和分析AWS 的费用支出情况
![image.png](_assets/AWS%20基础服务/1638777689409-473ba12e-0d07-44f9-82eb-108711b0cbaf.png)

### AWS  Support 计划
support类型
1. 基本支持（免费）
文档、白皮书、论坛支持、AWS Trusted Advisor、AWS Personal Health Dashboard
2. 开发支持
3. 商务支持
4. 企业支持
![image.png](_assets/AWS%20基础服务/1638777728824-2fa66a1a-3938-40f5-a941-ca22964a44a6.png)
### Amazon Marketplace
一种数字目录，包含独立软件供应商提供的上千款软件产品。有点类似于 应用商店/插件中心，一键部署等
[Amazon Marketplace](https://aws.amazon.com/marketplace/?nc2=type_a)
## AWS 迁移和创新
### CAF - AWS Cloud Adoption Framework
The AWS Cloud Adoption Framework (AWS CAF) leverages AWS experience and best practices to help you digitally transform and accelerate your business outcomes through innovative use of AWS. AWS CAF identifies specific organizational capabilities that underpin successful cloud transformations
CAF 快速顺利迁移到云上 Accelerate your cloud powered digital transformation
云迁移六项关键因素

**不同迁移的视角**
1. 业务  -  财务分析师
2. 人员  -  HR
3. 监管  -  云架构师
4. 平台
5. 安全性
6. 操作技术运维

**6R 迁移策略**

1. Re-host 			重新托管，直接迁移
2. Re-platform 		更换平台，修补后迁移
3. Retired 			停用，不再使用的应用不搬上去云
4. Retain 			保留，暂时不上云
5. Re-phurse 		重新购买
6. Refactory 		重构，写代码
### Snow系列
snow系列是一组物理设备
下面几个类别的区别是主要是容量不同
#### Amazon Snowcone
坚固安全的小型边缘计算和数据传输设备
2个cpu，4gb内存和8tb存储容量
#### Amazon Snowball

- **Snowball Edge Storage Optimized**

适合大型数据迁移和重复传输，高容量
80tb HDD 存储，用于数据块卷和s3对象存储
1tb 固态存储
40个cpu和80gb内存。 相当于一个独立的C5实例

- **Snowball Edge Compute Optimized**

适合机器学习，视频分析，分心数据等
42tb hdd ，兼容数据快卷和s3
7.65tb的ssd
52个vCPU。208GB内存 ，运行着Amazon EC2 sbe-c and sbe-g实例 。相当于独立的C5，M5a，G3和P3实例
#### Amazon Snowmobile
一次100PB容量，适合海量数据移动
45英尺场的集装箱。要用牵引车来拉。哇靠~
## AWS 创新领域
AWS VMware Cloud			VMware Cloud 虚拟机云
Amazon SageMaker			部署机器学习模型
Amazon Augmented AI			机器学习平台
Amazon Lex					语音智能助手
Amazon Textract				提取文档中的文本
Amazon Comprehend			发现文本中的模式
Amazon Fraud Detector			识别潜在的欺诈性在线活动
Amazon DeepRacer			机器强化学习
Amazon ground station			卫星通信
## AWS之旅
### Amazon Well Architected
这是一个评估您的架构好不好、完不完善的工具 
![image.png](_assets/AWS%20基础服务/1638778900818-63e9b804-c79e-4489-87ea-5e9bb0813c43.png)
五个指标

- 卓越运营
   - 监控系统，实现商业价值。进而优化流程和程序
   - 使用部署管道自动执行更改，或响应被触发的事件
- 安全性
   - 数据完整性 和 安全性
- 可靠性
   - 恢复规划。db的数据恢复
-  性能效率
   - 高效利用IT和计算资源
- 成本优化
   - 控制资金方向
   - EC2使用率等
### AWS 优势
AWS 服务，术语
6大优势
1.将固定费用交易变为可变费用
2.实现规模经济效益
实现比单独运行数据中心更低的可变成本
3.无需猜测容量
4.提供速度和敏捷性
5.不在话费资金来运行和维护数据中心
6.数分钟内实现全球部署
使用AWS CloudFormation 自动完成部署

参考资料：
官网：[https://aws.amazon.com/](https://aws.amazon.com/)
icon：[https://www.fintail.me/awsicons.html](https://www.fintail.me/awsicons.html)
网易云课堂：[网易云课堂亚马逊课程](https://study.163.com/courses-search?keyword=%E4%BA%9A%E9%A9%AC%E9%80%8A#/?scht=30)
基于课程：[亚马逊云从业者必修知识](https://study.163.com/course/courseMain.htm?courseId=1212155814)

无需预置或管理基础设施即可运行代码。只需编写并将代码作为 .zip 文件或容器镜像上传即可
无需预置或管理基础设施即可运行代码。只需编写并将代码作为 .zip 文件或容器镜像上传即可
