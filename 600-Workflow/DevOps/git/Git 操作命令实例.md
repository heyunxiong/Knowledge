# Git 操作命令实例
> git is a great version control system tool. :)

## Git工作流
![image.png](_assets/Git%20操作命令实例/1638197193314-389c8216-2042-4185-91fb-7c3cc5b7bf2d.png)
## Git的操作场景阶段
### Workspace 工作区
顾名思义，就是进行文件操作的地方，特点有：

-  可以添加文件到git的“监控”(track)中，移除亦可 
-  可以“监控”文件的修改，根据自己的需要进行内容调整 
-  可以进行分支的合并，管理标签等 
### Index、Stage 暂存区
在工作区进行的一系列操作，都会在暂存区有所体现；
通过git status就能看到文件的各种状态，确定好文件的状态后等待着commit，把修改提交到仓库中去
### Local Repository 仓库区（本地仓库）
本地仓库，即可以想象成：自己电脑里面有一个仓库管家帮你监控这这一切
暂存区的操作和修改，最后会commit到仓库中去。
本地仓库保存着文件的各种历史状态，能轻松的查看当前项目文件的改动
### Remote Repository  仓库区（远程仓库）
远程仓库，本质上和本地仓库一样的，只是代码放在了服务器上，别人可以通过服务器下载到你的代码；
大家通过共同维护服务器上的远程仓库，进行协同工作；
远程仓库的代码是通过本地仓库push上去的。也可以从远程clone，fetch、pull到本地；这三个操作还是有区别的，但目的都是从远程来下来，只是针对的使用情况不一样。
## Git 的配置 git config
### 常用配置操作
#### git config --list
显示git配置信息
```shell
# 显示目前的本地配置的全局Git配置（不在任何仓库目录下） git config --list
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
rebase.autosquash=true
http.sslbackend=openssl
http.sslcainfo=D:/Git/mingw64/ssl/certs/ca-bundle.crt
credential.helper=manager
user.name=He Yunxiong
user.email=hyxsean@gmail.com
core.autocrlf=false
filter.lfs.required=true
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process

# 如果在某一个指定的仓库中打开，还会在最后显示当前仓库的配置信息 。如：
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
rebase.autosquash=true
http.sslbackend=openssl
http.sslcainfo=D:/Git/mingw64/ssl/certs/ca-bundle.crt
credential.helper=manager
user.name=He Yunxiong
user.email=xxx@gmail.com
core.autocrlf=false
filter.lfs.required=true
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
core.repositoryformatversion=0  # 开始 - 该仓库test_repo_1自己的配置信息
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true  			# 结束 - 该仓库test_repo_1自己的配置信息
```
#### git config -e
修改git配置信息
```shell

# 打开并编辑全局配置的Git配置文件，适用于所有仓库的配置信息 ： git config -e --global
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ git config -e --global
# 配置文件路径：  "D:/test_workspace/GitTest/test_repo_1/.git/config" [unix] 7L, 130C
[user]
        name = He Yunxiong
        email = hyxsean@gmail.com
[core]
        autocrlf = false
[filter "lfs"]
        required = true
        clean = git-lfs clean -- %f
        smudge = git-lfs smudge -- %f
        process = git-lfs filter-process

# 打开并编辑当前仓库的Git配置文件， git config -e 需要指定一个仓库目录，否则会报错：fatal: not in a git directory
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git config -e 
# 配置文件路径：  "D:/test_workspace/GitTest/test_repo_1/.git/config" [unix] 7L, 130C
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true


# 设置全局提交代码时的用户信息，（全局的，全局的，全局的！），主要是用来标识自己是谁，然后怎么联系到你，毕竟，冤有头债有主！
$ git config --global user.name "He Yunxiong"
$ git config --global user.email "xxx@gmail.com"

# 当然，依旧可以进入到一个指定的仓库中设置对于该仓库特定的提交者信息：
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ cd test_repo_1/

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git config user.name "sean"

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git config user.email "sean@gmail.com"

# 然后可以在该仓库的config信息里面看到刚才添加的
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git config -e
# 配置文件路径：  "D:/test_workspace/GitTest/test_repo_1/.git/config" [unix] 7L, 130C
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[user]
        name = sean
        email = sean@gmail.com
```
## 新建本地代码库
### git init
```shell
# 在当前目录创建新的本地仓库 git init
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ mkdir test_repo_1

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ cd test_repo_1/

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1
$ git init
Initialized empty Git repository in D:/test_workspace/GitTest/test_repo_1/.git/

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls -al
total 4
drwxr-xr-x 1 heyunxiong 197610 0 Oct 12 20:41 ./
drwxr-xr-x 1 heyunxiong 197610 0 Oct 12 20:40 ../
drwxr-xr-x 1 heyunxiong 197610 0 Oct 12 20:41 .git/
```
### git init [project-name]
```shell
# 指定一个目录创建新的本地仓库  git init [project-name] 如： git init test_folder
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ git init test_folder
Initialized empty Git repository in D:/test_workspace/GitTest/test_folder/.git/

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_folder (master)
$ ls -al
total 4
drwxr-xr-x 1 heyunxiong 197610 0 Oct 12 20:44 ./
drwxr-xr-x 1 heyunxiong 197610 0 Oct 12 20:44 ../
drwxr-xr-x 1 heyunxiong 197610 0 Oct 12 20:44 .git/
```
### git clone [romote_repo_url]
```shell
# 通过克隆远程仓库创建本地仓库 git clone [romote_repo_url] 
# 如：git clone https://github.com/iissnan/hexo-theme-next.git ./hexo-theme-next
# 克隆远程仓库到指定的本地hexo-theme-next文件夹中，此时hexo-theme-next也变成了本地仓库, 耐心等待，有时候会抽风。

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ git clone https://github.com/iissnan/hexo-theme-next.git ./hexo-theme-next
Cloning into './hexo-theme-next'...

#  remot-url的形式
## git clone git@github.com/iissnan/hexo-theme-next.git         --SSH协议
## git clone git://github.com/iissnan/hexo-theme-next.git       --GIT协议
## git clone https://github.com/iissnan/hexo-theme-next.git     --HTTPS协议
```
## 添加、删除文件操作
在workspace中创建一个文件，此时文件没有被git跟踪，对于git来说，这就是一个普通的文件。
通过git add 命令把文件纳入到git的“监控”范围内;
### git add
git add 的形式：

