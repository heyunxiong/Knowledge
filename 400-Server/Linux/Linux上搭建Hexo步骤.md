# 安装Node.js
![image.png](_assets/Linux上搭建Hexo步骤/1602591768350-690d128e-9850-4b7d-b185-7aa0eece18fe.png)
![image.png](_assets/Linux上搭建Hexo步骤/1602591768374-369fcc4d-047f-4462-b1fc-f0ae49b65662.png)
# 安装git
`yum install git`
[root@localhost ~]# git --version
git version 1.8.3.1
[root@localhost ~]#
配置git信息
//配置基本信息
[root@localhost ~]# git config --global user.name "flymegoc"
[root@localhost ~]# git config --global user.email 343672271@qq.com
//查看配置
[root@localhost ~]# git config --list
user.name=flymegoc
user.email=343672271@qq.com
[root@localhost ~]#
# 安装Hexo
```shell
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
## 修改端口
hexo s -p 80 临时暂用80端口，下次启动hexo又还是4000了。
默认的linux hexo 端口是4000， 去找到node_modules\hexo-server\index.js文件，可以修改默认的port值 为 80
## 永远启动服务
因为关掉远程连接，会关闭服务 , nohup 命令 &;  &表示后台启动
`nohup hexo s -p 80 &`

