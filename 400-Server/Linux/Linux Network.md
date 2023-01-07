# 常用的网络命令
| 命令 | 用途 |
| --- | --- |
| ping | 向网络主机发送 ICMP ECHO__ REQUEST数据包 |
| traceroute | 显示数据包到网络主机的路由路径 |
| netstat | 显示网络连接、路由表、网络接口数据、伪连接以及多点传送成员等信息 |
| ftp | 文件传输命令 |
| lftp | 改善后的文件传输命令 |
| wget | 非交互式网络下载器 |
| ssh | OpenSSH（SSH协议的免费开源实现）版的SH客户端（远程系统登录命令） |
| scp | secure copy的缩写，是远程复制文件命令 |
| sftp | secure file transfer program的缩写，安全文件传输程序 |

# 检查、检测网络
## ping 向网络主机发送特殊数据包
ping命令会向指定的网络主机发送特殊网络数据包IMCP ECHO_REQUEST，大多数的网络设备收到后都会做出回应，即可验证网络连接是否正常
```shell
[root@localhost ~]# ping www.baidu.com
PING www.a.shifen.com (182.61.200.7) 56(84) bytes of data.
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=1 ttl=49 time=41.8 ms
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=2 ttl=49 time=41.3 ms
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=3 ttl=49 time=46.7 ms
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=4 ttl=49 time=47.3 ms
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=5 ttl=49 time=49.3 ms
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=6 ttl=49 time=50.5 ms
64 bytes from 182.61.200.7 (182.61.200.7): icmp_seq=7 ttl=49 time=40.7 ms
^C
--- www.a.shifen.com ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6011ms
rtt min/avg/max/mdev = 40.747/45.448/50.586/3.755 ms
[root@localhost ~]# 

```
## traceroute 跟踪网络数据包的传输路径
traceroute程序会显示文件通过网络从本地系统传输到指定主机过程中所有停靠点的列表
```shell
[root@localhost ~]# traceroute www.baidu.com
traceroute to www.baidu.com (182.61.200.6), 30 hops max, 60 byte packets
 1  gateway (192.168.1.1)  13.430 ms  12.920 ms  12.030 ms
 2  * * *
 3  10.132.135.213 (10.132.135.213)  10.341 ms  17.447 ms  17.750 ms
 4  10.132.133.169 (10.132.133.169)  17.175 ms  16.704 ms  16.267 ms
 5  14.197.242.101 (14.197.242.101)  6.589 ms * 14.197.242.197 (14.197.242.197)  15.308 ms
 6  14.197.253.21 (14.197.253.21)  15.016 ms 14.197.248.189 (14.197.248.189)  45.912 ms 14.197.248.185 (14.197.248.185)  45.735 ms
 7  14.197.253.137 (14.197.253.137)  45.551 ms 14.197.252.45 (14.197.252.45)  45.367 ms 14.197.253.137 (14.197.253.137)  45.288 ms
 8  14.197.252.50 (14.197.252.50)  45.037 ms 14.197.248.94 (14.197.248.94)  44.950 ms 14.197.252.54 (14.197.252.54)  44.836 ms
 9  14.197.149.182 (14.197.149.182)  44.689 ms 14.197.178.102 (14.197.178.102)  54.022 ms  53.913 ms
10  182.61.255.2 (182.61.255.2)  44.326 ms 182.61.255.32 (182.61.255.32)  56.021 ms 182.61.255.28 (182.61.255.28)  56.394 ms
11  182.61.255.47 (182.61.255.47)  56.211 ms 182.61.255.45 (182.61.255.45)  56.131 ms  56.019 ms
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
[root@localhost ~]# 

```
## netstat 检查网络设备及统计数据
netstat可以用于查看不同网络设置及数据。通过使用其丰富的参数选项，我们可以查看网络启动过程的许多特性。
```shell
[root@localhost ~]# netstat -ie
Kernel Interface table
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:ebff:fe68:334a  prefixlen 64  scopeid 0x20<link>
        ether 02:42:eb:68:33:4a  txqueuelen 0  (Ethernet)
        RX packets 38  bytes 20581 (20.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 45  bytes 3914 (3.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.105  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::e7d9:59b7:d769:34da  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:0f:76:d0  txqueuelen 1000  (Ethernet)
        RX packets 2104204  bytes 2446313615 (2.2 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 541798  bytes 51446232 (49.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 1590  bytes 201205 (196.4 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1590  bytes 201205 (196.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethc9e13a1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::fc85:d5ff:fe87:4d32  prefixlen 64  scopeid 0x20<link>
        ether fe:85:d5:87:4d:32  txqueuelen 0  (Ethernet)
        RX packets 38  bytes 21113 (20.6 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 53  bytes 4570 (4.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[root@localhost ~]# 

```
对网络进行日常诊断，关键是看能否在每个接口信息第四行的开头找到**UP**这个词以及能否在第二行的 **inet addr**字段找到有效的IP地址。UP代表着该网络接口已启用，而对于使用动态主机配置协议的系统（DHCP）， inet addr字段里面的有效IP地址则说明了DHCP正在工作