- git add [file1] [file2]     ##  添加指定文件到暂存区
- git add . 		            ##   添加所有文件
- git add [dir]                ##   添加指定目录到暂存区，包括子目录
- $ git add -p                ##    添加每个变化前，都会要求确认; 对于同一个文件的多处变化，可以实现分次提交
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ touch test1.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
test1.txt

# 通过 git status 可以查看当前workspace的文件跟踪、修改状态。此时可以看到新创建的文件未被跟踪。
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        test1.txt

nothing added to commit but untracked files present (use "git add" to track)

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add test1.txt

# 通过 git status 再次查看，此时文件被git跟踪，等待下一个commit操作。
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   test1.txt
        
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$

## 比较少用的 git add -p
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add -p test1.txt
No changes.

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add -p
No changes.
```
### git rm

-  git rm --cached [file1]  			 	##  从暂存区中移除跟踪的文件，但是会保留在工作区中。 
-  git mv [file-original] [file-renamed]      ##  在被跟踪的情况下，更改文件名会同步到暂存区 
-  git rm [file1] [file2]                                ##  删除一个或多个文件，同时把删除的操作同步到暂存区 

演示操作：
git rm --cached [file1]
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   test1.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git rm --cached test1.txt
rm 'test1.txt'

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```

git mv [file-original] [file-renamed]
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   test1.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git mv test1.txt test1_rename.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
test1_rename.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   test1_rename.txt
        
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```

git rm [file1] [file2]
注意：要先commit后才能rm，因为第一次add时候只是放到了暂存区；此时直接rm的话，由于缓存区有引用改文件，无法删除，同时抛出：
```shell

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git rm test1_rename.txt
error: the following file has changes staged in the index:
    test1_rename.txt
(use --cached to keep the file, or -f to force removal)
```
演示删除的过程，不过需要先提交到本地仓库先。毕竟你都没有进去别人的仓库里面；人家想删除你也不知道你是谁。
```shell
## 先把一开始创建的文件提交到本地仓库
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit -m "first commit"
[master (root-commit) 4cfc93a] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test1_rename.txt

## 查看此时的状态，干净的
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
nothing to commit, working tree clean

## 删除文件test_rename.txt
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git rm test1_rename.txt
rm 'test1_rename.txt'

## 查看状态，缓存区会有一个删除的动作，需要提交后，本地仓库的文件才会被删除
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    test1_rename.txt

