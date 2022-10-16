> 学习资料：《Linux命令行大全》第四部分

# 什么是shell脚本
shell脚本就是包含一系列命令的文件。shell读取这个文件，然后执行里面的命令，里面的内容就和在提示符下一个一个命令输入执行一样。
```shell
#! /bin/bash
# This is my first shell script.
echo "hello world, script."
```
一般的shell格式开头都是 **#! /bin/bash**** **不成文的规定，#!是特殊结构，称为shebang，用来告诉操作系统该脚本应该使用的解释器的名字，说明该脚本是在什么shell环境下执行，这里表示使用bash shell(Bounce Again Shell) 
shell也是有多种分类的，bash是最常用的shell。# 后面的内容表示注释, 不会被shell执行。
## 执行权限和位置
shell脚本是一个普通的文本文件，编写完之后需要设置执行权限，并放在能够被shell发现的位置
设置可执行权限，使用命令 _chmod_
```shell
[root@localhost ~]# ll -l hello_world 
-rw-r--r--. 1 root root 73 1月  17 15:06 hello_world
[root@localhost ~]# chmod 755 hello_world 
[root@localhost ~]# ll -l hello_world 
-rwxr-xr-x. 1 root root 73 1月  17 15:06 hello_world
[root@localhost ~]# 
```
设置完执行权限后，执行脚本
```shell
[root@localhost ~]# hello_world
bash: hello_world: 未找到命令...
```
执行执行脚本发现无法找到命令
为什么呢？因为脚本的位置放得不对，shell无法发现这个脚本
那要放在哪里呢？首先看下目前环境变量$PATH中，shell会去找到的地方
```shell
[root@localhost ~]# echo $PATH
/usr/lib64/qt-3.3/bin:/root/perl5/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
```
可以看到，shell会去在列出来的文件目录下找相应的脚本，也就是说，现在这个hello_world应该放在其中一个目录中（冒号分开为一个目录）
```shell
### 列表中有/root/bin，在root下面创建bin，然后把脚本移动到该目录下。执行成功
[root@localhost ~]# pwd
/root
[root@localhost ~]# mkdir bin
[root@localhost ~]# mv hello_world bin
[root@localhost ~]# hello_world 
hello world, script.
```
是不是一定要这么做呢？也不是，还有一种方法，就是带上sh 或者 . 告诉shell 脚本的位置。
把脚本放回到原处，
```shell
[root@localhost ~]# mv bin/hello_world .
### 放回原处后，直接执行失败。
[root@localhost ~]# hello_world
-bash: /root/bin/hello_world: 没有那个文件或目录
[root@localhost ~]# sh hello_world 
hello world, script.
[root@localhost ~]# . hello_world 
hello world, script.
```
另外如果先前 echo $PATH 中没有我们想要的目录，可以自己添加上去，假设想把自己创建的myshell目录让shell发现，并把自己写的shell script放在该目录下，然后执行，结果是可以的。
```shell
### 设置完后会在每一个终端terminal会话中生效
[root@localhost ~]# mkdir myshell
### 这里报错是应该语法错误了，=有空格
[root@localhost ~]# export PATH = ~/myshell:"$PATH"
-bash: export: `=': 不是有效的标识符
-bash: export: `/root/myshell:/usr/lib64/qt-3.3/bin:/root/perl5/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin': 不是有效的标识符
[root@localhost ~]# export PATH=~/myshell:"$PATH"
### 成功的把自己的目录添加进去了
[root@localhost ~]# echo $PATH
/root/myshell:/usr/lib64/qt-3.3/bin:/root/perl5/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
### 移动脚本，然后在任意目录下都执行脚本，成功！
[root@localhost ~]# mv hello_world myshell/
[root@localhost ~]# hello_world
hello world, script.


```
脚本存放位置建议
个人使用的脚本放在自己的用户名下。~/bin， 比如sean/bin，jacky/bin，root/bin
系统上所用用户都可以使用的话通常放在/usr/local/bin
不建议放在/bin或者/usr/bin，因为这些目录是linux系统层次上的，包含一些发行商的维护文件
# 编写shell
尝试编写一个生成html的script
```shell
[root@localhost ~]# #尝试编写一个生成html的script
[root@localhost ~]# vim ~/bin/sys_info_page[root@localhost ~]# cat bin/sys_info_page 
#！/bin/bash
# Program to output a system information page
echo "<HTML>"
echo "	<HEAD>"
echo "		<TITLE>Page Title</TITLE>"
echo "	</HEAD>"
echo "	<BODY>"
echo "		Page body."
echo "	</BODY>"
echo "</HTML>"
[root@localhost ~]# 
[root@localhost ~]# chmod 755 bin/sys_info_page 
[root@localhost ~]# sys_info_page > sys_info_page.html
[root@localhost ~]# cat sys_info_page.html 
<HTML>
	<HEAD>
		<TITLE>Page Title</TITLE>
	</HEAD>
	<BODY>
		Page body.
	</BODY>
</HTML>
```
## 变量和常量
在脚本中添加变量
```shell
[root@localhost ~]# vim bin/sys_info_page 
[root@localhost ~]# cat bin/sys_info_page 
#！/bin/bash
# Program to output a system information page
#echo "<HTML>"
#echo "	<HEAD>"
#echo "		<TITLE>Page Title</TITLE>"
#echo "	</HEAD>"
#echo "	<BODY>"
#echo "		Page body."
#echo "	</BODY>"
#echo "</HTML>"

# 一个echo即可
#！/bin/bash
# Program to output a system information page

#声明变量title
title="System Information Report"
echo "<HTML>
 	 <HEAD>
#引用变量title	
            <TITLE>$title</TITLE>
         </HEAD
         <BODY>
		<H1>$title</H1>
	</BODY>
</HTML>"
[root@localhost ~]# 
[root@localhost ~]# sys_info_page>sys_info_page.html 
[root@localhost ~]# cat sys_info_page.html 
<HTML>
 	 <HEAD>
#引用变量title	
            <TITLE>System Information Report</TITLE>
         </HEAD
         <BODY>
		<H1>System Information Report</H1>
	</BODY>
</HTML>
[root@localhost ~]# 

```
在命令行上的定义变量和常量
```shell
[root@localhost ~]# foo="yes"
[root@localhost ~]# echo $foo
yes
[root@localhost ~]# 
### fool1变量未定义，直接引用会默认为空 等同于直接echo
[root@localhost ~]# echo $fool1

[root@localhost ~]# echo

```
变量的命名规则如下所示：

