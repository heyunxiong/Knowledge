# 问题背景
工作过程中，需要处理一下Linux的时间，然后发现自己对于shell脚本的时间处理不是很熟悉，查了下资料记录一下。
## 解决思路
解决的方法其实很简答，就是取前后时间，然后进行相减即可，只是期间需要去查一下对应的函数，奈何自己不熟。


```
#starttime=$(date+%s)	//获取开始的时间戳(秒)
#endtime=$(date +%s)	//获取结束的时间戳(秒)
#diff=$(($endtime-starttime)  //相减时间戳
#echo ${diff} 			//打印差值,显示的是秒。如果要换成分钟, 除以60就好了!
```

```linux
[centos@localhost ~]$ starttime=$(date +%s)
[centos@localhost ~]$ endtime=$(date +%s)
[centos@localhost ~]$ diff=$(($endtime-$starttime))
[centos@localhost ~]$ echo starttime:$starttime ,endtime:$endtime ,diff:$diff
starttime:1547132367 ,endtime:1547132378 ,diff:11
```
# 相关知识补充
### date的语法

```
date [-u] [-d datestr] [-s datestr] [--utc] [--universal] [--date=datestr] [--set=datestr] [--help] [--version] [+FORMAT] [MMDDhhmm[[CC]YY][.ss]]
```

参数说明：
-d datestr : 显示 datestr 中所设定的时间 (非系统时间)
-s datestr : 将系统时间设为 datestr 中所设定的时间
-u : 显示目前的格林威治时间 --version : 显示版本编号
--help : 显示辅助讯息
### 时间日期格式详细参数
#### 时间:
```
% : 印出 %
%n : 下一行
%t : 跳格
%H : 小时(00..23)
%I : 小时(01..12)
%k : 小时(0..23)
%l : 小时(1..12)
%M : 分钟(00..59)
%p : 显示本地 AM 或 PM
%r : 直接显示时间 (12 小时制，格式为 hh:mm:ss [AP]M)
%s : 从 1970 年 1 月 1 日 00:00:00 UTC 到目前为止的秒数
%S : 秒(00..61)
%T : 直接显示时间 (24 小时制)
%X : 相当于 %H:%M:%S
%Z : 显示时区
```

#### 日期:
```
%a : 星期几 (Sun..Sat)
%A : 星期几 (Sunday..Saturday)
%b : 月份 (Jan..Dec)
%B : 月份 (January..December)
%c : 直接显示日期与时间
%d : 日 (01..31)
%D : 直接显示日期 (mm/dd/yy)
%h : 同 %b
%j : 一年中的第几天 (001..366)
%m : 月份 (01..12)
%U : 一年中的第几周 (00..53) (以 Sunday 为一周的第一天的情形)
%w : 一周中的第几天 (0..6)
%W : 一年中的第几周 (00..53) (以 Monday 为一周的第一天的情形)
%x : 直接显示日期 (mm/dd/yy)
%y : 年份的最后两位数字 (00.99)
%Y : 完整年份 (0000..9999)
```

说明 若是不以加号作为开头，则表示要设定时间，而时间格式为 MMDDhhmm[[CC]YY][.ss]，其中 MM 为月份，DD 为日，hh 为小时，mm 为分钟，CC 为年份前两位数字，YY 为年份后两位数字，ss 为秒数
#### 实例
```
[centos@localhost ~]$ date
Thu Jan 10 06:49:06 PST 2019
[centos@localhost ~]$ date '+%c'
Thu 10 Jan 2019 06:49:35 AM PST
[centos@localhost ~]$ date '+%D'
01/10/19
[centos@localhost ~]$ date '+%x'
01/10/2019
[centos@localhost ~]$ date '+%T'
06:50:39
[centos@localhost ~]$ date '+%X'
06:50:43 AM
[centos@localhost ~]$ date '+%T%n%D'
```
