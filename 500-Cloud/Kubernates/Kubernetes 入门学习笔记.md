# Kubernetes是什么？
1.它是一个全新的基于容器技术的分布式架构领先方案。
 谷歌自己老早就开始玩容器技术了，基于自己玩了十多年的Borg开发出来Kubernetes，是Brog的开源版本。直到2015年4月，传闻许久的Borg论文伴随Kubernetes的高调宣传被谷歌首次公开，大家才得以了解它的更多内幕。正是由于站在Borg这个前辈的肩膀上，汲取了Borg过去十年间的经验与教训，所以Kubernetes一经开源就一鸣惊人，并迅速称霸容器领域
2.它是一个可以简化系统设计的设计思想。Kubernetes提供了强大的自动化机制，所以系统后期的运维难度和运维成本大幅度降低
3.是一个开放的开发平台。
4.支持分布式系统的平台

borg系统架构图
![image.png](./_assets/Kubernetes%20%E5%85%A5%E9%97%A8%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/1607307624827-2dbf7fec-6a05-4383-b78a-445ea9febcef.png)

k8s架构图
![image.png](./_assets/Kubernetes%20%E5%85%A5%E9%97%A8%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/1607307669151-57a4415e-5321-4a8e-9535-7f5da663129e.png)
集群数目一般需要大于等于3，  且最好是奇数，因为有投票机制

# k8s的组件
# APISERVER
所有服务访问统一入口
# Replication Controller
维持副本期望数目
# Scheduler
负责介绍任务，选择合适的节点进行分配任务
# etcd
etcd是持久化服务，存储k8s节点
etcd的方将它定位成一个可信赖的分布式键值存储服务，它能够为整个分布式集群存储
些关键数据，协助分布式集群的正常运转

etcd架构图，采取了http协议
![image.png](./_assets/Kubernetes%20%E5%85%A5%E9%97%A8%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/1607307903950-34727924-b01d-474a-b2a9-093432805d1e.png)

# node节点
kubelet 和CRI ，container runtime interface？
kublet和cri，这里主要是和docker进行交互处理，维持pod生命周期
kubeproxy 提供负载均衡，

ETCD：键值对数据库储存K8s集群所有重要信息（持久化
# Kubelet
直接跟容器引擎交互实现容器的生命周期管理
# KubeProxy
负责写入规则至 IPTABLES、IPvs实现服务映射访间的
COREDNS：可以为集群中的svC创建一个域名IP的对应关系解析
DASHBOARD：给K8S集群提供一个B/S结构访问
INGRESS CONTROLLER, 提供到7层的代理，官方只有四层
FEDERATION：提供一个可以跨集群中心多K8S统一管理功能
PROMETHEUS：提供K8s集群的监控能力
ELK：提供K8s集群日志统一分析介入平台

# k8s的pod
什么是pod

- 自主式pod
- 控制管理的pod


Replication Controller用来确保容器应用的副本数始终保持在用户定义的副本数，即如果
有容器异常退出，会自动创建新的Pod来替代；而如果异常多出来的容器也会自动回收。
在新版本的 Kubernetes中建议使用 ReplicaSe来取代 ReplicationControlle
Replicase跟 Replication Controller没有本质的不同，只是名字不一样，并且
ReplicaSe支持集合式的 selector
虽然 ReplicaSe可以独立使用，但一般还是建议使用 Deployment来自动管理
Replicase，这样就无需担心跟其他机制的不兼容问题（比如 ReplicaSe不支持
rolling-update但 Deployment支持）


Horizontal Pod Autoscaling仅适用于 Deployment和 ReplicaSe，在v1版本中仅支持根据Pod
的cPU利用率扩所容，在 vlalpha版本中，支持根据内存和用户自定义的 metric扩缩容