查看路由表
```shell
[root@localhost ~]# netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         gateway         0.0.0.0         UG        0 0          0 ens33
172.17.0.0      0.0.0.0         255.255.0.0     U         0 0          0 docker0
192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 ens33
[root@localhost ~]# 
```
# 网络传输文件
## ftp 使用文件传输协议传输文件
```shell
NAME
     ftp — Internet 文件传输程序 (file transfer program)

概述 (SYNOPSIS)
     ftp [-pinegvd] [host] pftp [-inegvd] [host]

说明 (DESCRIPTION)
     用户通过 Ftp 这个程序来使用 Internet 上的标准文件传输协议 (File Transfer  Protocol).
     本程序允许用户向远端网站发送文件, 或从远端网站接收文件.

```
## wget 非交互式网络下载工具``
CLI形式的下载程序，可以下载内容或者站点的文件
```shell
[root@localhost ~]# wget www.baidu.com
--2021-01-20 15:38:31--  http://www.baidu.com/
正在解析主机 www.baidu.com (www.baidu.com)... 182.61.200.7, 182.61.200.6
正在连接 www.baidu.com (www.baidu.com)|182.61.200.7|:80... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：2381 (2.3K) [text/html]
正在保存至: “index.html”

100%[=====================================================================>] 2,381       --.-K/s 用时 0s      

2021-01-20 15:38:32 (103 MB/s) - 已保存 “index.html” [2381/2381])

[root@localhost ~]# wget https://wx1.sinaimg.cn/large/5f808b33ly1gmta1aw8p0j20oa0sg42g.jpg
--2021-01-20 15:38:58--  https://wx1.sinaimg.cn/large/5f808b33ly1gmta1aw8p0j20oa0sg42g.jpg
正在解析主机 wx1.sinaimg.cn (wx1.sinaimg.cn)... 124.42.245.30
正在连接 wx1.sinaimg.cn (wx1.sinaimg.cn)|124.42.245.30|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：130740 (128K) [image/jpeg]
正在保存至: “5f808b33ly1gmta1aw8p0j20oa0sg42g.jpg”

100%[=====================================================================>] 130,740     --.-K/s 用时 0.04s   

2021-01-20 15:38:58 (3.18 MB/s) - 已保存 “5f808b33ly1gmta1aw8p0j20oa0sg42g.jpg” [130740/130740])

[root@localhost ~]# 

```
# 与远程主机通信
## ssh 安全登录
为了解决明文传送的问题，一个叫做SSH（ Secure Shell的缩写）的新协议应运而生。SSH协议解决了与远程主机进行安全通信的两个基本问题：
第一，该协议能验证远程主机的身份是否真实，从而避免中间人攻击；
第二，该协议将本机与远程主机之间的通信内容全部加密。

SSH协议包括两个部分：一个是运行在远程主机上的SSH服务端，用来监听端口22上可能过来的连接请求；另一个是本地系统上的SSH客户端，用来与远程服务器进行通信。
```shell
[root@localhost ~]# ssh --help
unknown option -- -
usage: ssh [-1246AaCfGgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]
           [-D [bind_address:]port] [-E log_file] [-e escape_char]
           [-F configfile] [-I pkcs11] [-i identity_file]
           [-J [user@]host[:port]] [-L address] [-l login_name] [-m mac_spec]
           [-O ctl_cmd] [-o option] [-p port] [-Q query_option] [-R address]
           [-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]]
           [user@]hostname [command]
[root@localhost ~]# 

```
ssh命令除了能开启远程系统上的shll会话外，还能在远程系统上执行单个简单命令。
例如，我们可以在 remote-sys远程主机上执行free命令并将其结果直接输出到本地系统上。
![image.png](_assets/Linux%20Network/1611128847394-028ef328-2e51-4dc8-8783-0d4526dd954e.png)
该特性可以有更有趣的用途，比如在远程系统上执行ls命令后直接将运行结果输出到本地系统的文件中。
![image.png](_assets/Linux%20Network/1611128854158-50c7fc79-c8f5-4157-9244-ae4964f215dc.png)
## scp和sftp 安全传输文件
scp，sftp分别是cp，ftp的安全版本。而且支持远程加密传输
```shell
[root@localhost ~]# scp
usage: scp [-12346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
           [-l limit] [-o ssh_option] [-P port] [-S program]
           [[user@]host1:]file1 ... [[user@]host2:]file2
[root@localhost ~]# sftp
usage: sftp [-1246aCfpqrv] [-B buffer_size] [-b batchfile] [-c cipher]
          [-D sftp_server_path] [-F ssh_config] [-i identity_file] [-l limit]
          [-o ssh_option] [-P port] [-R num_requests] [-S program]
          [-s subsystem | sftp_server] host
       sftp [user@]host[:file ...]
       sftp [user@]host[:dir[/]]
       sftp -b batchfile [user@]host
[root@localhost ~]# 

```