## 提交删除的动作到本地仓库中
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit -m "delete file"
[master 984e01d] delete file
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 test1_rename.txt

## 查看状态，干净的
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
nothing to commit, working tree clean

## 同时工作区的文件也删除了
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```
## 提交修改到本地仓库
### git commit  -m
常见的 git commit 提交修改
git commit -m [message] 				   	  ##  提交所有文件的修改，暂存区到仓库区
git commit [file1] [file2] ... -m [message] 		  ##  提交暂存区的指定文件到仓库区
```shell

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   test1.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit -m "add file test1.txt"
[master 5958e66] add file test1.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test1.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
nothing to commit, working tree clean

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```
### git commit -a
提交时会弹出另外个窗口，工作区自上次commit之后的变化，直接到仓库区
```shell
## git commit -a ## 提交时会弹出另外个窗口，工作区自上次commit之后的变化，直接到仓库区

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit -a
[master 961675c] using commit -a
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test2.txt

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#       new file:   test2.txt
#
```
### git commit -v
提交时会弹出另外一个窗口，显示所有diff信息
```shell
$ git commit -v # 提交时会弹出另外一个窗口，显示所有diff信息

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#       new file:   test3.txt
#
# ------------------------ >8 ------------------------
# Do not modify or remove the line above.
# Everything below it will be ignored.
diff --git a/test3.txt b/test3.txt
new file mode 100644
index 0000000..e69de29
```
### git commit --amend
替代上一次提交
```shell

# 替代上一次提交
# 改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit -m "commit test4.txt"
[master 8ac6d06] commit test4.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test4.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit --amend -m "amend commit massage for test4.txt"
[master a225126] amend commit massage for test4.txt
 Date: Sat Oct 16 10:16:24 2021 +0800
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test4.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ vim test4.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit --amend test4.txt
[master f4111d7] amend commit massage for test4.txt addd new line
 Date: Sat Oct 16 10:16:24 2021 +0800
 1 file changed, 1 insertion(+)
 create mode 100644 test4.txt
```
## 分支branch 操作
### 分支的查看，添加，删除，切换操作
```shell
# 列出所有本地分支
# $ git branch
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch
* master

# 列出所有远程分支，换了一个远程仓库进行演示
# git branch -r
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git branch -r
  origin/HEAD -> origin/master
  origin/master

# 列出所有本地分支和远程分支
# git branch -a
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch -a
* master

# 创建新的本地分支，但依然停留在当前分支
# git branch [branch_name]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch new_branch

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch
* master
  new_branch

# 创建新的本地分支，但切换到新的分支
# git checkout -b [branch_name]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout -b new_branch2
Switched to a new branch 'new_branch2'

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git branch
  master
  new_branch
* new_branch2

# 切换到特定的分支
# git checkout [branch_name]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch
* master
  new_branch
  new_branch2

# 切换到上一个使用的分支
# git checkout -
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch
* master
  new_branch
  new_branch2

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout -
Switched to branch 'new_branch2'

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git branch
  master
  new_branch
* new_branch2

# 删除分支，无法删除当前的分支，需要切换到另外的分支才能删除
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git branch
  master
  new_branch
* new_branch2

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git branch -d new_branch2
error: Cannot delete branch 'new_branch2' checked out at 'D:/test_workspace/GitTest/test_repo_1'

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git branch -d new_branch
Deleted branch new_branch (was f4111d7).

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git branch
  master
* new_branch2

# 删除远程分支
# git push origin --delete [branch-name]
# git branch -dr [remote/branch]
```
### 分支的合并操作
```shell
# 合并指定分支到当前分支
# git merge [branch]
# 演示：在new_branch2 进行操作，然后合并到master上。
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git branch
* master
  new_branch2
  
# 目前master的提交记录是到f4111d79...
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log
commit f4111d790c5a98cd09eff4c380bbe72bff4a20e8 (HEAD -> master, new_branch2)
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 10:16:24 2021 +0800

    amend commit massage for test4.txt
    addd new line

commit 912bbec58a90a215ab2e57477b97f9546e47cff1
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 10:08:25 2021 +0800

    amend massage

commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt

commit 984e01d979cdb0a3310a09502abc798a2f6996d4
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:46 2021 +0800

    delete file

commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit
    