- 变量名称应由字母、数字和下划线组成。
- 变量名称的第一个字符必须是字母或者下划线
- 变量名称中不允许空格和标点

为变量和常量赋值
```shell
a=z 								#将字符串“z”赋值给变量a
b="a string" 				#嵌入的空格必须用引号括起来
c="a string and$b"  #可以被扩展到赋值语句中的其他扩展，比如变量
d=$(ls -l foo.txt)  #命令的结果
e=$((5*7)) 					#算术扩展
f="\t\ta string\n"  #转义序列，比如制表符和换行符

a=5 b="a string" 		#一行给多个变量赋值
```
关于{ }的使用
```shell
### 定义filename变量
[root@localhost test1]# filename="myfile"
### 使用filename变量创建一个文件
[root@localhost test1]# touch $filename
[root@localhost test1]# ll
总用量 0
-rw-r--r--. 1 root root 0 1月  17 16:07 myfile
### mv里的 第一个参数$filename 代表文件myfile，第二个参数是一个新的未定义的变量，mv 不接受这种
[root@localhost test1]# mv $filename $filename2
mv: 在"myfile" 后缺少了要操作的目标文件
Try 'mv --help' for more information.
### 使用{}后，${filename}2 表示 要把文件名由myfile改成myfile2
[root@localhost test1]# mv $filename ${filename}2
[root@localhost test1]# ll
总用量 0
-rw-r--r--. 1 root root 0 1月  17 16:07 myfile2
[root@localhost test1]# 
### 变量filename依旧是原来的值，说明修改的是文件
[root@localhost test1]# echo $filename
myfile
[root@localhost test1]# 

```
## here文档的方式
here文档？感觉是一种使用定位符的方式去开始和结束
hure文档或者说here文档来输出文本，here文档是I/O重定向的另外一种形式
```shell
command << token
text1
text2
text3
token
```
command 表示接受标注输入的命令名，token是用来嵌入文本结尾的字符串

