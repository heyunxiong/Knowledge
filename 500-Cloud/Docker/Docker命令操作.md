## Docker
为什么会有Docker? Docker的出现解决了什么问题?
在Docker之前的问题：
## Docker的核心组件

- **Docker 客户端和服务器**，也称为Docker引擎
   - Docker是一个客户端/服务器（C/S）架构的程序。
   - Docker客户端只需向Docker服务器或守护进程发出请求，服务器或守护进程将完成所有工作并返回结果
- **Docker Images 镜像**
   - 镜像是构建Docker世界的基石。用户基于镜像来运行自己的容器
- **Docker Container 容器**
   - Docker可以帮用户构建和部署容器，用户只需要把自己的应用程序或服务打包放进容器即可
- **Registry 仓库**
   - Docker用Registry来保存用户构建的镜像
   - Registry分为公共和私有两种。Docker公司运营的公共Registry叫作Docker Hub
## 三个基本概念

- 镜像

镜像就是一个模板，这个模板里面可以定义需要的配置；镜像是容器的基础。

- 容器

启动、开始、停止、删除；相互隔离，互不可见。

- 仓库

存放镜像文件的场所
## 镜像的操作
**获取镜像 docker pull**
命令：docker pull 镜像名称:标签
如：docker pull ubuntu:18.04
TAG 信息用于标记来自同一个仓库的不同镜像，不指定tag标签，默认拉取latest的版本
 例如 ubuntu 仓库中有多个镜像， 通过TAG 信息来区分发行版本， 如18.04、 18.10 等
```bash
[root@yunxionghost ~]# docker pull ubuntu
Using default tag: latest
Trying to pull repository docker.io/library/ubuntu ... 
latest: Pulling from docker.io/library/ubuntu
125a6e411906: Pull complete 
Digest: sha256:26c68657ccce2cb0a31b330cb0be2b5e108d467f641c62e13ab40cbec258c68d
Status: Downloaded newer image for docker.io/ubuntu:latest
[root@yunxionghost ~]# 
```

**查看镜像**
docker images
```bash
[root@yunxionghost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/ubuntu    latest              d2e4e1f51132        31 hours ago        77.8 MB
docker.io/tomcat    latest              e36064f7c6f0        2 years ago         528 MB
docker.io/mysql     latest              9228ee8bac7a        2 years ago         547 MB
```

**给镜像添加标签**
docker tag
```bash
[root@yunxionghost ~]# docker tag ubuntu:latest myubuntu:latest
[root@yunxionghost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
myubuntu            latest              d2e4e1f51132        31 hours ago        77.8 MB
docker.io/ubuntu    latest              d2e4e1f51132        31 hours ago        77.8 MB
docker.io/tomcat    latest              e36064f7c6f0        2 years ago         528 MB
docker.io/mysql     latest              9228ee8bac7a        2 years ago         547 MB
```

**查看镜像详细信息**
docker inspect
docker inspect ubuntu:latest
```bash
[root@yunxionghost ~]# docker inspect ubuntu:latest
[
    {
        "Id": "sha256:d2e4e1f511320dfb2d0baff2468fcf0526998b73fe10c8890b4684bb7ef8290f",
        "RepoTags": [
            "docker.io/ubuntu:latest",
            "myubuntu:latest"
        ],
```

**查看镜像历史**
docker history ubuntu:latest
```bash
[root@yunxionghost ~]# 
[root@yunxionghost ~]# docker history ubuntu:latest
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
d2e4e1f51132        31 hours ago        /bin/sh -c #(nop)  CMD ["bash"]                 0 B                 
<missing>           31 hours ago        /bin/sh -c #(nop) ADD file:37744639836b248...   77.8 MB             
[root@yunxionghost ~]# 
```
**搜索镜像**
docker search ubuntu
```bash
[root@localhost ~]# docker search ubuntu
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                           Ubuntu is a Debian-based Linux operating sys…   14159     [OK]       
websphere-liberty                WebSphere Liberty multi-architecture images …   283       [OK]       
ubuntu-upstart                   DEPRECATED, as is Upstart (find other proces…   112       [OK]       
neurodebian                      NeuroDebian provides neuroscience research s…   89        [OK]       
open-liberty                     Open Liberty multi-architecture images based…   52        [OK]       

```
**删除、清理镜像**
docker rmi、docker image rm 
当有该镜像创建的容器存在时， 镜像文件默认是无法被删除的