# 切换到new_branch2进行操作
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout new_branch2
Switched to branch 'new_branch2'

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ touch test_merge.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git add .

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git commit -m "test merge"
[new_branch2 585ed8b] test merge
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test_merge.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (new_branch2)
$ git checkout master
Switched to branch 'master'
# 合并new_branch2到master上，此时查看提交log，到585ed8bd....
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git merge new_branch2
Updating f4111d7..585ed8b
Fast-forward
 test_merge.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test_merge.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log
commit 585ed8bdb553d1452bd3af10ceea205417fa04af (HEAD -> master, new_branch2)
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 20:36:40 2021 +0800

    test merge

commit f4111d790c5a98cd09eff4c380bbe72bff4a20e8
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 10:16:24 2021 +0800

    amend commit massage for test4.txt
    addd new line

commit 912bbec58a90a215ab2e57477b97f9546e47cff1
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 10:08:25 2021 +0800

    amend massage

commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt

commit 984e01d979cdb0a3310a09502abc798a2f6996d4
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:46 2021 +0800

    delete file

commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```
### 其他分支操作
```shell
# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]

# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]
```
## 标签
### 标签的查看，增加，删除
```shell
# 列出所有标签
# git tag
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git tag

# 在当前/最近一次的commit上添加tag
# git tag [tag_name]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git tag new_tag

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git tag
new_tag

# 查看特定tag的信息，就是看这个tag被用到了哪些地方，这里因为刚才打了一个tag，所以会在当前提交上，即merger的操作
# git show [tag_name]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git show new_tag
commit 585ed8bdb553d1452bd3af10ceea205417fa04af (HEAD -> master, tag: new_tag, new_branch2)
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 20:36:40 2021 +0800

    test merge

diff --git a/test_merge.txt b/test_merge.txt
new file mode 100644
index 0000000..e69de29

# 在特定的commit上打上tag
# git tag [tag_name] [commit]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git tag first 4cfc93
# 可以看到commit后面带有 (tag: first)
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git show first
commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b (tag: first)
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit

diff --git a/test1_rename.txt b/test1_rename.txt
new file mode 100644
index 0000000..e69de29

# 删除tag
# git tag -d [tag_name]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git tag -d testtag
Deleted tag 'testtag' (was 585ed8b)

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```
### 标签远程操作
```shell
# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```
## 各种查看操作
### git status
```shell
# 显示有变更的文件，会显示工作区，暂存区和仓库区里面的文件改动差别
# git status
# 这里显示了三种情况，t1.txt是已经入库了的，然后又有改动，显示的信息是：modified
# 而 t2.txt 是add到了暂存区的，等待commit，
# t3.txt 尚未被git 跟踪 状态是 untracked
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   t2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   t1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        t3.txt
```
### git log
查看分支版本历史
#### git log
```shell
# 显示当前分支的提交版本历史
# git log
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log
commit 603577c6690fd746493d38da3975fc1754982f77 (HEAD -> master)		# 提交编号ID，一般使用前面的几位就能定位到哪次，
																		# HEAD代表此时在哪个分支上
Author: sean <sean@gmail.com>											# 提交者
Date:   Sat Oct 16 21:27:09 2021 +0800 									# 提交时间

    add t1.txt															# 此次提交的修改信息，即commit -m后面的信息

commit 585ed8bdb553d1452bd3af10ceea205417fa04af (tag: new_tag, new_branch2) # tag表示该次commit被打上了哪些标签
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 20:36:40 2021 +0800

    test merge

########### 省略中间几次的提交，避免过长篇幅 ###########

commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b (tag: first)
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$

# 搜索提交历史，根据关键词
$ git log -S [keyword]

# 显示过去5次提交，并格式化提交信息
# git log -5 --pretty --oneline
$ git log -5 --pretty --oneline
603577c (HEAD -> master) add t1.txt
585ed8b (tag: new_tag, new_branch2) test merge
f4111d7 amend commit massage for test4.txt addd new line
912bbec amend massage
5958e66 add file test1.txt

# 显示所有提交过的用户，按提交次数排序
# git shortlog -sn
$ git shortlog -sn
     7  sean
```
#### git log --stat
```shell

# 显示commit历史，以及每次commit发生变更的文件
# git log --stat
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log --stat
commit 603577c6690fd746493d38da3975fc1754982f77 (HEAD -> master)
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 21:27:09 2021 +0800

    add t1.txt

 t1.txt | 0 												# 变更的文件
 1 file changed, 0 insertions(+), 0 deletions(-)			# 变更的操作是哪中，增删改

commit 585ed8bdb553d1452bd3af10ceea205417fa04af (tag: new_tag, new_branch2)
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 20:36:40 2021 +0800

    test merge

 test_merge.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

commit f4111d790c5a98cd09eff4c380bbe72bff4a20e8
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 10:16:24 2021 +0800

    amend commit massage for test4.txt
    addd new line

 test4.txt | 1 +
 1 file changed, 1 insertion(+)

########### 省略中间几次的提交，避免过长篇幅 ###########

commit 984e01d979cdb0a3310a09502abc798a2f6996d4
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:46 2021 +0800

    delete file

 test1_rename.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b (tag: first)
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit

 test1_rename.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
```
#### git log [tag] HEAD
```shell

# 显示某个commit之后的所有变动，每个commit占据一行
# git log [tag] HEAD --pretty=format:%s
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log HEAD --pretty=format:%s
add t1.txt
test merge
amend commit massage for test4.txt addd new line
amend massage
add file test1.txt
delete file
first commit

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
# git log [tag] HEAD --grep feature
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$  git log HEAD --grep add
commit 603577c6690fd746493d38da3975fc1754982f77 (HEAD -> master)
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 21:27:09 2021 +0800

    add t1.txt

commit f4111d790c5a98cd09eff4c380bbe72bff4a20e8
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 10:16:24 2021 +0800

    amend commit massage for test4.txt
    addd new line

commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt
```
#### git log --follow [file]
查看某个文件的版本历史，修改情况
```shell
# 显示某个文件的版本历史，包括文件改名
# git log --follow [file]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log --follow test1.txt
commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt

# git whatchanged [file]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git whatchanged test1.txt
commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt

:000000 100644 0000000 e69de29 A        test1.txt
```
#### git log -p [file]
```shell
# 显示指定文件相关的每一次diff
# git log -p [file]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log -p test1.txt
commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt

diff --git a/test1.txt b/test1.txt
new file mode 100644
index 0000000..e69de29
```

