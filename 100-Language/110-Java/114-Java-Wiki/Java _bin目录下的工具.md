> java 周边： bin目录下的自带工具介绍

| 工具 | 描述 |
| --- | --- |
| javap | java反编译工具、主要用于根据java字节码文件反汇编为java源代码文件 |
| jcmd | java命令行，用于向正在运行的JVM发送诊断命令请求 |
| jconsole | 图像化用户界面的监测工具，主要用于监测并显示运行于java平台上的应用程序的性能和资源占用等情况 |
| jdeps | 用于分析java class的依赖关系 |
| jdb | java调试工具，主要用于对java应用进行断点调试 |
| jhat | java堆分析工具，用于分析java堆内存中的对象信息 |
| jinfo | java配置信息工具，用于打印指定java进程、核心文件或远程调试服务器的配置信息 |
| jmap | java内存映射工具，主要用于打印指定java进程，核心文件或远程调试服务器的共享对象内存映射或堆内存细节 |
| jmc | java任务控制工具，主要用于hospot jvm的生产时间监测、分析、诊断 |
| jps | jvm进程状态工具，用于显示目标系统上的hotspot jvm的java进程信息 |
| jrunscript | java命令行脚本外壳工具，主要用于解释执行JavaScript、groovy、ruby等脚本语言 |
| jstack | java堆栈跟踪工具、主要用于打印指定java进程、核心文件或远程调试服务器的java线程的堆栈跟踪信息 |
| jstat | jvm统计监测工具，主要用于监测并显示jvm的性能统计信息，包括GC统计信息 |
| jstatd | 一个RMI服务器应用，用于监测hotspot jvm的创建和终止，并提供一个接口，允许远程监测工具附加到运行于本地主机的jvm上 |
| jvisualvm | jvm监测、故障排除、分析工具；以图形化界面的方式提供运行于指定虚拟机的java应用信息 |


Jcmd：		综合工具
jps：		虚拟机进程状况工具
jinfo jstat：	虚拟机统计信息监视工具
jinfo：		Java配置信息工具
jmap：		Java内存映像工具
jhat：		虚拟机堆转储快照分析工具
jstack：		Java堆栈跟踪工具