1. 使用镜像标签删除
```shell
[root@localhost ~]# docker images
REPOSITORY            TAG       IMAGE ID       CREATED         SIZE
myubuntu              latest    c6ad7e71ba7d   32 hours ago    63.2MB
ubuntu                18.04     c6ad7e71ba7d   32 hours ago    63.2MB
redis                 latest    ef47f3b6dc11   16 months ago   104MB

#移除自定义的tag的镜像，不影响原来的ubuntu镜像文件
[root@localhost ~]# docker rmi myubuntu:latest
Untagged: myubuntu:latest

[root@localhost ~]# docker images
REPOSITORY            TAG       IMAGE ID       CREATED         SIZE
ubuntu                18.04     c6ad7e71ba7d   32 hours ago    63.2MB
redis                 latest    ef47f3b6dc11   16 months ago   104MB

#最后一个镜像文件会删除文件层
[root@localhost ~]# docker rmi ubuntu:18.04
Untagged: ubuntu:18.04
Untagged: ubuntu@sha256:d21b6ba9e19feffa328cb3864316e6918e30acfd55e285b5d3df1d8ca3c7fd3f
Deleted: sha256:c6ad7e71ba7d4969784c76f57c4cc9083aa96bb969d802f2ea38f4aaed90ff93
Deleted: sha256:3e549931e0240b9aac25dc79ed6a6259863879a5c9bd20755f77cac27c1ab8c8

```

2. 使用镜像ID 移除

会先尝试删除所有指向该镜像的标签， 然后删除该镜像文件本身，这个时候，不管多少个标签都会删除。因为ID是唯一的。

docker image prune命令来进行清理。清理遗留的一些临时文件
会自动清理临时的遗留镜像文件层， 最后会提示释放的存储空间：
$ docker image prune -f

创建镜像
1.基于已有容器创建
docker [container] commit
```bash
$ docker run -it ubuntu:18.04 /bin/bash
root@a925cb40b3f0:/# touch test
root@a925cb40b3f0:/# exit
```
记住容器的 ID 为 a925cb40b3£0 。
此时该容器与原 ubuntu:18.04 镜像相比， 已经发生了改变， 可以使用 docker[container] commit命令来提交为一个新的镜像。提交时可以使用 ID 或名称来指定容器：
docker [container] commit-m "Added a new file" -a "Docker Newbee" a925cb40b3f0 test:0.1

2.基于本地模板导入
docker import 导入
$cat ubuntu-18.04-x86_64-minimal.tar.gz I docker import - ubuntu:lB.04

3.基于Dockefile创建镜像
最常见的创建方式，dockerfile是一个文本文件，利用给定的指令描述基于某个父镜像创建新镜像的过程。
docker build dockerfile文件

导出和载入

导出
导出镜像到本地文件，可以使用docker save
docker save -o ubuntu_latet.tart ubuntu:latest  //导出latest的ubuntu镜像到本地，保存为ubuntu_latst.tart

载入
导入镜像到本地列表
docker load -i ubuntu_18.04.tar 

上传镜像
上传镜像到仓库，默认是DockerHub官方镜像仓库（需要注册）
docker push 
## 容器的操作
容器的操作主要涉及：create, start, run, wait 
容器的状态状态有7种：

- created（已创建）
- restarting（重启中）
- running 或 Up（运行中）
- removing（迁移中）
- paused（暂停）
- exited（停止）
- dead（死亡）