### git diff

```shell
# 显示指定文件是什么人在什么时间修改过，#blame这个单词就离谱，甩锅小能手
# git blame [file]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git blame t1.txt
6404751f (sean 2021-10-16 22:46:54 +0800 1) new line

# 显示暂存区和工作区的差异
# git diff
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff
diff --git a/t1.txt b/t1.txt
index 86ba82a..28370d8 100644
--- a/t1.txt
+++ b/t1.txt
@@ -1 +1,2 @@
 new line
+hi 													## 在工作区的文件t1.txt添加了 hi 这个改动，尚未add到暂存区


# 显示暂存区和上一个commit的差异
# git diff --cached [file]
## 刚才做了hi这个改动，add到暂存区
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add t1.txt

# 修改的t1.txt 已到暂存区，等待commit
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   t1.txt
        new file:   t2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        t3.txt

# 此时查看暂存区和上一次提交的差别，可以看到，这次新加的 hi 为新的， 上一次coomit并没有
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff --cached t1.txt
diff --git a/t1.txt b/t1.txt
index 86ba82a..28370d8 100644
--- a/t1.txt
+++ b/t1.txt
@@ -1 +1,2 @@
 new line
+hi


# 显示工作区与当前分支最新commit之间的差异
# git diff HEAD
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff HEAD
diff --git a/t1.txt b/t1.txt
index 86ba82a..28370d8 100644
--- a/t1.txt
+++ b/t1.txt
@@ -1 +1,2 @@
 new line
+hi
diff --git a/t2.txt b/t2.txt
new file mode 100644
index 0000000..e69de29


# 显示两次提交之间的差异
# git diff [first-branch]...[second-branch]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff master new_branch2
diff --git a/t1.txt b/t1.txt
deleted file mode 100644
index 86ba82a..0000000
--- a/t1.txt
+++ /dev/null
@@ -1 +0,0 @@
-new line
```
### git show
```shell
# 显示某次提交的元数据和内容变化
# git show [commit]
# 第一次提交ID：4cfc93
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git show  4cfc93
commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b (tag: first)
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit

diff --git a/test1_rename.txt b/test1_rename.txt
new file mode 100644
index 0000000..e69de29


# 显示某次提交发生变化的文件
# git show --name-only [commit]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git show --name-only 4cfc93
commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b (tag: first)
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit

test1_rename.txt


# 显示某次提交时，某个文件的内容
# git show [commit]:[filename]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git show 6404751:t1.txt
new line
```
### 其他查看操作
```shell
# 显示当前分支的最近几次提交
# git reflog
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git reflog
6404751 (HEAD -> master) HEAD@{0}: commit: commit t1.txt
603577c HEAD@{1}: commit: add t1.txt
585ed8b (tag: new_tag, new_branch2) HEAD@{2}: merge new_branch2: Fast-forward
f4111d7 HEAD@{3}: checkout: moving from new_branch2 to master
585ed8b (tag: new_tag, new_branch2) HEAD@{4}: commit: test merge
f4111d7 HEAD@{5}: checkout: moving from master to new_branch2
f4111d7 HEAD@{6}: checkout: moving from new_branch2 to master
f4111d7 HEAD@{7}: checkout: moving from master to new_branch2
f4111d7 HEAD@{8}: checkout: moving from new_branch2 to master
f4111d7 HEAD@{9}: checkout: moving from master to new_branch2
f4111d7 HEAD@{10}: commit (amend): amend commit massage for test4.txt
a225126 HEAD@{11}: commit (amend): amend commit massage for test4.txt
8ac6d06 HEAD@{12}: commit: commit test4.txt
912bbec HEAD@{13}: commit (amend): amend massage
961675c HEAD@{14}: commit: using commit -a
5958e66 HEAD@{15}: commit: add file test1.txt
984e01d HEAD@{16}: commit: delete file
4cfc93a (tag: first) HEAD@{17}: commit (initial): first commit


# 显示今天你写了多少行代码
# git diff --shortstat "@{0 day ago}"
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff --shortstat "@{0 day ago}"
 2 files changed, 1 insertion(+)
```
## 远程同步
### git remote
```shell
# 克隆远程仓库到本地
$ git clone [remote_url] [local_path]

# 显示所有远程仓库
# git remote -v
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git remote -v
origin  https://gitee.com/y_project/RuoYi.git (fetch)
origin  https://gitee.com/y_project/RuoYi.git (push)

# 显示某个远程仓库的信息
# git remote show [remote]
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git remote show origin
* remote origin
  Fetch URL: https://gitee.com/y_project/RuoYi.git
  Push  URL: https://gitee.com/y_project/RuoYi.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (local out of date)

heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$

# 增加一个新的远程仓库
# git remote add [shortname] [url]
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git remote add myremote https://exmaple.com/test.git
# 查看刚才添加的新的远程仓库
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git remote -v
myremote        https://exmaple.com/test.git (fetch)
myremote        https://exmaple.com/test.git (push)
origin  https://gitee.com/y_project/RuoYi.git (fetch)
origin  https://gitee.com/y_project/RuoYi.git (push)

heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$

# 移除一个远程仓库
# git remote remove [remote_name]
# 帮刚添加的myremote删除
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git remote remove myremote

heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git remote -v
origin  https://gitee.com/y_project/RuoYi.git (fetch)
origin  https://gitee.com/y_project/RuoYi.git (push)

heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$
```
### git fetch, git pull, git push
```shell
# 获取远程仓库的所有变动
# git fetch [remote]
heyunxiong@hyx MINGW64 /d/Open_Source/RuoYi_2021/RuoYi (master)
$ git fetch origin
remote: Enumerating objects: 27, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 27 (delta 8), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (27/27), done.
From https://gitee.com/y_project/RuoYi
   0efa0494..51251331  master     -> origin/master

# 取回远程仓库的变化，并与本地分支合并, pull相当于fetch+merge
$ git pull [remote] [branch] 

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突，不建议这么操作。
$ git push [remote] --force

# 推送所有分支到远程仓库
$ git push [remote] --all
```
## 撤销操作
### git checkout
注重恢复整个文件
```shell

# git-checkout - Switch branches or restore working tree files 	##from git help description
# 所以此命令即可切换分支，也可以恢复工作区文件

# 演示案例： 
# 先清空各个区的差异，然后在工作区新加一个文件，add到暂存区，
# 此时删除工作区的文件，最后用checkout把删除的文件从暂存区恢复到工作区

# 恢复暂存区的指定文件到工作区
# git checkout [file]

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ touch file1.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        file1.txt

nothing added to commit but untracked files present (use "git add" to track)

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add .

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ rm file1.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   file1.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    file1.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
t1.txt  t3.txt          test1.txt  test3.txt
t2.txt  test_merge.txt  test2.txt  test4.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout file1.txt
Updated 1 path from the index

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
file1.txt  t2.txt  test_merge.txt  test2.txt  test4.txt
t1.txt     t3.txt  test1.txt       test3.txt

# 恢复暂存区的所有文件到工作区 ，和checkout指定文件的操作同理
# git checkout .
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add file2.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ rm file2.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    file1.txt
        deleted:    file2.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout .
Updated 2 paths from the index

# 恢复某个commit的指定文件到暂存区和工作区
# git checkout [commit] [file]
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ rm test1.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout 020079 test1.txt
Updated 1 path from 64ac81e
```
### git reset
注重重置改动
#### git reset [commit]
重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
演示如下：
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
file1.txt  t1.txt  t3.txt          test1.txt  test3.txt
file2.txt  t2.txt  test_merge.txt  test2.txt  test4.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ rm *

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    file1.txt
        deleted:    file2.txt
        deleted:    t1.txt
        deleted:    t2.txt
        deleted:    t3.txt
        deleted:    test1.txt
        deleted:    test2.txt
        deleted:    test3.txt
        deleted:    test4.txt
        deleted:    test_merge.txt