现在是here文档形式来输出脚本，之前用的是echo
```shell
[root@localhost ~]# cat bin/sys_info_page 
#！/bin/bash
# Program to output a system information page
#echo "<HTML>"
#echo "	<HEAD>"
#echo "		<TITLE>Page Title</TITLE>"
#echo "	</HEAD>"
#echo "	<BODY>"
#echo "		Page body."
#echo "	</BODY>"
#echo "</HTML>"

# 一个echo即可
#！/bin/bash
# Program to output a system information page
#
#声明变量title
# TITLE="System Information Report for $HOSTNAME"
# CURRENT_TIME=$(date +"%x %r %Z")
# TIME_STAMP="Generated $CURRENT_TIME,by $USER"
# 
# echo "<HTML>
#  	 <HEAD>
#             <TITLE>$TITLE</TITLE>
#          </HEAD>
#          <BODY>
# 		<H1>$TITLE</H1>
# 		<P>$TIME_STAMP</P>
# 	</BODY>
# </HTML>"

# 使用here文档的形式输出文本信息
#！/bin/bash
# Program to output a system information page

#声明变量title
TITLE="System Information Report for $HOSTNAME"
CURRENT_TIME=$(date +"%x %r %Z")
TIME_STAMP="Generated $CURRENT_TIME,by $USER"
cat << _EOF_
<HTML>
         <HEAD>
            <TITLE>$TITLE</TITLE>
         </HEAD>
         <BODY>
                <H1>$TITLE</H1>
                <P>$TIME_STAMP</P>
        </BODY>
</HTML>
_EOF_
```
token可以是任意的文本，只要再次出现就会终止，感觉上相当于一个定位标识。
<< 和 <<- 的区别：<<- 的话shell会忽略here文档中Tab字符，就能缩进文档提高可读性。
```shell
[root@localhost ~]# var="myvar"
### 这里的token就是my_EOF_，可以看到后面都是 > 等待输入直到token再次出现终止，输出之前的操作。
[root@localhost ~]# cat << my_EOF_
> $var
> good
> hi
> "hi"
> \tgood morning
> my_EOF_
myvar
good
hi
"hi"
\tgood morning
[root@localhost ~]# 

```
# shell函数
## shell函数的形式
shell函数的语法形式， 形式都是等价的
```shell
### 形式1：
function name {
	commands
  return
}
### 形式2：
name() {
	commands
  return
}
```
shell函数demo
```shell
#！ /bin/bash
# shell function demo
function func1 {
	echo "this is func1"
  return
}
# 这里是main，中间调用了func1函数，直接用函数名字即可
echo "step1"
func1
echo "step3"
```
执行过程
```shell
[root@localhost ~]# vim funcdemo
[root@localhost ~]# chmod 755 funcdemo 
[root@localhost ~]# . funcdemo 
step1
this is func1
step3
[root@localhost ~]# 
```
## shell函数命名方式
shell函数的命名和变量命名规则相同，一个函数必须至少包含一个命名，return虽然是可选的命名，但是可以满足这个条件，即可以在函数体内放一个return，表示返回空。
```shell
[root@localhost ~]# cat funcdemo 
#! /bin/bash
# hell function demo

function func1 {
	return
}
# 这里是main，中间调用了func1函数，直接用函数名字即可
echo "step1"
func1
echo "step3"
[root@localhost ~]# . funcdemo 
step1
step3
[root@localhost ~]# 
```
## 局部变量与全局变量
```shell
#！/bin/bash
# local-vars:script to demonstrate local variables
foo=global #全局变量 foo
funct_1(){
	local foo #使用local定义foo，作用于funct_1内
	foo=local_1
	echo "funct_1:foo=$foo"
  }
funct_2() {
	local foo #使用local定义foo，作用于funct_2内
	foo=local_2
	echo "funct_2:foo=$foo"
	}	
### 引用全局变量
echo "global:foo = $foo"
funct_1
echo "global:foo = $foo"
funct_2
echo "global:foo = $foo"

##############################################
执行结果
[root@localhost ~]# . funcdemo 
global:foo = global
funct_1:foo=local_1
global:foo = global
funct_2:foo=local_2
global:foo = global
[root@localhost ~]# 

```
现在sys_info_page脚本内容
```shell
# 使用here文档的形式输出文本信息
#！/bin/bash
# Program to output a system information page

#声明变量title
TITLE="System Information Report for $HOSTNAME"
CURRENT_TIME=$(date +"%x %r %Z")
TIME_STAMP="Generated $CURRENT_TIME,by $USER"


report_uptime() {
	cat <<- _EOF_
			<H2>System Uptime</H2>
			<PRE>$(uptime)</PRE>
			_EOF_
	return
}

report_disk_space() {
	cat <<- _EOF_
			<H2>Disk Space Utilization</H2>
			<PRE>$(df -h)</PRE>
			_EOF_
	return
}

report_home_space() {
	cat <<- _EOF_
			<H2>Home Space Utilization</H2>
			<PRE>$(du -sh /home/*)</PRE>
			_EOF_
	return
}

cat << _EOF_
<HTML>
         <HEAD>
            <TITLE>$TITLE</TITLE>
         </HEAD>
         <BODY>
                <H1>$TITLE</H1>
                <P>$TIME_STAMP</P>
				$(report_uptime)
				$(report_disk_space)
				$(report_home_space)
        </BODY>
</HTML>
_EOF_

```
执行效果在浏览器上
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1610874724302-b9056423-2358-4f66-94b2-528b4195eb74.png#align=left&display=inline&height=686&margin=%5Bobject%20Object%5D&name=image.png&originHeight=686&originWidth=1324&size=77332&status=done&style=stroke&width=1324)
# 流控制：if 分支语句
## if语句的语法形式
注意[ ]内的空格是必须的。贼坑这点，= 号的空格也是必须的，$var=5 相当于赋值。一定要有空格才是判断
```shell
if commands; then
		commands
[elif commands; then
 				commands....]
[else
		commands]
fi

#### 例子 
#### 注意[ ]内的空格是必须的。贼坑这点，= 号的空格也是必须的，$var=5 相当于赋值。一定要有空格才是判断
var=5
if [ $var = 5 ]; then
	echo "var equals 5"
elif [ $var = 6 ]; then
	echo "var equals 6"
else
	echo "var not equals 5"
fi

###### 执行结果1：直接在命名行出判断
[root@localhost ~]# if [ $var = 5 ]; then
> echo "var equals 5"
> elif [ $var = 6 ]; then
> echo "var equals 6"
> else
> echo "var not equals 5"
> fi
var equals 5
[root@localhost ~]# 
###### 执行结果2：在函数文件里面写好执行
[root@localhost ~]# . funcdemo 
var equals 5
[root@localhost ~]# 
```
## 退出状态
0表示成功，1表示失败；echo $? 表示上一个命令执行的情况。
```shell
[root@localhost ~]# ls test
test
[root@localhost ~]# echo $?
0
[root@localhost ~]# ls test123
ls: 无法访问test123: 没有那个文件或目录
[root@localhost ~]# echo $?
2
[root@localhost ~]# 

```
shell内置了两个命名，true表示命令执行成功，false表示命令执行失败。
```shell
[root@localhost ~]# true
[root@localhost ~]# echo $?
0
[root@localhost ~]# false
[root@localhost ~]# echo $?
1
[root@localhost ~]# 
```
## $? 及其特殊变量
对echo $?和其他特殊变量的一些解释
```shell
1、$# 表示参数个数。
2、$0 是脚本本身的名字。
3、$1 是传递给该shell脚本的第一个参数。
4、$2 是传递给该shell脚本的第二个参数。
5、$@ 表示所有参数，并且所有参数都是独立的。
6、$$ 是脚本运行的当前进程ID号。
7、$? 是显示最后命令的退出状态，0表示没有错误，其他表示有错误。
```
## test命令
该命令经常和if一起使用，test命令会执行各种检查和比较，结果为true返回0退出状态，结果为false返回1退出状态。
语法形式
```shell
#形式1
test expression
#形式2，注意[  ]的空格是必须的。贼坑这点
[ expression ]
```
前面的例子中就用到了 [ ] 来判断  注意 = 号两边的空格一定要有才表示判断，贼坑啊
```shell
# [ ]形式 注意 = 号两边的空格，贼坑啊
if [ $var = 5 ]; then
	echo "var equals 5,$var"
elif [ $var = 6 ]; then
	echo "var equals 6"
else
	echo "var not equals 5"
fi

# test形式 注意 = 号两边的空格，贼坑啊
if test $var = 5 ; then
	echo "var equals 5, var=$var"
elif test $var = 6 ; then
	echo "var equals 6, var=$var"
else
	echo "var not equals 5"
fi
```
### test命令对于文件状态的判断
```shell
表达式							成为true的条件
file1 -ef file2   # file1和file2拥有相同的信息节点编号(这两个文件通过硬链接指向同一个文件)
filel -nt file2   # file1比fle2新
filel -ot file2   # file1比fie2旧
-b file           # 存在并且是一个块(设备)文件
-c file 				  # file存在并且是一个字符(设备)文件
-d file 					# file存在并且是一个目录
-e file 					# file存在
-f file						# file存在并且是一个普通文件
-g file						# file存在并且设置了组ID
-G file						# file存在并且属于有效组ID
-k file 					# file存在并且有"粘滞位( sticky bit)"属性
-L file 					# file存在并且是一个符号链接
-O file						# file存在并且属于有效用户ID
-p file 					# file存在并且是一个命名管道
-r file 					# file存在并且可读(有效用户有可读权限)
-s file 					# file存在并且其长度大于0
-S file						# file存在并且是一个网络套接字
-t fd							# fd是一个定向到终端/从终端定向的文件描述符，可以用来确定标准输入输出/错误
是否被重定向
-u file 					# file存在并且设置了 setuid位
-w file						# file存在并且可写（有效用户拥有可写权限）
-x file						# file存在并且可执行（有效用户拥有执行搜索权限)

### 使用这些判断
#! /bin/bash
# test-file:Evaluate the status of a file
FILE=/root/funcdemo
if [ -e "$FILE" ];then
		if [ -f "$FILE" ];then
					echo "$FILE is a regular file."
		fi
		if [ -d "$FILE" ]; then
					echo "$FILE is a directory."
		fi
		if [ -x "$FILE" ]; then
					echo "$FILE is executable."
		fi
else
		echo "$FILE does not exist."
		#exit 1
fi

### 执行结果
[root@localhost ~]# . funcdemo 
/root/funcdemo is a regular file.
/root/funcdemo is executable.
[root@localhost ~]# 


```
### test命令对于字符串的判断
```shell
表达式						 成为true的条件
string 					  # string不为空
-n string				  # string的长度大于0
-z string				  # string的长度等于0
stringl = string2 # string1和 string2相等.单等号和双等号都可以使用,但是双等号使用的更多,注意空格
string1 == string2 
string1 != string2  # string1和 string2不相等
string1 > string2   # 在排序时, string1在string2之后 ,  > 运算符需要用引号或者转义 \
string1 < string2		# 在排序时, string1在string2之前 ,	 < 运算符需要用引号或者转义 \
```
### test命令对于整数的判断
```shell
表达式
integerl -eq integer2     # integer1和integer2相等
integerl -ne integer2			# integer1和integer2不相等

integerl -lt integer2			# integer1小于 integer2
integerl -le integer2			# integer1小于等于integer2

integerl -gt integer2		  # integer大于 integer2
integerl -ge integer2			# integel大于等于integer2
```
更加现代的判断语法 [[ expression ]]  结果返回true 或者false，注意expression两侧的空格