创建容器
docker create 
创建后的容器处于停止状态
```bash
[root@localhost ~]# docker create -it ubuntu:latest
WARNING: IPv4 forwarding is disabled. Networking will not work.
8a9e5e5a0ec110746cd300a8b9d5ea950667979d7ccf9d3bb6582ef373730b08
[root@localhost ~]# 

```
docker start 启动容器
docker ps 查看docker的容器运行情况
```bash
[root@localhost ~]# docker start 8a9e
8a9e
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED         STATUS         PORTS     NAMES
8a9e5e5a0ec1   ubuntu:latest   "bash"    3 minutes ago   Up 7 seconds             blissful_knuth
[root@localhost ~]# 

```
docker run
创建并运行容器，相当于create+start的操作，如果本地没有镜像，还会自己去docker hub的仓库里面拉取镜像，运行完后容器自动终止
```bash
[root@localhost ~]# docker run ubuntu echo "hello ubuntu / docker"
WARNING: IPv4 forwarding is disabled. Networking will not work.
hello ubuntu / docker
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED         STATUS         PORTS     NAMES
8a9e5e5a0ec1   ubuntu:latest   "bash"    5 minutes ago   Up 2 minutes             blissful_knuth
[root@localhost ~]# 

```
docker run docker背后的操作

- 检查本地是否存在指定的镜像,不存在就从公有库载;
- 利用镜像创建一个容器,并启动该容器;
- 分配一个文件系统给容器,并在只读的镜像层外面挂载一层可读写层;
- 从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去;
- 从网桥的地址池配置一个P地址给容器;
- 执行用户指定的应用程序;
- 执行完毕后容器被自动终止

启动bash终端，并进入交互模式，exit推出交互模式，同时容器使命完成，处于停止状态！
docker run -it ubuntu:latest /bin/bash
```bash
[root@localhost ~]# docker run -it ubuntu:latest /bin/bash
WARNING: IPv4 forwarding is disabled. Networking will not work.
root@743784e2390a:/# echo hello-ubuntu 
hello-ubuntu
root@743784e2390a:/# 
root@743784e2390a:/# ps
   PID TTY          TIME CMD
     1 pts/0    00:00:00 bash
     8 pts/0    00:00:00 ps
root@743784e2390a:/# pwd
/
root@743784e2390a:/# exit
exit
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED         STATUS         PORTS     NAMES
8a9e5e5a0ec1   ubuntu:latest   "bash"    8 minutes ago   Up 6 minutes             blissful_knuth
[root@localhost ~]# 

```
后台启动
docker run -d ubuntu /bin/bash
返回一个id，通过docker ps查看

停止容器
```bash
$ docker test --rm -it ubuntu bash
$ docker pause test
$ docker ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
893c8llcf845 ubuntu "bash ” 2 seconds ago Up 12 seconds (Paused) test
```
docker pause  暂停 、 解除暂停
```bash
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED              STATUS              PORTS     NAMES
6e79f9a72762   ubuntu:latest   "bash"    About a minute ago   Up About a minute             silly_feistel
[root@localhost ~]# docker pause 6e79
6e79
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED              STATUS                       PORTS     NAMES
6e79f9a72762   ubuntu:latest   "bash"    About a minute ago   Up About a minute (Paused)             silly_feistel
[root@localhost ~]# docker unpause 6e79
6e79
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED              STATUS              PORTS     NAMES
6e79f9a72762   ubuntu:latest   "bash"    About a minute ago   Up About a minute             silly_feistel
[root@localhost ~]# 

```

docker stop 终止
```bash
[root@localhost ~]# docker stop 8a9e
8a9e
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@localhost ~]# 

```
docker ps -qa 查看容器ID