no changes added to commit (use "git add" and/or "git commit -a")

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add . | git commit -m "delete all"
[master c9f2ead] delete all
 10 files changed, 3 deletions(-)
 delete mode 100644 file1.txt
 delete mode 100644 file2.txt
 delete mode 100644 t1.txt
 delete mode 100644 t2.txt
 delete mode 100644 t3.txt
 delete mode 100644 test1.txt
 delete mode 100644 test2.txt
 delete mode 100644 test3.txt
 delete mode 100644 test4.txt
 delete mode 100644 test_merge.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
nothing to commit, working tree clean

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log --pretty
commit c9f2eadc670269b809c890bac4c7bf037a007090 (HEAD -> master)
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 15:38:35 2021 +0800

    delete all

commit e7e98cd35bd28d7e2dc063cf430de72eb79222a3
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 14:55:37 2021 +0800

    clear workspace

commit 0200792ea50c77d0f3fdf5e5e09de253c345faed
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 13:22:38 2021 +0800

    fo clear working space

############## 省略中间几次commit #############

commit 5958e66bf570e110be9fb48b6c3c35c6feadd8e7
Author: sean <sean@gmail.com>
Date:   Thu Oct 14 20:29:45 2021 +0800

    add file test1.txt

commit 984e01d979cdb0a3310a09502abc798a2f6996d4
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:46 2021 +0800

    delete file

