
展示了git merge和git rebase的操作区别

```sh

heyunxiong@hyx MINGW64 /d/GitRepos
$ git init ./rebase-demo
Initialized empty Git repository in D:/GitRepos/rebase-demo/.git/

heyunxiong@hyx MINGW64 /d/GitRepos
$ cd rebase-demo/

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ ls

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git branch

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git branch -a

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git log
fatal: your current branch 'master' does not have any commits yet

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ touch file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ touch file2.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git add .

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git commit -m "add files from mater"
[master (root-commit) 148d8fd] add files from mater
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1.txt
 create mode 100644 file2.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git log
commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c (HEAD -> master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git branch
* master

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout -b feature1
Switched to a new branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ ls
file1.txt  file2.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ touch file3.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git status
On branch feature1
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        file3.txt

nothing added to commit but untracked files present (use "git add" to track)

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git add .

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit -m "add file3 from feature1"
[feature1 2bf839e] add file3 from feature1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file3.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82 (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c (master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log -h
usage: git log [<options>] [<revision-range>] [[--] <path>...]
   or: git show [<options>] <object>...

    -q, --quiet           suppress diff output
    --source              show source
    --use-mailmap         Use mail map file
    --decorate-refs <pattern>
                          only decorate refs that match <pattern>
    --decorate-refs-exclude <pattern>
                          do not decorate refs that match <pattern>
    --decorate[=...]      decorate options
    -L <n,m:file>         Process line range n,m in file, counting from 1


heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log -q
commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82 (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c (master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkou master
git: 'checkou' is not a git command. See 'git --help'.

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ touch file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git add .

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git commit -m "add file4 from master"
[master d9889fc] add file4 from master
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout feature1
Switched to branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82 (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git merge master
Merge made by the 'recursive' strategy.
 file4.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit d19cde7bf8470ae98c535cceb371abc41f10630c (HEAD -> feature1)
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730 (master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git diff master
diff --git a/file3.txt b/file3.txt
new file mode 100644
index 0000000..e69de29

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ ls
file1.txt  file2.txt  file3.txt  file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ ls
file1.txt  file2.txt  file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git merge feature1
Updating d9889fc..d19cde7
Fast-forward
 file3.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file3.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git log
commit d19cde7bf8470ae98c535cceb371abc41f10630c (HEAD -> master, feature1)
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ ls
file1.txt  file2.txt  file3.txt  file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ #开始测试rebase

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout feature1
Switched to branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ ls
file1.txt  file2.txt  file3.txt  file4.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ touch file5.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git add .

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit "add file5 from feature1"
error: pathspec 'add file5 from feature1' did not match any file(s) known to git

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit -m "add file5 from feature1"
[feature1 d32406d] add file5 from feature1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file5.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ touch file6.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git add .

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git commit -m "add file6.txt from master"
[master acb8520] add file6.txt from master
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file6.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout feature1
Switched to branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit d32406dbeeda96aa6bd1cdecb9bb86da46a6b834 (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git log
commit acb85202cc2576f3db41494835ea8b6b78f52651 (HEAD -> master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout feature1
Switched to branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: add file5 from feature1

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit 8a3658dac0265d3e8fb63f436a02fde96f146d57 (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit acb85202cc2576f3db41494835ea8b6b78f52651 (master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git status
On branch feature1
nothing to commit, working tree clean

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git rebase feature1
First, rewinding head to replay your work on top of it...
Fast-forwarded master to feature1.

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git log
commit 8a3658dac0265d3e8fb63f436a02fde96f146d57 (HEAD -> master, feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit acb85202cc2576f3db41494835ea8b6b78f52651
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$

```