进入容器
使用-d参数时，容器启动在后台，用户无法看到容器中的信息，也无法进行操作
1.attach命令
使用attach命令的不方便：当多个窗口同时attach同一个容器时，所有窗口都会同步显示；当某个窗口因命令阻塞时，其他窗口也无法执行操作
而且，attach的方式进入容器，退出时会停止容器
```bash
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED         STATUS         PORTS     NAMES
6e79f9a72762   ubuntu:latest   "bash"    8 minutes ago   Up 8 minutes             silly_feistel
[root@localhost ~]# docker attach 6e79
root@6e79f9a72762:/# ls       
bin   dev  home  lib32	libx32	mnt  proc  run	 srv  tmp  var
boot  etc  lib	 lib64	media	opt  root  sbin  sys  usr
root@6e79f9a72762:/# exit   
exit
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@localhost ~]# 

```
2.exec命令
exec的方式进入容器，退出时容器不会停止
```bash
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED         STATUS         PORTS     NAMES
6e79f9a72762   ubuntu:latest   "bash"    7 minutes ago   Up 7 minutes             silly_feistel
[root@localhost ~]# docker exec -it 6e79 /bin/bash
root@6e79f9a72762:/# ls
bin   dev  home  lib32	libx32	mnt  proc  run	 srv  tmp  var
boot  etc  lib	 lib64	media	opt  root  sbin  sys  usr
root@6e79f9a72762:/# exit
exit
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE           COMMAND   CREATED         STATUS         PORTS     NAMES
6e79f9a72762   ubuntu:latest   "bash"    8 minutes ago   Up 8 minutes             silly_feistel
[root@localhost ~]# 

```
删除容器
默认情况下（强制 -f），只能删除处于终止或者退出状态下的容器，并不能删除正在运行的容器 
```bash
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS                        PORTS                    NAMES
6e79f9a72762   ubuntu:latest   "bash"                   10 minutes ago   Exited (0) 56 seconds ago                              silly_feistel
5bf6a0d55289   ubuntu:latest   "bash"                   11 minutes ago   Exited (0) 11 minutes ago                              friendly_rubin
[root@localhost ~]# docker rm 6e79
6e79
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS                        PORTS                    NAMES
5bf6a0d55289   ubuntu:latest   "bash"                   12 minutes ago   Exited (0) 12 minutes ago                              friendly_rubin
[root@localhost ~]# 
```
导出载入容器
docker export -o test for run.tar ce5
docker import test_for_run.tar - test/ubuntu:vl.O

查看容器
查看容器详情 docker inspect
```bash
[root@localhost ~]# docker inspect 5bf6
[
    {
        "Id": "5bf6a0d55289253622968f2cb7c37bfbe8f2c87defddaba4fb7e0f41e752eb7c",
        "Created": "2022-05-01T09:13:18.118878901Z",
        "Path": "bash",
        "Args": [],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
...
...
...
```
查看容器内进程
docker top 
```bash
[root@localhost ~]# docker top 902c
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                51310               51291               0                   17:33               pts/0               00:00:00            bash
[root@localhost ~]# 

```

查看统计信息，CPU 内存 网络等使用情况
docker stats  
```bash
CONTAINER ID   NAME            CPU %     MEM USAGE / LIMIT     MEM %     NET I/O     BLOCK I/O     PIDS
902cd999376e   elastic_cohen   0.00%     2.082MiB / 972.4MiB   0.21%     998B / 0B   12.7MB / 0B   1

```
其他容器命令

复制文件
docker cp命令支持在容器和主机之间复制文件
将主机的data复制到容器id为902c的temp路径下
docker cp data 902c:/tmp/
```bash
[root@localhost ~]# touch local-file.txt
[root@localhost ~]# docker cp local-file.txt 902c:/tmp/
[root@localhost ~]# docker  exec -it 902c /bin/bash
root@902cd999376e:/# cd tmp 
root@902cd999376e:/tmp# ls
local-file.txt
root@902cd999376e:/tmp# 

```
查看容器内文件系统的变更
docker container diff 
查看端口映射
docker container port 
更新容器配置
更新运行时配置，主要时一些资源的限制份额
docker update --cpu-quota 1000000 test
## 仓库的操作
Repository是集中存放镜像的地方

- DockerHub

官方最大的公共镜像仓库，https://hub.docker.com

- 第三方镜像仓库

阿里云镜像，腾讯云镜像仓库等

- 本地自建私有仓库

官方有提供repository容器