### 正则表达式在判断中的使用
有一个重要的特点： string1=~regex    如果string1和正则表达式regex匹配，返回true
```shell
if [[ "$var" =~ ^[0-9] ]] ;then echo "var $var is a number" fi  #  ^[0-9] 是一个正则
```
(( )) 也是和[[ ]] 一样的复合命令，用于操作整数
```shell
var1=6
if [[ "$var1" =~ ^[0-9] ]] ;then 
	if (( var1 == 6 )); then
		echo "var is $var"
	fi
fi
```
### 逻辑操作符
组合判断表达
Operation     test命令            [[ ]] and (( ))
AND              -a                         &&
OR                -o                           ||
NOT                !                            !
```shell
#!/bin/bash
# test-integer 3: determine if an integer is within a
# specified range of values
MIN_VAL=1
MAX_VAL=100

INT=50

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
		if [[ INT -ge MIN_VAL && INT -le MAX_VAL ]]; then
			echo "$INT is within $MIN_VAL to $MAX_VAL"
		else
			echo "$INT is out of range"
    fi
else
	echo "INT is not an integer, " >&2
	#exit 1
fi
```
由于test使用的所有表达式和操作符都被shell看做命令参数(不像[[ ]]以及(( ))，因此在bash中有特殊含义的字符,如"<"、">"、"("和")",必须用引号括起来或者进行转义.

test和[[ ]]命令基本上完成相同的功能,那么,哪一个更好呢?
test更为传统(而且也是 POSIX的一部分)，而[[ ]]则是bash特定的，由于test命令的使用更为广泛，因此直到如何使用test更为重要；但是[[ ]]命令显然更有用,而且更容易编码。

另一种方式的分支:
bash还提供了两种可以执行分支的控制运算符。"&&" (AND) 和 "‖" (OR)运算符与[[ ]]复合命令中的逻辑运算符类似
语法如下：
_command1 && command2_
和
_command1 || command2_

理解这两个运算符是非常重要的
对于 "&&" 运算符来说，先执行command1，只有在 command1执行成功时，command2才能够执行
对于 "‖" 运算符来说，先执行 command2，则只有在 command1执行失败时, command2才能够执行
# 读取输入—read
内嵌命令read的作用是读取一行标准输入
```shell
# read语法
read [-option] [variable...]

# option选项解释
-a array					 		# 将输入值从索引为0的位置开始赋给aray
-d delimiter					# 用字符串 delimiter的第一个字符标志输入的结束，而不是新的一行的开始
-e										# 使用Readline处理输入。此命令使用户能使用命令行模式的相同方式编辑输入
-n num							  # 从输入中读取num个字符，而不是一整行
-p prompt							# 使用 prompt字符串提示用户进行输入
-r 										# 原始模式。不能将后斜线字符翻译为转义码
-S										# 保密模式。不在屏幕显示输入的字符。此模式在输入密码和其他机密信息时很有用处
-t seconds						# 超时。在 seconds秒后结束输入。若输入超时，read命令返回一个非0的退出状态
-u fd									# 从文件说明符fd读取输入，而不是从标准输入中读取

```
使用例子
```shell
#! /bin/bash
# read from input
echo -n "please input the number: "
read int
echo "the number you inputed was: $int. "

#### 执行结果
[root@localhost ~]# readscript 
please input the number: 123
the number you inputed was: 123. 
[root@localhost ~]# 
```
read命令输入赋值多个变量
```shell
[root@localhost ~]# readscript 
please input multi numbers:  1 2 3 4 5 
var1 = '1' 
var2 = '2' 
var3 = '3' 
var4 = '4' 
var5 = '5' 
### 少于5个输入数目，剩下的默认给空
[root@localhost ~]# readscript 
please input multi numbers: 1 2
var1 = '1' 
var2 = '2' 
var3 = '' 
var4 = '' 
var5 = '' 
### 多于5个输入数目，会在最后的变量包含所有多出的值
[root@localhost ~]# readscript 
please input multi numbers: 1 2 3 4 5 6 
var1 = '1' 
var2 = '2' 
var3 = '3' 
var4 = '4' 
var5 = '5 6' 
[root@localhost ~]# 

```
## 默认接受参数 $REPLY
read 的默认接收参数是 $REPLY
```shell
# 使用 -p 改变输入提示符
#! /bin/bash
# read from input
read -p "enter one or more values > "
echo "REPLY = $REPLY"


### 执行结果
[root@localhost ~]# readscript 
enter one or more values > 123
REPLY = 123
[root@localhost ~]# 

### 当然也可以自定义自己的接收参数 ，如下readfrom为接收参数
#! /bin/bash
# read from input
read -p "enter one or more values > " readfrom
echo "readfrom = $readfrom"

```
## 使用IFS间隔输入字段
IFS，Internal Field Separator。默认的值包含了空格，制表符，换行符。
IFS是可以自定义的
read命令不可重定向
```shell

#! /bin/bash
#  display the menu demo from input

echo "
Please Select:
	1. Display System Information
	2. Display Disk Space
	3. Display Home Space Utilization
	0. Quit
"

read -p "Enter your selection [0-3] > "

if [[ $REPLY =~ ^[0-3]$ ]]; then
	if [[ $REPLY == 0 ]]; then
		echo "Program Terminated"
		exit
	fi
	if [[ $REPLY == 1 ]]; then
		echo "Hostname: $HOSTNAME"
		uptime
		exit 
	fi
	if [[ $REPLY == 2 ]]; then
		echo "Disk Space"
		df -h
		exit 
	fi		
	if [[ $REPLY == 3 ]]; then
		if [[ $(id -u) -eq 0 ]]; then
			echo "Home Space Utilization(All users)"
			du -sh /home/*
		else	
			echo "Home Space Utilization($USER)"
			du -sh $HOME
		fi	
		exit
	fi
else
	echo "Invailed entry" >&2
	exit 1
fi


### 执行结果
[root@localhost ~]# menudemo 

Please Select:
	1. Display System Information
	2. Display Disk Space
	3. Display Home Space Utilization
	0. Quit

Enter your selection [0-3] > 1
Hostname: localhost.localdomain
 20:44:29 up 5 days, 22:23,  3 users,  load average: 1.65, 1.74, 1.75
[root@localhost ~]# menudemo 

Please Select:
	1. Display System Information
	2. Display Disk Space
	3. Display Home Space Utilization
	0. Quit

Enter your selection [0-3] > 2
Disk Space
文件系统                 容量  已用  可用 已用% 挂载点
devtmpfs                 470M     0  470M    0% /dev
tmpfs                    487M     0  487M    0% /dev/shm
tmpfs                    487M   52M  435M   11% /run
tmpfs                    487M     0  487M    0% /sys/fs/cgroup
/dev/mapper/centos-root   17G   14G  3.3G   81% /
/dev/sda1               1014M  172M  843M   17% /boot
tmpfs                     98M  4.0K   98M    1% /run/user/42
tmpfs                     98M   52K   98M    1% /run/user/1000
/dev/sr0                 4.4G  4.4G     0  100% /run/media/sean/CentOS 7 x86_64
overlay                   17G   14G  3.3G   81% /var/lib/docker/overlay2/2b854f92ff00c818848a7eceed6fe863b22c9d7c9c20d81e3cfa8bc0b9622f91/merged
tmpfs                     98M     0   98M    0% /run/user/0
[root@localhost ~]# menudemo 

Please Select:
	1. Display System Information
	2. Display Disk Space
	3. Display Home Space Utilization
	0. Quit

Enter your selection [0-3] > 3
Home Space Utilization(All users)
166M	/home/sean
[root@localhost ~]#


```
# 关于grep命令
常用于查找各种乱七八糟的东西
```shell
用法: grep [选项]... PATTERN [FILE]...
在每个 FILE 或是标准输入中查找 PATTERN。
默认的 PATTERN 是一个基本正则表达式(缩写为 BRE)。
例如: grep -i 'hello world' menu.h main.c

正则表达式选择与解释:
  -E, --extended-regexp     PATTERN 是一个可扩展的正则表达式(缩写为 ERE)
  -F, --fixed-strings       PATTERN 是一组由断行符分隔的定长字符串。
  -G, --basic-regexp        PATTERN 是一个基本正则表达式(缩写为 BRE)
  -P, --perl-regexp         PATTERN 是一个 Perl 正则表达式
  -e, --regexp=PATTERN      用 PATTERN 来进行匹配操作
  -f, --file=FILE           从 FILE 中取得 PATTERN
  -i, --ignore-case         忽略大小写
  -w, --word-regexp         强制 PATTERN 仅完全匹配字词
  -x, --line-regexp         强制 PATTERN 仅完全匹配一行
  -z, --null-data           一个 0 字节的数据行，但不是空行

Miscellaneous:
  -s, --no-messages         suppress error messages
  -v, --invert-match        select non-matching lines
  -V, --version             display version information and exit
      --help                display this help text and exit

输出控制:
  -m, --max-count=NUM       NUM 次匹配后停止
  -b, --byte-offset         输出的同时打印字节偏移
  -n, --line-number         输出的同时打印行号
      --line-buffered       每行输出清空
  -H, --with-filename       为每一匹配项打印文件名
  -h, --no-filename         输出时不显示文件名前缀
      --label=LABEL         将LABEL 作为标准输入文件名前缀
  -o, --only-matching       show only the part of a line matching PATTERN
  -q, --quiet, --silent     suppress all normal output
      --binary-files=TYPE   assume that binary files are TYPE;
                            TYPE is 'binary', 'text', or 'without-match'
  -a, --text                equivalent to --binary-files=text
  -I                        equivalent to --binary-files=without-match
  -d, --directories=ACTION  how to handle directories;
                            ACTION is 'read', 'recurse', or 'skip'
  -D, --devices=ACTION      how to handle devices, FIFOs and sockets;
                            ACTION is 'read' or 'skip'
  -r, --recursive           like --directories=recurse
  -R, --dereference-recursive
                            likewise, but follow all symlinks
      --include=FILE_PATTERN
                            search only files that match FILE_PATTERN
      --exclude=FILE_PATTERN
                            skip files and directories matching FILE_PATTERN
      --exclude-from=FILE   skip files matching any file pattern from FILE
      --exclude-dir=PATTERN directories that match PATTERN will be skipped.
  -L, --files-without-match print only names of FILEs containing no match
  -l, --files-with-matches  print only names of FILEs containing matches
  -c, --count               print only a count of matching lines per FILE
  -T, --initial-tab         make tabs line up (if needed)
  -Z, --null                print 0 byte after FILE name

文件控制:
  -B, --before-context=NUM  打印以文本起始的NUM 行
  -A, --after-context=NUM   打印以文本结尾的NUM 行
  -C, --context=NUM         打印输出文本NUM 行
  -NUM                      same as --context=NUM
      --group-separator=SEP use SEP as a group separator
      --no-group-separator  use empty string as a group separator
      --color[=WHEN],
      --colour[=WHEN]       use markers to highlight the matching strings;
                            WHEN is 'always', 'never', or 'auto'
  -U, --binary              do not strip CR characters at EOL (MSDOS/Windows)
  -u, --unix-byte-offsets   report offsets as if CRs were not there
                            (MSDOS/Windows)

‘egrep’即‘grep -E’。‘fgrep’即‘grep -F’。
直接使用‘egrep’或是‘fgrep’均已不可行了。
若FILE 为 -，将读取标准输入。不带FILE，读取当前目录，除非命令行中指定了-r 选项。
如果少于两个FILE 参数，就要默认使用-h 参数。
如果有任意行被匹配，那退出状态为 0，否则为 1；
如果有错误产生，且未指定 -q 参数，那退出状态为 2。

```
# 流控制：while 和 until 循环
## while循环
while命令的语法
_while commands; do command ; done_
```shell
#! /bin/bash
# while loops demo

count=1
while [ $count -le 5 ]; do
	echo $count
	count=$(( count + 1 ))
done
echo "Finished"

### 执行结果
[root@localhost ~]# loops
1
2
3
4
5
Finished
[root@localhost ~]# 

```
### 跳出循环
bash中提供了两种用于控制循环内部程序流的内建命令。
break命令立即终止跳出循环，continue命令则会跳过当前循环，进入下一个循环迭代。
```shell
#! /bin/bash
# while loops demo

DELAY=3
while true ; do
	read -p "demo for dead-loop, enter your password> "
	if [[ $REPLY =~ ^[0-9]$ ]]; then
		echo "Passwd is incorrent.try again~"
		sleep $DELAY
		continue
	elif [[ $REPLY == 10 ]]; then
		echo "your has tried too many times, exited~"
		break
	else
		echo "please let your number from 0~10，try again~"
		sleep $DELAY
		continue
	fi
done
	
### 执行结果
[root@localhost ~]# loops
demo for dead-loop, enter your password> 1
Passwd is incorrent.try again~
demo for dead-loop, enter your password> 3
Passwd is incorrent.try again~
demo for dead-loop, enter your password> 6
Passwd is incorrent.try again~
demo for dead-loop, enter your password> 123
please let your number from 0~10，try again~
demo for dead-loop, enter your password> 10
your has tried too many times, exited~
[root@localhost ~]# 

```
## until 循环
while命令终止循环，退出状态不为0；而 until命令则刚好相反。until终止条件是退出状态为0。
```shell
#! /bin/bash
# until loops demo

count=1
# 判断条件和while的相反
until [ $count -gl 5 ]; do
	echo $count
	count=$(( count + 1 ))
done
echo "Finished"

```
done语句后面可以添加重定向操作符
如：循环读取distros.txt 的内容
```shell
#! /bin/bash
# while-read:read lines from a file
while read distro version release; do
	printf "Distro：%s\tVersion：%s\tRelease %s\n" \
	$distro  \
	$version \
  $release
done < distros.txt
```
将标准输入重定向到循环中
```shell
#! /bin/bash
# while-read:read lines from a file
sort -k 1,1, -k 2n distros.txt | while read distro version release; do
	printf "Distro：%s\tVersion：%s\tRelease %s\n" \
	$distro  \
	$version \
  $release
done
```
# 流控制：case 分支语句
case的语法
_case word in_
_[pattern [ | pattern ] ) .. commands  ; ; ] ..._
_esac_
esac结尾符号就很骚气了。逆写case
使用case分支简化上面使用if分支的meno例子
```shell

#! /bin/bash
#  display the menu demo from input

echo "
Please Select:
	1. Display System Information
	2. Display Disk Space
	3. Display Home Space Utilization
	0. Quit
"

read -p "Enter your selection [0-3] > "
case $REPLY in
	0)	echo "Program Terminated"
			exit
      ;;
	1)	echo "Hostname: $HOSTNAME"
			uptime
			exit 
      ;;
	2)	echo "Disk Space"
		  df -h
		  exit 
      ;;

	3)	if [[ $(id -u) -eq 0 ]]; then
				echo "Home Space Utilization(All users)"
				du -sh /home/*
			else	
				echo "Home Space Utilization($USER)"
				du -sh $HOME
			fi
      ;;
	*)	echo "Invailed entry" >&2
			exit 1
      ;;
esac
```
## case的匹配模式
匹配的选项使用 ) 结尾
模式描述 -- 注意一定是 ) 结尾的
a)                 若关键字为a则吻合
[[:alpha:]])    若关键字为单个字母则吻合
???)              若关键字为三个字符则吻合
*.txt)            若关键字以.txt结尾则吻合
*)                与任何关键字吻合.在case命令的最后的一个模式应用此项是个不错的做法,
     可对应所有前模式不吻合的关键字,也就是对应任何可能的无效值