commit 4cfc93a2e29b08eaa8dabccf04c181a5e9e48c1b (tag: first)
Author: sean <sean@gmail.com>
Date:   Wed Oct 13 20:45:19 2021 +0800

    first commit
(END)

### reset 到上一次提交
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git reset e7e98cd
Unstaged changes after reset:
D       file1.txt
D       file2.txt
D       t1.txt
D       t2.txt
D       t3.txt
D       test1.txt
D       test2.txt
D       test3.txt
D       test4.txt
D       test_merge.txt

# 查看status，可以看到刚才删除的文件已经重新回到暂存区了
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    file1.txt
        deleted:    file2.txt
        deleted:    t1.txt
        deleted:    t2.txt
        deleted:    t3.txt
        deleted:    test1.txt
        deleted:    test2.txt
        deleted:    test3.txt
        deleted:    test4.txt
        deleted:    test_merge.txt

no changes added to commit (use "git add" and/or "git commit -a")

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls

# 利用checkout ，把暂存区的文件同步到工作区，就可以看到一开始删除的文件
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git checkout .
Updated 10 paths from the index
# 查看刚才删除的文件。
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
file1.txt  t1.txt  t3.txt          test1.txt  test3.txt
file2.txt  t2.txt  test_merge.txt  test2.txt  test4.txt
```
#### git reset 其他
一定要清楚是哪些地方保持不变，哪些地方有影响。
```shell
# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区所有文件与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]
```
### git revert
git revert [commit]
新建一个commit，用来撤销指定commit
后者（指定的commit）的所有变化都将被前者（新建的commit）抵消，并且应用到当前分支
案例：新建一个文件提交，然后revert这个提交。预期结果：新建文件消失
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ touch file_test.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git add .

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git commit -m "add for test git revert"
[master e7ccf14] add for test git revert
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file_test.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log
commit e7ccf1443878d9054ab46e5cd98cfaf4d655c539 (HEAD -> master)
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 21:39:56 2021 +0800

    add for test git revert

commit e7e98cd35bd28d7e2dc063cf430de72eb79222a3
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 14:55:37 2021 +0800

    clear workspace

commit 0200792ea50c77d0f3fdf5e5e09de253c345faed
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 13:22:38 2021 +0800

    fo clear working space

commit 6404751f30345947b1e55d5de77649d6d06f5a8a
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 22:46:54 2021 +0800

    commit t1.txt
##########省略下面的commit################

# revert指定刚才提交的commit。
# 可以看到是，这次提交的东西覆盖上一次的提交。
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git revert e7ccf144
[master 4e173a7] Revert "add for test git revert"
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 file_test.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git log
commit 4e173a7ab2c52939e008a09c65b76e7bdcfccbe7 (HEAD -> master)
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 21:40:49 2021 +0800

    Revert "add for test git revert"

    This reverts commit e7ccf1443878d9054ab46e5cd98cfaf4d655c539.

commit e7ccf1443878d9054ab46e5cd98cfaf4d655c539
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 21:39:56 2021 +0800

    add for test git revert

commit e7e98cd35bd28d7e2dc063cf430de72eb79222a3
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 14:55:37 2021 +0800

    clear workspace

commit 0200792ea50c77d0f3fdf5e5e09de253c345faed
Author: sean <sean@gmail.com>
Date:   Sun Oct 17 13:22:38 2021 +0800

    fo clear working space

commit 6404751f30345947b1e55d5de77649d6d06f5a8a
Author: sean <sean@gmail.com>
Date:   Sat Oct 16 22:46:54 2021 +0800

    commit t1.txt
##########省略下面的commit################


## revert之后查看状态，一开始新创建的文件file_test.txt 已删除
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
nothing to commit, working tree clean

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ ls
file1.txt  t1.txt  t3.txt          test1.txt  test3.txt
file2.txt  t2.txt  test_merge.txt  test2.txt  test4.txt

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git diff --cached

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```
### git stash
```shell
# 暂时将未提交的变化从暂存区移除
$ git stash
# 把上次从暂存区暂时移除的改动回复过来，就像栈一样，pop出来，只能pop出最近一次的，先入后出
$ git stash pop


# 两个未提交的文件改动
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git stash
Saved working directory and index state WIP on master: 0200792 fo clear working space
## 此时工作区和暂存区都是干净的
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
nothing to commit, working tree clean
## 弹出刚才暂时不提交的改动
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git stash pop
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt

Dropped refs/stash@{0} (29f2ade75f9cb0aa717f4208983dd55c600dc517)

heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt


heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/test_repo_1 (master)
$
```
## 其他操作
### git archive
```shell
# 生成一个可供发布的压缩包
$ git archive
```
## 附录 & 参考
### git 命令操作
基于windows端的操作，但是linux也大同小异的操作。
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest/
$ git
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```
### git config 配置信息操作命令
```shell
heyunxiong@hyx MINGW64 /d/test_workspace/GitTest
$ git config
usage: git config [<options>]