Statefulset是为了解决有状态服务的问题（对应 Deployments和 Replicasets是为无状态服务而设
计），其应用场景包括：
*稳定的持久化存储，即Pod重新调度后还是能访问到相同的持久化数据，基于PVC来实现
*稳定的网络标志，即Pod重新调度后其 PodName和 HostName不变，基于 Headless Service
（即没有 Cluster ip的 Service）来实现
*有序部署，有序扩展，即Pod是有顺序的，在部署或者扩展的时候要依据定义的顺序依次依次进
行（即从0到N1，在下一个Pod运行之前所有之前的Pod必须都是 Running和 Ready状态）
基于 init containers来实现
*有序收缩，有序删除（即从N1到0）

Daemon Set确保全部（或者些）Node上运一个Pod的副本。当有Node加入集群时，也会为他们
新增一个Pod。当有Node从集群移除时，这些Pod也会被回收。删除 Daemon Set将会删除它创建
的所有Pod
使用 Daemon Set的一些典型用法：
*运行集群存储 daemon，例如在每个Node上运行 glusterd、ceph
*在每个Node上运行日志收集 daemon，例如 fluent、 logstash。
*在每个Node上运行监控 daemon，例如 Prometheus Node Exporter

Job负责批处理任务，即仅执行一次的任务，它保证批处理任务的一个或多个Pod成功结束
Cron job管理基于时间的Job，即：
*在给定时间点只运行一次
*周期性地在给定时间点运行

服务发现
pod集群之间使用的是用service来调用
# 网络通讯方式
pod与pod是怎么通信的？
网络通讯模型
Kubernetes的网络模型假定了所有Pod都在一个何可以直接连通的扁平的网络空间中，这在
GCE（ Google Compute Engine）里面是现成的网络模型， Kubernetes假定这个网络已经存在。
而在私有云里搭建 Kubernetes集群，就不能假定这个网络已经存在了。我们需要自己实现这
个网络假设，将不同节点上的 Docker容器之间的互相访问先打通，然后运行 Kubernetes

同一个Pod内的多个容器之间：lo
各Pod之间的通讯：verla Network
Pod与 Service之间的通讯：各节点的 Iptables规则

Flannel是 Cores团队针对 Kubernetes设计的一个网络规划服务，简单来说，它的功能是
让集群中的不同节点主机创建的 Docker容器都具有全集群唯一的虚拟IP地址。而且它还能在
这些IP地址之间建立一个覆盖网络（0 verla Network），通过这个覆盖网络，将数据包原封
不动地传递到目标容器内
**重点网络通讯图**
![image.png](./_assets/Kubernetes%20%E5%85%A5%E9%97%A8%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/1607311675295-0f9e5e09-93bb-4100-8107-8c8913ad780a.png)
ETCD之 Flannel提供说明：
存储管理 Flannel可分配的IP地址段资源
监控ETCD中每个Pod的实际地址，并在内存中建立维护Pod节点路由表

同一个Pod内部通讯：同一个Pod共享同一个网络命名空间，共享同一个 Linux协议栈
Pod1至Pod2
Podl与Pod2不在同一台主机，Pod的地址是与 docker0在同一个网段的，但 docker0网段与宿主机网卡是两个完
全不同的IP网段，并且不同Node之间的通信只能通过宿主机的物理网卡进行。将Pod的IP和所在Node的IP关联起来，通过
这个关联让Pod可以互相访问
Podl与Pod2在同一台机器，由 Docker0网桥直接转发请求至Pod2，不需要经过 Flannel演示
Pod至 Service的网络：目前基于性能考虑，全部为 iptables维护和转发
Pod到外网：Pod向外网发送请求，查找路由表，转发数据包到宿主机的网卡，宿主网卡完成路由选择后， iptables执
行 Masquerade，把源IP更改为宿主网卡的IP，然后向外网服务器发送请求
外网访问Pod:Service

![image.png](./_assets/Kubernetes%20%E5%85%A5%E9%97%A8%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/1607312097413-942638fb-8a77-4682-b2e5-444fcae50124.png)







linux的分区解释：？？
swap分区。。。。。。

为什么要关闭swap分区？
防止容器运行在虚拟内存中。

centos 7 内核版本升级到4.4 版本使得kubernetes更加稳定
> 内核和CentOS的关系？Linux内核和内核的关系





