rebase的冲突例子
```sh

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout feature1
Switched to branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ ls
file1.txt  file2.txt  file3.txt  file4.txt  file5.txt  file6.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ vim file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git status
On branch feature1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit -m "change file1 from master"
On branch feature1
Changes not staged for commit:
        modified:   file1.txt

no changes added to commit

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit -am "change file1 from master"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[feature1 647c844] change file1 from master
 1 file changed, 1 insertion(+)

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ vim file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit --amend --message = "change file1 from feature1"
error: pathspec 'change file1 from feature1' did not match any file(s) known to git

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git commit --amend --message="change file1 from feature1"
[feature1 9119e03] change file1 from feature1
 Date: Sun Jul 31 14:06:24 2022 +0800
 1 file changed, 1 insertion(+)

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit 9119e03a26e7face62d39cb8ba3bb5f60a1d1b9e (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:06:24 2022 +0800

    change file1 from feature1

commit 8a3658dac0265d3e8fb63f436a02fde96f146d57 (master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit acb85202cc2576f3db41494835ea8b6b78f52651
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ vim file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git commit -am "change file1 from master"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[master 5097267] change file1 from master
 1 file changed, 1 insertion(+)

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git checkout feature1
Switched to branch 'feature1'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: change file1 from feature1
Using index info to reconstruct a base tree...
M       file1.txt
Falling back to patching base and 3-way merge...
Auto-merging file1.txt
CONFLICT (content): Merge conflict in file1.txt
error: Failed to merge in the changes.
hint: Use 'git am --show-current-patch' to see the failed patch
Patch failed at 0001 change file1 from feature1
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ ls
file1.txt  file2.txt  file3.txt  file4.txt  file5.txt  file6.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git am --show-current-patch
commit 9119e03a26e7face62d39cb8ba3bb5f60a1d1b9e (feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:06:24 2022 +0800

    change file1 from feature1

diff --git a/file1.txt b/file1.txt
index e69de29..7e1841f 100644
--- a/file1.txt
+++ b/file1.txt
@@ -0,0 +1 @@
+change from feature1

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git log
commit 509726756d7e87972d60e95811df4abd026d3038 (HEAD, master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:09:31 2022 +0800

    change file1 from master

commit 8a3658dac0265d3e8fb63f436a02fde96f146d57
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit acb85202cc2576f3db41494835ea8b6b78f52651
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ vi file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git rebase --continue
file1.txt: needs merge
You must edit all merge conflicts and then
mark them as resolved using git add

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git status
rebase in progress; onto 5097267
You are currently rebasing branch 'feature1' on '5097267'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

        both modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git add .

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git commit "fix rebase conflict"
error: pathspec 'fix rebase conflict' did not match any file(s) known to git

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1|REBASE 1/1)
$ git rebase --continue
Applying: change file1 from feature1

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git log
commit 0181a0ebafb1a6fa385bcef987abe650feecd039 (HEAD -> feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:06:24 2022 +0800

    change file1 from feature1

commit 509726756d7e87972d60e95811df4abd026d3038 (master)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:09:31 2022 +0800

    change file1 from master

commit 8a3658dac0265d3e8fb63f436a02fde96f146d57
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit acb85202cc2576f3db41494835ea8b6b78f52651
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ vim file1

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ ls
file1.txt  file2.txt  file3.txt  file4.txt  file5.txt  file6.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ vim file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (feature1)
$ git checkout master
Switched to branch 'master'

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ vim file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git rebase feature1
First, rewinding head to replay your work on top of it...
Fast-forwarded master to feature1.

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ vim file1.txt

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$ git log
commit 0181a0ebafb1a6fa385bcef987abe650feecd039 (HEAD -> master, feature1)
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:06:24 2022 +0800

    change file1 from feature1

commit 509726756d7e87972d60e95811df4abd026d3038
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 14:09:31 2022 +0800

    change file1 from master

commit 8a3658dac0265d3e8fb63f436a02fde96f146d57
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:13 2022 +0800

    add file5 from feature1

commit acb85202cc2576f3db41494835ea8b6b78f52651
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:48:50 2022 +0800

    add file6.txt from master

commit d19cde7bf8470ae98c535cceb371abc41f10630c
Merge: 2bf839e d9889fc
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:43:32 2022 +0800

    Merge branch 'master' into feature1

commit d9889fc369118f6fd84e3ef3a6717cfe02dab730
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:42:56 2022 +0800

    add file4 from master

commit 2bf839e7355b67c5d08c5bd042ca27fe64c76f82
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:41:32 2022 +0800

    add file3 from feature1

commit 148d8fd2857a0aa23b2f37d7b9e0d09c90ac313c
Author: He Yunxiong <hyxsean@gmail.com>
Date:   Sun Jul 31 13:40:21 2022 +0800

    add files from mater

heyunxiong@hyx MINGW64 /d/GitRepos/rebase-demo (master)
$

```