多个组合
```shell
#! /bin/bash
# case-menu: a menu driven system information program
clear
echo "
Please Select
A. Display System Information
B. Display Disk Space
C. Display Home Space Utilization
Q. Quit
"
read -p "Enter selection [A, B,C or Q] >"
case $REPLY in
	q|Q)	echo "Program terminated."
				exit
  			;;
	a|A)	echo "Hostname $HOSTNAME"
				uptime
        ;;
	b|B) df -h
  			;;
	c|C)	if [ $(id -u) -eq 0 ]]; then
						echo "Home Space Utilization (All Users)"
						du -sh /home/*
				else
						echo "Home Space Utilization ($USER)."
						du -sh $HOME
				fi
        ;;
	*)	echo "Invalid entry" >&2
			exit 1
      ;;
esac
```
# 位置参数
## shell的参数扩展
shell提供了一组名为位置参数的变量，用于存储命令行中的关键字变量名分别是 0-9，这种方式叫参数扩展
```shell
#! /bin/bash
# cmd-param: script to view command line parameters

echo "
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"

### 执行结果
[root@localhost ~]# cmd-para 

$0 = /root/bin/cmd-para
$1 = 
$2 = 
$3 = 
$4 = 
$5 = 
$6 = 
$7 = 
$8 = 
$9 = 

[root@localhost ~]# 
[root@localhost ~]# cmd-para a b c d e

$0 = /root/bin/cmd-para
$1 = a
$2 = b
$3 = c
$4 = d
$5 = e
$6 = 
$7 = 
$8 = 
$9 = 

[root@localhost ~]# 

```
变量$0总是会存储命令行显示的第一项数据，也就是所执行程序所在的路径名，上面结果显示的就是说cmd-para这个脚本在 /root/bin/cmd-para 这里
另外可以使用 $# 变量给出命令行参数的数目
```shell
#! /bin/bash
# cmd-param: script to view command line parameters

echo "
number of arguments：$#
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"
### 执行结果

[root@localhost ~]# cmd-para a b c d e

number of arguments：5
$0 = /root/bin/cmd-para
$1 = a
$2 = b
$3 = c
$4 = d
$5 = e
$6 = 
$7 = 
$8 = 
$9 = 

[root@localhost ~]# 

```
## shift—处理大量的实参
shift 命令执行后，所有参数的值都下移一位
```shell

#! /bin/bash

count=1

echo "
the number of arguments： $#
"

while [[ $# -gt 0 ]]; do
	echo "argument $count = $1"
	count=$((count+1))
	shift
done

### 执行结果
[root@localhost ~]# cmd-para a b c d e

the number of arguments： 5

argument 1 = a
argument 2 = b
argument 3 = c
argument 4 = d
argument 5 = e
[root@localhost ~]# ^C
[root@localhost ~]# 

```
shell函数中使用位置参数
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1610979381211-570438ab-ca72-42d3-86ca-996cecd7188a.png#align=left&display=inline&height=211&margin=%5Bobject%20Object%5D&name=image.png&originHeight=296&originWidth=814&size=34288&status=done&style=none&width=579)

