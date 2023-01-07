Linux Package Management
# 软件包系统
不同的Linux发行版本用的是不同的软件包系统，互相之间并不兼容。主要用有两种阵营
**Debian的.deb和Red Hat的.rpm**

| 软件包系统 | Linux发行版（部分） |
| --- | --- |
| Debian的deb技术 | Debian、Ubuntu、Xandros |
| Red Hat的rpm技术 | Fedora、CentOS、openSUSE、Red Hat Enterprise Linux |

# 软件包工作方式
## 软件包文件
包文件是组成软件包系统的基本软件单元，它是由组成软件包的文件压缩而成的文件集。一个包可能包含大量的程序以及支持这些程序的数据文件，包文件既包含了安装文件，又包含了有关包自身及其内容的文本说明之类的软件包元数据。此外，许多软件包中还包含了安装软件包前后执行配置任务的安装脚本
## 库
虽然一些软件项目选择自己包装和分销，但如今多数软件包均由发行商或感兴趣的第三方创建。 Linux用户可以从其所使用的 Linux版本的中心库中获得软件包。所谓的中心库，一般包含了成千上万个软件包，而且每一个都是专门为该发行版本建立和维护的。
## 依赖关系
几乎没有一个程序是独立的，程序之间相互依赖彼此完成既定的工作。软件包之间也是有相互依赖的关系。
## 软件包系统命令
高级命令工具，其实主要就是为了解决包之间的依赖关系

| 发行版本 | 低级 | 高级 |
| --- | --- | --- |
| Debian 类 | dpkg | apt-get、aptitude |
| RHEL、CentOS、Fedora | rpm | yum |

# 软件包管理
## 在库里面查找
包搜索命令

- Debian：    1.apt-get update    2.apt-cache search package_name
- Red Hat：   yum search package_name

`#在red hat的yum库中搜索emac文本编辑器`
`yum search emacs  `   
## 安装库中软件包
包安装命令

- Debian：   1.apt-get update    2.apt-get install package_name
- Red Hat：   yum install package_name

`#在Debian的apt元数据库中安装emacs编辑器`
`apt-get update; apt-get install emacs`
## 安装软件包文件中的软件包？
如果软件包并不是从deb库或者yum库中下载的，那就需要用低级命令工具（dpkg、rpm）直接安装，但是要注意的是，此时没有解决依赖问题，缺少依赖关系安装过程中仍然会报错退出

- Debian：  dpkg --install package_file
- Red Hat： rpm -i package_file

`# 安装emacs-22.1-7.fc7-i386.rpm软件包, 该软件包从非库资源网站下载`
`rpm -i emacs-22.1-7.fc7-i386.rpm `
## 删除软件包

- Debian：  apt-get remove package_name
- Red Hat： yum erase package_name

`# 卸载emacs软件包`
`apt-get remove emacs`
## 更新库中的软件包

- Debian：   1.apt-get update    2.apt-get upgrade
- Red Hat：  yum update

`# Debian的更新`
`apt-get update; apt-get upgrade`
## 更新软件包文件中的软件包

- Debian：   dpkg --install package_file
- Red Hat：  rpm -U package_file

`#Red Hat`
`rpm -U emacs-22.1-7.fc7-i386.rpm  `
## 列出已安装软件包

- Debian：   dpkg --list
- Red Hat：  rpm -qa
## 判断软件包是否安装

- Debian：   dpkg --status package_name
- Red Hat：  rpm -q package_name

`dpgk --status emacs`
## 已安装软件包的信息

- Debian：   apt-cache show package_name
- Red Hat：  yum info package_name

`apt-cahce show emacs`
## 某个文件由哪个软件包安装得到
判断某个特定的文件是由哪个软件包负责安装的

- Debian：   dpkg --search file_name
- Red Hat：  rpm -qf file_name

`rpm -qf /usr/bin/vim`

# 小结
Linux发行版本上有着自己维护的库，一般而言使用yum或apt-get就是从库中找到相应的软件包进行安装即可；而对于一些已经自己从别的地方下载的，使用rpm或dpkg的方式进行安装即可，但是不保证其依赖性的问题是否解决，报错依旧会退出。