Config file location
    --global              use global config file
    --system              use system config file
    --local               use repository config file
    --worktree            use per-worktree config file
    -f, --file <file>     use given config file
    --blob <blob-id>      read config from given blob object

Action
    --get                 get value: name [value-regex]
    --get-all             get all values: key [value-regex]
    --get-regexp          get values for regexp: name-regex [value-regex]
    --get-urlmatch        get value specific for the URL: section[.var] URL
    --replace-all         replace all matching variables: name value [value_regex]
    --add                 add a new variable: name value
    --unset               remove a variable: name [value-regex]
    --unset-all           remove all matches: name [value-regex]
    --rename-section      rename section: old-name new-name
    --remove-section      remove a section: name
    -l, --list            list all
    -e, --edit            open an editor
    --get-color           find the color configured: slot [default]
    --get-colorbool       find the color setting: slot [stdout-is-tty]

Type
    -t, --type <>         value is given this type
    --bool                value is "true" or "false"
    --int                 value is decimal number
    --bool-or-int         value is --bool or --int
    --path                value is a path (file or directory name)
    --expiry-date         value is an expiry date

Other
    -z, --null            terminate values with NUL byte
    --name-only           show variable names only
    --includes            respect include directives on lookup
    --show-origin         show origin of config (file, standard input, blob, command line)
    --default <value>     with --get, use default value when missing entry
```
### 参考资料
[Git 各种操作命令详细清单](https://blog.csdn.net/zjhred/article/details/104951936)