## 处理多个位置参数
**特殊的参数 * 和 @**
$* 可扩展为从1开始的位置参数列，当包括在双引号内时，扩展为双引号引用的由全部位置参数构成的字符创，每个位置参数以IFS shell变量的第一个字符（默认空格）间隔开
$@ 可扩展为从1开始的位置参数列，当包括在双引号内时，将每个位置参数扩展为双引号引用的单独单词
```shell
#! /bin/bash
# script to demo $* and $@
print_params() {
	echo "\$1 = $1"
	echo "\$2 = $2"
	echo "\$3 = $3"
	echo "\$4 = $4"
}

pass_params() {
	echo -e "\n" '$* :'; print_params $*
	echo -e "\n" '"$*" :'; print_params "$*"
	echo -e "\n" '$@ :'; print_params $@
	echo -e "\n" '"$@" :'; print_params "$@"

}


pass_params "word" "words with spaces"


###执行结果
[root@localhost ~]# cmd-para

 $* :
$1 = word
$2 = words
$3 = with
$4 = spaces

 "$*" :
$1 = word words with spaces
$2 = 
$3 = 
$4 = 

 $@ :
$1 = word
$2 = words
$3 = with
$4 = spaces

 "$@" :
$1 = word
$2 = words with spaces
$3 = 
$4 = 
[root@localhost ~]# 

```
# 流控制：for 循环
_for varible [in words]; do_
_commands_
_done_
循环都是done结束的，while和until也是done结束
```shell
[root@localhost ~]# for i in a b c d;do echo $i;done
a
b
c
d
[root@localhost ~]# 
### 使用{ } 可以扩展范围
[root@localhost ~]# for i in {a..e};do echo $i;done
a
b
c
d
e
[root@localhost ~]# 

```
for的c语言形式
_for (( expression1; expression2; expression3 )) ;do _
_commands_
_done_
```shell
for (( i=0; i<5; i++ )); do
	echo $i
done
```
# 字符串和数组
## 参数扩展 ParameterExpansion
对于一个变量a, 被定义声明后，使用** $a **形式获取内容，也可以是使用 **${a} **的形式，两个就单单引用该变量a时并没有什么区别，但是如果引用变量后面有接其它字符内容，如：echo $a_abc，那么shell会尝试去获取一个变量名为a_abc的内容，而我们显然不是这个想法。所以此时只能用 ${a}_abc, 这样的话获取的内容就是变量a的内容连接上abc，所以这么看，{ }有种小括号的感觉
例子：
```shell
[root@localhost ~]# a=1
[root@localhost ~]# echo $a
1
[root@localhost ~]# echo ${a}
1
### shell尝试去找变量为a_abc的内容，显然没有。
[root@localhost ~]# echo $a_abc

[root@localhost ~]# echo ${a}_abc
1_abc
[root@localhost ~]# 

```
### 参数扩展的形式
_${parameter:-word}_
_${parameter:=word}_
_
空变量扩展的处理
如果parameter参数没有设定或者空参，则默认是word的值，否则是传入的参数值，其实就是怕传入的参数不存在或者为空的时候对后面的程序有影响，所以需要给一个默认值
```shell
### 定义vr为空
[root@localhost ~]# var=
### 这里其实在判断var，因为此时var是空，所以 echo出来的是default
[root@localhost ~]# echo ${var:-"default"}
default
### 再次输出var还是空
[root@localhost ~]# echo $var

### 赋值var=1
[root@localhost ~]# var=1
### 判断var，此时var=1，echo出来的就是不默认值default，而是实打实的1
[root@localhost ~]# echo ${var:- "default"}
1
[root@localhost ~]# 

```

另外两种形式
_${parameter:?word}  _如果parameter为空或者未指定，这样扩展会导致脚本出错而退出，并且word内容输出到标准错误，如果parameter非空，则扩展结果为parameter值
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1611060863506-33d54eb0-b13d-436c-b248-5e84bfd94c70.png#align=left&display=inline&height=174&margin=%5Bobject%20Object%5D&name=image.png&originHeight=224&originWidth=813&size=36528&status=done&style=stroke&width=633)
_${parameter:=word} _ 如果parameter为空或者未指定，将不产生任何扩展。如果parameter非空，word值取代parameter值
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1611060854203-180d762e-d068-4347-8126-5869be3a0878.png#align=left&display=inline&height=117&margin=%5Bobject%20Object%5D&name=image.png&originHeight=146&originWidth=793&size=26968&status=done&style=stroke&width=638)
返回变量名的扩展
_${!prefix*}_
_${!prefix@}_
列出环境变量中BASH开头的变量
```shell
[root@localhost ~]# echo ${!BASH*}
BASH BASHOPTS BASHPID BASH_ALIASES BASH_ARGC BASH_ARGV BASH_CMDS BASH_COMMAND BASH_COMPLETION_COMPAT_DIR BASH_LINENO BASH_REMATCH BASH_SOURCE BASH_SUBSHELL BASH_VERSINFO BASH_VERSION
[root@localhost ~]# echo ${!BASH@}
BASH BASHOPTS BASHPID BASH_ALIASES BASH_ARGC BASH_ARGV BASH_CMDS BASH_COMMAND BASH_COMPLETION_COMPAT_DIR BASH_LINENO BASH_REMATCH BASH_SOURCE BASH_SUBSHELL BASH_VERSINFO BASH_VERSION
[root@localhost ~]# 

```
## 字符串的操作
_${#parameter}_
_${#parameter:offset}_
_${#parameter:offset:length}_
```shell
[root@localhost ~]# str="this is a long string"
[root@localhost ~]# echo "'$str' is ${#str} chars long"
'this is a long string' is 21 chars long
[root@localhost ~]# echo ${str:5}
is a long string
[root@localhost ~]# echo ${str:2:9}
is is a l
[root@localhost ~]# 

```
## 算术计算和扩展
$(( expression )) expression是一个有效的算术表达式 ，可以是八进制和十六进制，八进制0开头，十六进制0x开头， base#number base进制的number==》 echo$(( 2#11111111 ))

算术操作符号： **表示求幂， 5**3 即是 5x5x5=125
```shell
[root@localhost ~]# echo $(( 5+2 ))
7
[root@localhost ~]# echo $(( 5-2 ))
3
[root@localhost ~]# echo $(( 5*2 ))
10
[root@localhost ~]# echo $(( 5/2 ))
2
[root@localhost ~]# echo $(( 5**2 ))
25
[root@localhost ~]# echo $(( 5%2 ))
1
[root@localhost ~]# echo $(( 5**3 ))
125
[root@localhost ~]#
```

### bc : 一种任意精度计算语言
bc是一个专门的计算器程序，读取一个使用类C语言编写的程序文件，并执行， quit退出
例子脚本
```shell
#! /bin/bash
# for bc program
2+2 

### 执行结果
[root@localhost ~]# vim bin/bc_script 
[root@localhost ~]# bc bin/bc_script 
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
4

eixt
0
exit
0
1=1
(standard_in) 4: syntax error
1+1
2
quit
[root@localhost ~]# bc --help
usage: bc [options] [file ...]
  -h  --help         print this usage and exit
  -i  --interactive  force interactive mode
  -l  --mathlib      use the predefined math routines
  -q  --quiet        don't print initial banner
  -s  --standard     non-standard bc constructs are errors
  -w  --warn         warn about non-standard bc constructs
  -v  --version      print version information and exit
[root@localhost ~]# 
```
## 数组
bash中的数组是一维的
创建数组：a[1]=foo
使用数组元素：echo ${a[1]}
使用declare命令创建数组 ： declare -a array     
数组的赋值
name[subscript]=value
name是数组名 subscript是容量，附多个值 name=(value1, value2....)
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1611063030145-871605f8-9e4e-4fe7-a957-13ac32528079.png#align=left&display=inline&height=93&margin=%5Bobject%20Object%5D&name=image.png&originHeight=142&originWidth=831&size=33115&status=done&style=stroke&width=545)
输出数组的所有内容
使用*和@来访问数组中的每个元素，@用得比较多
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1587784/1611063161504-3dd2d9f7-8d2a-4ffe-9c2d-9234c6b944eb.png#align=left&display=inline&height=317&margin=%5Bobject%20Object%5D&name=image.png&originHeight=460&originWidth=789&size=59384&status=done&style=stroke&width=543)
数组的数目
数组的下标
数组的结尾增加元素
数组的排序操作
数组的删除

