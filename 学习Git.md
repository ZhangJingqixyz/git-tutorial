# 1GitHub入门与实践

## 第1章　欢迎来到GitHub的世界

> 讲解GitHub 是什么,以及有哪些革新之处.在开源软件的世界中,
> GitHub 为开发者带来了革命性的社会化编程概念.在这里我们将会接触
> 这一概念,并对其带来的优势与功能进行讲解.

## 第2章　Git的导入

> 要使用GitHub,离不开Git 这一版本管理系统.本章将深入介绍关
> 于Git 的知识,加深各位对Git 的理解,同时说明实际操作的相关流程.

2.4　初始设置
下面我们对本地计算机里安装的Git 进行设置.
● 设置姓名和邮箱地址
首先来设置使用Git 时的姓名和邮箱地址.名字请用英文输入.

```bash
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
```

这个命令,会在“~/.gitconfig”中以如下形式输出设置文件.

```
[user]
    name = Firstname Lastname
    email = your_email@example.com
```

​	想更改这些信息时,可以直接编辑这个设置文件.这里设置的姓名和邮箱地址会用在Git 的提交日志中.由于在GitHub 上公开仓库时,这里的姓名和邮箱地址也会随着提交日志一同被公开,所以请不要使用不便公开的隐私信息.
​	在GitHub 上公开代码后,前来参考的程序员可能来自世界任何地方,所以请不要使用汉字,尽量用英文进行描述.当然,如果您不想使用真名,完全可以使用网络上的昵称.

● 提高命令输出的可读性
顺便一提,将color.ui 设置为auto 可以让命令的输出拥有更高的可
读性.

```bash
$ git config --global color.ui auto
```

“~/.gitconfig”中会增加下面一行.

```
[color]
	ui = auto
```

这样一来,各种命令的输出就会变得更容易分辨.

## 第3章　使用GitHub的前期准备

> 使用GitHub 需要开设账户（免费）,因此我们将按照顺序为您讲解
> 正式使用前需要进行的一系列设置.
> 另外,本章还会讲解包括操作示例在内的,实际在GitHub 上创建
> 仓库并发布代码的相关流程.

**使用前的准备**

**设置SSH Key**

```bash
$ ssh-keygen -t rsa -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key
(/Users/your_user_directory/.ssh/id_rsa): 按回车键
Enter passphrase (empty for no passphrase): 输入密码
Enter same passphrase again: 再次输入密码
```

输入密码后：

```bash
Your identification has been saved in /Users/your_user_directory/.ssh/id_rsa.
Your public key has been saved in /Users/your_user_directory/.ssh/id_rsa.pub.
The key fingerprint is:
fingerprint值 your_email@example.com
The key's randomart image is:
+--[ RSA 2048]----+
| .+ + |
| = o O . |
略
```

id_rsa 文件是私有密钥,id_rsa.pub 是公开密钥.

以下是在本机运行结果：

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ ssh-keygen -t rsa -C "1779418049@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/asus/.ssh/id_rsa):
/c/Users/asus/.ssh/id_rsa already exists.
Overwrite (y/n)? n
```

**添加公共密钥**

在GitHub 中添加公开密钥,今后就可以用私有密钥进行认证了.
点击右上角的账户设定按钮（Account Settings）,选择SSH Keys 菜单.点击Add SSH Key 之后,会出现如图3.2 的输入框.在Title 中输入适当的密钥名称.Key 部分请粘贴id_rsa.pub 文件里的内容.id_rsa.pub的内容可以用如下方法查看.

```bash
$ cat ~/.ssh/id_rsa.pub
ssh-rsa 公开密钥的内容 your_email@example.com

asus@LAPTOP-7HTOEHI1 MINGW64 /e/天翼云盘同步盘/学习/学习Git
$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDAVWdqD4GMzSiNnbDiStTQqQvfG27VPErODJ6P/irjAUlAyfD7a/dNt53w1ctY4XbxAdYkbhS5eLZy3LtRFn/nmgsRzJT5Oy/hUR+uh+k4FEPNes/buKeKFn1+36K9gUuI4IQ9HMamHOicYjiUjyzHLz9ImnJ8CbGrmTyTVMGGGmgOhJnKOIgiSCXFjI1Yu7p83818sBdNQvGXr2RC8BWvfSJhMQMa8Am83tuB5SdHSWD9ngpK6d99lvupe14qmh+lkgBK/LQzPGURuw2H7C++8F7eG1ayG5ffcU/zuWIY/sVJ3ozskFWUF+CbQDzcurB39Yttv6vuI3xPCBIBNOFhnN6HvRueNFqB3mPJiZNt2N23pTEaCPpP2u/oQVU9P2a82tvzUPsJgS/9eLalhXAPhP4TvbnaG6jvNMByHmvfENgX8xrRdXFlUyaSdy2bzrvAvAAecBN6K/ccdd/hEP7k/jp26PAIUtdCOkCuxFSGVjvWDOWscOF954ZEK3J7Cj0= asus@LAPTOP-7HTOEHI1
```

添加成功之后,创建账户时所用的邮箱会接到一封提示“公共密钥添加完成”的邮件.

完成以上设置后,就可以用手中的私人密钥与GitHub 进行认证和通信了.让我们来实际试一试.

```bash
$ ssh -T git@github.com
The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is fingerprint值 .
Are you sure you want to continue connecting (yes/no)? 输入yes
```

出现以下结果：

```bash
Hi hirocastest! You've successfully authenticated， but GitHub does not
provide shell access.
```

在本机：

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi ZhangJingqixyz! You've successfully authenticated， but GitHub does not provide shell access.
```

**创建仓库**

**连接仓库**

Markdown语法资料：https://www.ituring.com.cn/article/775

**公开代码**

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ git clone git@github.com:ZhangJingqixyz/ZhangJingqi.git
Cloning into 'ZhangJingqi'...
remote: Enumerating objects: 9， done.
remote: Counting objects: 100% (9/9)， done.
remote: Compressing objects: 100% (5/5)， done.
remote: Total 9 (delta 0)， reused 6 (delta 0)， pack-reused 0
Receiving objects: 100% (9/9)， done.
```

**编写代码**

这里我们编写一个hello_world.php 文件,用来输出“Hello World!”.

hello_word.php的内容:

```bash
<?php
	echo "Hello World!";
?>
```

由于hello_word.php 还没有添加至Git 仓库,所以显示为Untracked files.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/ZhangJingqi (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello_world.php

nothing added to commit but untracked files present (use "git add" to track)
```

**提交**

将hello_word.php 提交至仓库.这样一来,这个文件就进入了版本管理系统的管理之下.今后的更改管理都交由Git 进行.

```bash
$ git add hello_world.php
$ git commit -m "Add hello world script by php"
[main 54d2725] Add hello world script by php
 1 file changed， 3 insertions(+)
 create mode 100644 hello_world.php
```

通过git add命令将文件加入暂存区A,再通过git commit命令提交.
添加成功后,可以通过git log命令查看提交日志.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/ZhangJingqi (main)
$ git log
commit 54d2725f9984289afd32855119b7af5244305d01 (HEAD -> main)
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 19:37:18 2023 +0800

    Add hello world script by php

commit 4d613982de1f2bcfb7998e0fb61f150ca8030152 (origin/main， origin/HEAD)
Author: 张靖奇 <1779418049@qq.com>
Date:   Wed Oct 26 13:00:53 2022 +0800

    SOURCETREE

commit b3090838a6c1d6c4d410950615e47e7e38270243
Author: 张靖奇 <1779418049@qq.com>
Date:   Wed Oct 26 12:20:56 2022 +0800

    Create canyouseeme.md

    ok today is 10/26

commit 5ff30b2486c5c4f8ca9c3a5cd526f86982ec7519 (origin/dev)
Author: 张靖奇 <111581419+ZhangJingqixyz@users.noreply.github.com>
Date:   Mon Oct 3 19:32:30 2022 +0800

    Initial commit
```

**进行push**

之后只要执行push,GitHub 上的仓库就会被更新.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/ZhangJingqi (main)
$ git push
Enumerating objects: 4， done.
Counting objects: 100% (4/4)， done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2)， done.
Writing objects: 100% (3/3)， 322 bytes | 322.00 KiB/s， done.
Total 3 (delta 1)， reused 0 (delta 0)， pack-reused 0
remote: Resolving deltas: 100% (1/1)， completed with 1 local object.
To github.com:ZhangJingqixyz/ZhangJingqi.git
   4d61398..54d2725  main -> main

```

## 第4章　通过实际操作学习Git

> 在实际操作中学习使用GitHub 时所必需掌握的Git 的基本知识和操作方法.从最基本操作到多人开发时所需的复杂操作,读者都可以随着本章的讲解简单实践一番.

### 4.1　基本操作

#### ● git init——初始化仓库

要使用Git 进行版本管理,必须先初始化仓库.Git 是使用git init命令进行初始化的.请实际建立一个目录并初始化仓库.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ mkdir git-tutorial

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ cd git-tutorial

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial
$ git init
Initialized empty Git repository in D:/Code/Gitcode/GitHub/git-tutorial/.git/
```

#### ● git status——查看仓库的状态

git status命令用于显示Git 仓库的状态.这是一个十分常用的命令,请务必牢记.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

尚没有可提交的内容,就是说当前我们建立的这个仓库中还没有记录任何文件的任何状态.这里,我们建立README.md 文件作为管理对象,为第一次提交做前期准备.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ touch README.md

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

可以看到在Untracked files 中显示了README.md 文件.类似地,
只要对Git 的工作树或仓库进行操作,git status命令的显示结果就
会发生变化.

#### ● git add——向暂存区中添加文件

要想让文件成为Git 仓库的管理对象,就需要用git add命令将其加入暂存区（Stage 或者Index）中.暂存区是提交之前的一个临时区域.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git add README.md

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

#### ● git commit——保存仓库的历史记录

git commit命令可以将当前暂存区中的文件实际保存到仓库的历史记录中.通过这些记录,我们就可以在工作树中复原文件.

**记述一行提交信息：**

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git commit -m "First commit"
[master (root-commit) 8d6ca52] First commit
 1 file changed， 0 insertions(+)， 0 deletions(-)
 create mode 100644 README.md
```

-m 参数后的"First commit"称作提交信息,是对这个提交的概述.

**记述详细提交信息：**

刚才我们只简洁地记述了一行提交信息,如果想要记述得更加详细,请不加-m,直接执行git commit命令.执行后编辑器就会启动,并显示如下结果.

```bash

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored， and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#       new file:   a.txt
#
仅仅是一次尝试

因为我是初学者
~
~
~
~
~
~
~
~
~
~
~
.git/COMMIT_EDITMSG [unix] (20:00 03/01/2023)                          1，0-1 All
<de/Gitcode/GitHub/git-tutorial/.git/COMMIT_EDITMSG" [unix] 8L， 206B



asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git commit
[master dcaf3a5] 仅仅是一次尝试
 1 file changed， 0 insertions(+)， 0 deletions(-)
 create mode 100644 a.txt

```

**查看提交后的状态：**

执行完git commit命令后再来查看当前状态.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git status
On branch master
nothing to commit， working tree clean

```

#### ● git log——查看提交日志

git log命令可以查看以往仓库中提交的日志.包括可以查看什么人在什么时候进行了提交或合并,以及操作前后有怎样的差别.关于合并我们会在后面解说.
我们先来看看刚才的git commit命令是否被记录了.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log
commit dcaf3a57c8964c30d9fc048a9d6be093634dcfa6 (HEAD -> master)
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 20:00:46 2023 +0800

    仅仅是一次尝试

    因为我是初学者

commit 8d6ca5238a1aca06f837d7cae454711455adbda6
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 19:56:27 2023 +0800

    First commit

```

如上图所示,屏幕显示了刚刚的提交操作.commit 栏旁边显示的“dcaf3a……”是指向这个提交的哈希值.Git 的其他命令中,在指向提交时会用到这个哈希值.

Author 栏中显示我们给Git 设置的用户名和邮箱地址.Date 栏中显示提交执行的日期和时间.再往下就是该提交的提交信息.

**只显示提交信息的第一行：**

如果只想让程序显示第一行简述信息,可以在git log命令后加上--pretty=short.这样一来开发人员就能够更轻松地把握多个提交.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log --pretty=short
commit dcaf3a57c8964c30d9fc048a9d6be093634dcfa6 (HEAD -> master)
Author: Jingqi_Zhang <1779418049@qq.com>

    仅仅是一次尝试

commit 8d6ca5238a1aca06f837d7cae454711455adbda6
Author: Jingqi_Zhang <1779418049@qq.com>

    First commit

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log -1
commit dcaf3a57c8964c30d9fc048a9d6be093634dcfa6 (HEAD -> master)
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 20:00:46 2023 +0800

    仅仅是一次尝试

    因为我是初学者

```

**只显示指定目录、文件的日志**

只要在git log命令后加上目录名,便会只显示该目录下的日志.如果加的是文件名,就会只显示与该文件相关的日志.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log README.md
commit 8d6ca5238a1aca06f837d7cae454711455adbda6
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 19:56:27 2023 +0800

    First commit

```

**显示文件的改动**

如果想查看提交所带来的改动,可以加上-p参数,文件的前后差别就会显示在提交信息之后.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log -p
commit dcaf3a57c8964c30d9fc048a9d6be093634dcfa6 (HEAD -> master)
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 20:00:46 2023 +0800

    仅仅是一次尝试

    因为我是初学者

diff --git a/a.txt b/a.txt
new file mode 100644
index 0000000..e69de29

commit 8d6ca5238a1aca06f837d7cae454711455adbda6
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 19:56:27 2023 +0800

    First commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

```

比如,执行下面的命令,就可以只查看README.md 文件的提交日志以及提交前后的差别.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log -p README.md
commit 8d6ca5238a1aca06f837d7cae454711455adbda6
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 19:56:27 2023 +0800

    First commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

```

如上所述,git log命令可以利用多种参数帮助开发者把握以往提交的内容.不必勉强自己一次记下全部参数,每当有想查看的日志就积极去查,慢慢就能得心应手了.

#### ● git diff——查看更改前后的差别

git diff命令可以查看工作树、暂存区、最新提交之间的差别.单从字面上可能很难理解,各位不妨跟着笔者的解说亲手试一试.我们在刚刚提交的README.md 中写点东西.

```bash
# Git教程
```

**查看工作树和暂存区的差别**

执行git diff命令,查看当前工作树与暂存区的差别.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git diff
diff --git a/README.md b/README.md
index e69de29..567b605 100644
--- a/README.md
+++ b/README.md
@@ -0，0 +1 @@
+# Git教程
\ No newline at end of file

```

由于我们尚未用git add命令向暂存区添加任何东西,所以程序只会显示工作树与最新提交状态之间的差别.

用git add命令将README.md 文件加入暂存区.

```
$ git add README.md
```

**查看工作树和最新提交的差别**

如果现在执行git diff命令,由于工作树和暂存区的状态并无差别,结果什么都不会显示.要查看与最新提交的差别,请执行以下命令.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git diff

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git diff HEAD
diff --git a/README.md b/README.md
index e69de29..567b605 100644
--- a/README.md
+++ b/README.md
@@ -0，0 +1 @@
+# Git教程
\ No newline at end of file

```

不妨养成这样一个好习惯：在执行git commit命令之前先执行git diff HEAD命令,查看本次提交与上次提交之间有什么差别,等确认完毕后再进行提交.这里的HEAD 是指向当前分支中最新一次提交的指针.

由于我们刚刚确认过两个提交之间的差别,所以直接运行git commit命令.

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git commit -m "Add index"
[master 29f3425] Add index
 1 file changed， 1 insertion(+)

```

保险起见,我们查看一下提交日志,确认提交是否成功.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log
commit 29f3425df5a7b25e20952f7a8ae995260146d29a (HEAD -> master)
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 20:58:13 2023 +0800

    Add index

commit dcaf3a57c8964c30d9fc048a9d6be093634dcfa6
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 20:00:46 2023 +0800

    仅仅是一次尝试

    因为我是初学者

commit 8d6ca5238a1aca06f837d7cae454711455adbda6
Author: Jingqi_Zhang <1779418049@qq.com>
Date:   Tue Jan 3 19:56:27 2023 +0800

    First commit

```

成功查到了第三个提交.



### 4.2　分支的操作

#### ● git branch——显示分支一览表

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git branch
* master

```

#### ● git checkout -b——创建、切换分支

**切换到feature-A 分支并进行提交**

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git checkout -b feature-A
Switched to a new branch 'feature-A'

```

实际上，连续执行下面两条命令也能收到同样效果。

```bash
$ git branch feature-A
$ git checkout feature-A
```

创建feature-A 分支，并将当前分支切换为feature-A 分支。这时再来查看分支列表，会显示我们处于feature-A 分支下。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (feature-A)
$ git branch
* feature-A
  master

```

下面来实际操作一下。在README.md 文件中添加一行。

```
# Git教程
- feature-A
```

这里我们添加了feature-A 这样一行字母，然后进行提交。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (feature-A)
$ git add README.md

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (feature-A)
$ git commit -m "Add feature-A"
[feature-A 3711c7e] Add feature-A
 1 file changed, 5 insertions(+), 1 deletion(-)

```

**切换到master 分支**

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (feature-A)
$ git checkout master
Switched to branch 'master'

```

**切换回上一个分支**

现在，我们再切换回feature-A 分支。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git checkout -
Switched to branch 'feature-A'

```

#### ● 特性分支

#### ● 主干分支

接下来，我们假设feature-A 已经实现完毕，想要将它合并到主干分支master 中。首先切换到master 分支。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (feature-A)
$ git checkout master
Switched to branch 'master'

```

然后合并feature-A 分支。为了在历史记录中明确记录下本次分支合并，我们需要创建合并提交。因此，在合并时加上--no-ff参数。

```
$ git merge --no-ff feature-A
```

随后编辑器会启动，用于录入合并提交的信息。

```
Merge branch 'feature-A'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
.git/MERGE_MSG [unix] (22:01 25/01/2023)                                1,1 All
<d/Code/Gitcode/GitHub/git-tutorial/.git/MERGE_MSG" [unix] 6L, 251B

```

默认信息中已经包含了是从feature-A 分支合并过来的相关内容，所以可不必做任何更改。将编辑器中显示的内容保存，关闭编辑器，然后就会看到下面的结果。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git merge --no-ff feature-A
Merge made by the 'ort' strategy.
 README.md     | 6 +++++-
 feature-A.txt | 0
 2 files changed, 5 insertions(+), 1 deletion(-)
 create mode 100644 feature-A.txt

```

#### ● git log --graph——以图表形式查看分支

用git log --graph命令进行查看的话，能很清楚地看到特性分支（feature-A）提交的内容已被合并。除此以外，特性分支的创建以及合并也都清楚明了。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git log --graph
*   commit 6dbb81af9552d19178438d596162efb15bd57ce1 (HEAD -> master)
|\  Merge: 29f3425 646ea3e
| | Author: Jingqi_Zhang <1779418049@qq.com>
| | Date:   Wed Jan 25 22:01:47 2023 +0800
| |
| |     Merge branch 'feature-A'
| |
| * commit 646ea3e8736d8ec9f22505d08c7f8aefe1780687 (feature-A)
| | Author: Jingqi_Zhang <1779418049@qq.com>
| | Date:   Wed Jan 25 22:01:04 2023 +0800
| |
| |     2023
| |
| * commit 3711c7e7bad339025cd6ea4b57ff6c7dc0d45760
|/  Author: Jingqi_Zhang <1779418049@qq.com>
|   Date:   Wed Jan 25 21:35:08 2023 +0800
|
|       Add feature-A
|
* commit 29f3425df5a7b25e20952f7a8ae995260146d29a
| Author: Jingqi_Zhang <1779418049@qq.com>
| Date:   Tue Jan 3 20:58:13 2023 +0800
|
|     Add index

```

### 4.3　更改提交的操作

#### ● git reset——回溯历史版本

**回溯到创建feature-A 分支前**

要让仓库的HEAD、暂存区、当前工作树回溯到指定状态，需要用到git rest --hard命令。只要提供目标时间点的哈希值A，就可以完全恢复至该时间点的状态。事不宜迟，让我们执行下面的命令。

```bash
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git reset --hard 29f3425df5a7b25e20952f7a8ae995260146d29a
HEAD is now at 29f3425 Add index

```

**创建fix-B 分支**























### 4.4　推送至远程仓库

### 4.5　从远程仓库获取

### 4.6　帮助大家深入理解Git 的资料

### 4.7　小结



## 第5章　详细解说GitHub的功能

> 本章我们将以图配文,对GitHub 的功能逐一进行讲解,同时还会
> 详细解说其作为源代码查看器的功能,带您领略方便快捷的UI.
> 建议正在使用GitHub 的开发者也读一读本章,您或许会发现一些
> 将来能用到的小技巧.



## 第6章　尝试Pull Request

> Pull Request 是GitHub 的代表功能,本章我们将带您亲自动手体会.
> 请务必参考本书内容试着进行一次Pull Request.



## 第7章　接收Pull Request

> 站在仓库维护方的角度,教您在接到Pull Request 之后应该如何考
> 虑,如何判断,以及该进行哪些操作.



## 第8章　与GitHub相互协作的工具及服务

> 前半部分为您讲解通过CLI 对GitHub 进行操作时所需的hub 命令.
> 另外,在持续集成环境方面,将讲解可与GitHub 结合使用的Travis CI
> 及Jenkins 的构建及设定方法.
> 除此之外,本章还会介绍一些能够与GitHub 共同使用的服务.



## 第9章　使用GitHub的开发流程

> 详细讲解以GitHub 为中心进行开发的GitHub Flow、Git Flow 两个
> 开发流程.从两者共通的团队开发心得到各自开发流程的特征,都可以
> 通过本章的讲解实际动手体会.



## 第10章　将GitHub应用到企业

> 总结在企业中采用GitHub 时需要考虑的问题及一些有用的信息.安
> 全保障、故障信息、事前需要考虑的问题、GitHub Enterprise 的讨论等,
> 这些实际引入GitHub 时需要考虑或者了解的知识将在本章中进行讲解.



## 附录A　支持GitHub的GUI客户端

> 团队中并不是每个人都对CLI 得心应手.因此,我们为读者总结了
> 辅助GitHub 的GUI 客户端的相关知识.



## 附录B　通过Gist轻松实现代码共享

> Gist 能帮助开发者轻松与其他人共享简单的代码示例或日志,我们将
> 在这部分对Gist 进行讲解.利用Gist 可以轻松管理日常的小代码片段.



# 2Git从入门到精通——高见龙

## 一、Git入门

## 二、环境安装

### windows

https://git-scm.com/download/安装后启动git bash

```bash
$ which git
$ git --version
```

检验安装是否成功.

### macOS

https://brew.sh/index_zh-cn.html 下载Homebrew软件,复制网站上的如下代码

```bash
$ /bin/bash -c "
$ (curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

在终端机窗口粘贴运行,安装完成后,在终端机上运行以下指令：

```bash
$ brew install git
```

### Linux

打开终端,输入以下指令：

```bash
$ sudo apt-get install git
```

借由sudo指令临时提高权限顺利完成软件

### 图形界面工具

https://git-scm.com/downloads/guis 

windows/macOS可用GitHub Desktop或者Source Tree 

Linux/Ubuntu操作系统中,可以安装gitk软件

```bash
$ sudo apt-get install gitk
```

## 三、终端机/命令提示符

### 常用命令

| Windows | macOS/Linux | 说明               |
| ------- | ----------- | ------------------ |
| cd      | cd          | 切换目录           |
| cd      | pwd         | 获取当前所在的位置 |
| dir     | ls          | 列出当前的文件列表 |
| mkdir   | mkdir       | 创建新的目录       |
| 无      | touch       | 创建文件           |
| copy    | cp          | 复制文件           |
| move    | mv          | 移动文件           |
| del     | rm          | 删除文件           |
| cls     | clear       | 清除画面上的内容   |

macOs/Linux操作系统中使用：

**1.目录切换及显示**

```bash
# 切换到 /tmp 目录（绝对路径）
$ cd /tmp

# 切换到my_project 目录（相对路径）
$ cd my project

# 往上一层目录移动
$ cd ..

# 切换到使用者的home / project 下的namecards目录
# 这个 "~" 符号表示home目录
$ cd ~/project/namecards/

# 显示当前所在目录
$ pwd
/tmp
```

Windows操作系统中,命令如下：

```powershell
# 切换到D槽的5xruby目录（绝对路径）
C:\> cd D:\5xruby

# 切换到5xruby目录（相对路径）
D:\> cd 5xruby

# 往上一层目录移动
D:\5xruby> cd ..

# 显示当前所在目录
D:\5xruby> cd D:\5xruby
```

**2.文件列表**

Is 命令可列出当前目录下的所有文件及目录.后面接的 -al 参数中,a 是指以小数点开头的件(如.gitignore)也会显示,l则是完整文件的权限、所有者,以及创建、修改的时间.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ ls -al
total 5
drwxr-xr-x 1 asus 197121  0 Jan  4 18:03 ./
drwxr-xr-x 1 asus 197121  0 Jan  3 22:18 ../
drwxr-xr-x 1 asus 197121  0 Jan  3 20:58 .git/
-rw-r--r-- 1 asus 197121 11 Jan  3 20:41 README.md
-rw-r--r-- 1 asus 197121  0 Jan  3 20:00 a.txt
-rw-r--r-- 1 asus 197121  0 Jan  4 18:03 index.html

```

**3.创建文件、目录**

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-
$ touch index.html

```

如果 index.html 文件本来不存在,touch 命令会创建一个名为 idex.html 的空白文件;如果 indexhtml 文件本来就已经存在,则 touch 命令只会改变该文件的最后修改时间,不会改动原本的内容.

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ mkdir demo

```

mkdir 命令会在当前所在目录下创建一个名为 demo 的目录.

**4.文件操作**

复制文件 index.html,并将副本命名为 about.html:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ cp index.html about.html

```

把文件 index.html 更名为 info.html :

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ mv index.html info.html

```

删除文件 index.html :

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ rm index.html

```

删除这个目录中所有的 .html 文档:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ rm *.html

```

在 Windows 操作系统下,则需把 cp、mv 及 rm 命令分别替换为 copy、move 及 del命令.



### 超简明的Vim操作介绍

喜欢用 Vim 而且用习惯的人会觉得它非常好用,但这软件的人门门有点高.限于篇幅这里仅介绍它的基本使用方法,以便可以顺利地输人、存储、退出.

在 Vim 中,主要是通过模式的切换来进行输人、移动光标、选取、复制及粘贴等操作.

模式有两种,即Normal 模式和 Insert 模式,如图 3-3 所示.

![](E:\小米云盘\学习\学习Git\Git从入门到精通_高见龙\第4章 设置git\1672827292314.jpg)

模式说明如下：
(1)Normal 模式又称命令模式,在该模式下无法输人文本,仅能进行复制、粘贴、存储或离开操作.

(2) 输人文本前,需要先按下“i”“a”或“o”中的一个键进入 Insert 模式.其中i表示insert,a 表示 append,而o则表示新建一行并开始输人.

(3)在 Insert 模式下,按下“Esc”键或“Ctrl+[”组合键,可退回至 Normal模式.

(4)在 Normal模式下,按下“:w”键将对文件进行存储,按下“:q”键将关闭文件(若未存储会提示先存储再离开),而按下“:wq”键则是存储完成后直接关闭文件.

Vim 的命令非常多,但就在 Git 中会遇到的状况 (主要是编辑 Commit 信息)来说,上述这些命令已经足够使用.



## 四、GIT设置

### 用户设置

使用 Git 时,首先要做的就是设置用户的 E-mail 信箱及用户名.打开终端机窗口,输人下面两行命令:

```
$ git config --global user.name "Jingqi_Zhang"
$ git config --global user.email "1779418049@qq.com"
```

输人完成后,可以再检查一下当前的设置:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-
$ git config --list
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
http.sslbackend=openssl
http.sslcainfo=D:/N.W.P.U/Git/mingw64/ssl/certs/ca-bundle.crt
core.autocrlf=true
core.fscache=true
core.symlinks=false
pull.rebase=false
credential.helper=manager-core
credential.https://dev.azure.com.usehttppath=true
init.defaultbranch=master
user.name=Jingqi_Zhang

```

**设置文件的保存位置**

不管是通过终端机命令还是图形界面工具完成的设置,所有 Git相关的设置都默认保存在自已账号下的.gitconfig 文件中,所以使用一般的文字编辑器直接手动修改该文件,也会有一样的效果:

"C:\Users\asus\.gitconfig"

### 每个项目设置不同作者

可能有读者注意到了,前面在设置的时候多加了一个 --global参数,其含义是要进行全局(Global)设置.但偶尔也会遇到一些特殊状况,例如,针对特定的项目设置不同的作者(不要问我什么时候需要做这件事),怎么办呢? 可以在对该项目目录进行 Git 设置的时候,加上 --local参数:

```
$ git config --local user.name SherlyS 
$ git config --local user.email sherly@5xruby.tw
```

这样一来,在对这个项目进行操作的时候,就会使用为其特别定制的用户名及 E-mail 来操作离开这个项目后的 Git 操作,还是会使用默认的 Global 设置.

### 其它方便的设置

**更换编辑器**

不过还好,不一定非要用 Vim,可以在终端机执行以下命令:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git config --global core.editor emacs

```

这样就可以把默认的 Vim 编辑器换成 Emacs了.

除了上述两者,还可以使用Sublime Text、Atom或Visual Studio Code等比较现代的文字编辑器.只需先搜索一下怎样从终端机启动这些应用程序,然后就可以用同样方法把Vim更换掉.

如果在操作 Git 的过程中弹出 Vim 这件事情让你很困扰,那么建议搭配图形界面软件使用

**设置缩写**

虽然 Git 命令不长,但有时懒得打那么多字(如 checkout 命令就有 8 个字母),或者有些命令经常会打错(如 status 命令可能会打成 state).遇到这种状况,可以在 Git 中设置一些“缩写”,这样就可以少打几个字.只需在终端机执行以下命令:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git config --global alias.co checkout

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git config --global alias.br branch

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git config --global alias.st status

```

设置之后,只需输入 git co 命令,就可以实现与输入 git checkout 命令一样的效果;输人git st命令,就可以实现与输人 git status 命令一样的效果.

此外,还可以再加人一些参数.例如,每次在查看 log 时,为了看到比较精简的信息,都要输入

git log --oneline --graph 这么长的命令,而改用Alias 设置(如下所示):

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git config --global alias.l "log --oneline --graph"

```

以后只需输入 git l命令,就可以实现与原来的 --oneline --graph 命令一样的效果了

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git l
* 29f3425 (HEAD -> master) Add index
* dcaf3a5 仅仅是一次尝试
* 8d6ca52 First commit

```

甚至可以把格式弄得再复杂一点,把 Commit的人与时间都加进来:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git config --global alias.ls 'log --graph --pretty=format:"%h <%an> %ar %s"'

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-tutorial (master)
$ git ls
* 29f3425 <Jingqi_Zhang> 22 hours ago Add index
* dcaf3a5 <Jingqi_Zhang> 23 hours ago 仅仅是一次尝试
* 8d6ca52 <Jingqi_Zhang> 23 hours ago First commit

```

结尾那个看起来有点复杂的 format 参数就是用于输出 Commit 的个别信息,其含义是执行git help log 后查阅关于 format 有关的段落.用起来会像这样:

这样,即使不使用图形界面工具也可以轻松地查看 log.上面这些 Alias 的设置,也可以直接到~/.gitconfig 中修改:

```
[alias]
co = checkout 
br = branch
st = statusl = log --oneline --graph
ls = log --graph --pretty=format:"%h <%an> %ar %s"
```

虽然只是少输人了几个字母,但长期累积下来,减少的输人量也是很惊人的.



## 五、开始使用GIT

### 新增、初始Repository

**如果是全新的开始**

如果这是你第一次使用 Git,那么就先从创建一个全新的目录开始吧.打开终端机窗口,并试着操作以下命令(命令后面的 # 是说明,不需要输人):

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ mkdir git-practice

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub
$ cd git-practice

asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice
$ git init
Initialized empty Git repository in D:/Code/Gitcode/GitHub/git-practice/.git/
```

在上面的示例中主要做了以下几件事.
(1)使用mkdir 命令创建了 git-practice 目录.
(2)使用cd 命令切换到刚刚创建的 git-practice 目录.
(3)使用git init命令初始化 git-practice 目录,主要目的是让Git开始对这个目录进行版本控制

其中,git init 命令会在 git-practice 目录中创建一个.git 目录,整个Git 的精华都集中在这个目录中了.如果读者有兴趣,可以先看一下这个目录中的内容,不过现在并不打算介绍里面的细节,只是想让读者先体会一下使用 Git 的感觉,在后面的章节中再详细介绍.

如果使用 SourceTree,可以执行 New一 Create Local Repository 命令,如图5-1所示.

**如果是本来就有的目录**



**如果这个目录不想再被Git控制**

其实,Git 的版控很单纯,全都是靠.git 目录在做事.如果这个目录不想被版控,或者只想给客户不含版控记录的内容,只要把.git 目录移除,Git 就对这个目录失去控制权了.

**为什么一直用/tmp目录,其他目录可以吗**

在本书的示例中,经常会在 /tmp 目录下进行练习,那是因为在 macOS 操作系统下,/tmp目录中的内容在下次计算机重启(或宕机)的时候就会全部被清空,所以不需要再手动整理.这算是我在练习时的个人喜好,要使用其他目录也是可以的,但如果是重要的文件,千万不要放在这个目录下.



### 把文件交给Git管控

#### 创建文件后交给Git

**创建文件**

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice (master)
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

```

现在在这个目录中,除了 Git生成的那个.git 隐藏目录外什么都没有,所以提示“nothing to commit”(现在没有内容可以提交).接下来,在这个目录中通过系统命令创建一个内容为“hello.git”的文件,并命名为 welcome.html:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice (master)
$ echo "hello.git" > welcome.html

```

这个步骤使用一般的文本编辑器成由文件管理员来完成都可以,总之在这个目录中创建一个名为 welcome.html 的文件即.接着,再次使用 git status 命今,然后来看一下这个目录的状态：

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice (master)
$ git st
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        welcome.html

nothing added to commit but untracked files present (use "git add" to track)

```

这时的状态与一开始不太一样了.这个welcome.html 文件当前的状态是 Untracked files,即这个文件尚未被加到 Git版控系统中,还未正式被 Git“追踪”,只是刚刚加入这个目录而已.

**把文件交给Git**

既然文件当前的状态是 Untracked,接下来就要把 welcome.html 文件交给 Git,让 Git 开始“追踪”它.使用的命令是 git add,后面加上文件名:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHu
$ git add welcome.html
warning: in the working copy of 'welcome.html'， LFnext time Git touches it

```

在终机执行这个命令不会输出任何结果.如果使用 SourceTree,可以在 wecome.html文件右击,然后选择 Add to index 选项,如图5-6所示.

这样就可以把该文件交给 Git 管控了.再次使用 git status 命令查看当前的状态:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHu
$ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   welcome.html

```

从以上信息可以看出,文件状态已从 Untracked 变成 new file.这表示该文件已经被安置到暂存区(Staging Area),稍后将与其他文件一起被存储到存储库中.

**这个暂存区也称为下标 (Index)**,所以在图 5-6 所示的 Source Tree 快捷菜单中才会显示为 Add to index 字样.为便于理解,本书将统一使用“暂存区”的称谓.至于为什么要有这样的设计,详见5.3节,add 命令看起来很简单,其实能做不少事,详情可参阅5.18节.

如果觉得 git add welcome.html 这样一次只加一个文件有点麻烦,也可以使用万用字元:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice (master)
$ git add *.html

```

这样就可把所有后缀名是.html 的文件全部加到暂存区.如果想要一口气把全部的文件都加到暂存区,可以直接使用 --all 参数:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice (master)
$ git add --all
```

### 如果在git add之后又改动了那个文件的内容该怎么办

设想一下下面这样一种情境.
(1) 新增了一个文件 abc.txt.
(2) 执行 git add abc.txt 命令,把文件加至暂存区.
(3) 编辑 abc.txt 文件.
完成编辑后,可能想要进行 Commit,把刚刚改动的内容保存下来.这是新手很容易犯的错误之一,以为执行 Commit 命令就能把所有的异动都保存下来,事实上这样的想法是不正确的.执行git status 命令,看一下当前的状态:

```
asus@LAPTOP-7HTOEHI1 MINGW64 /d/Code/Gitcode/GitHub/git-practice (master)
$ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   abc.txt
        new file:   welcome.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   abc.txt

```

可以发现,abc.txt 文件变成了两个,这是为什么? 其实步(2)的确把 abc.txt 文件加入暂存区了,但在步骤(3)中又编辑了该文件.对 Git 来说,编辑的内容并没有再次被加入暂存区,所以此时暂存区中的数据还是步骤(2) 中加进来的那个文件.如果确定这个改动是你想要的,那就再使用 git add abc.txt 命令,把 abc.txt 文件加人暂存区.其实,这样的动作会产生一些 unreachable 的边缘对象.这部分算是进阶的内容,有兴趣读者可参阅9.4节.





## 六、使用分支

## 七、修改历史记录

## 八、标签

## 九、其他常见情况及一些冷知识

## 十、远端共同协作——使用GitHub

## 十一、使用Git Flow



> git从入门到精通--高见龙 清华大学出版社





# 3Youtube——懂点Gi

## #02 萌新也看的懂的 Git 基本操作

1. 配置：git config --global uesr.name "zjq"

   git config --global uesr.email "1779418049@qq.com"

   cat ~/.gitconfig

2. 创建一个新的仓库：git init

   ll

   touch README.md

   git status 显示仓库状态

   git add 添加文件到暂存区管理

   git rm --cached README.md

   git add -A 将当前仓库下所有文件提交到版本控制中

   ll -la

   cd .git

   ll

   cat index

   cls

3. git commit -m “add README.md” 提交暂存区文件

   …or create a new repository on the command line

   ```
   echo "# 2022-11-25" >> README.md
   git init
   git add README.md
   git commit -m "first commit"
   git branch -M main
   git remote add origin https://github.com/ZhangJingqixyz/2022-11-25.git
   git push -u origin main
   ```

   …or push an existing repository from the command line

   ```
   git remote add origin https://github.com/ZhangJingqixyz/2022-11-25.git
   git branch -M main
   git push -u origin main
   ```

   git clone https://github.com/ZhangJingqixyz/2022-11-25.git git-demo

   cd git-demo

   ll

   vim README.md

   git push

   ..

   git pull origin main

## #03 Git 中的分支

1. git branch feature1 创建分支

   git branch 查看已有分支

2. git checkout feature1 切换分支

   ll

   touch a.txt

   vi a.txt

   git add a.txt

   git commit -m "add a.txt"

   git branch feature2

   git checkout feature2

   cat a.txt

   git checkout -b feature3 创建并切换分支

   git branch -d feature2 删除分支

   touch b.txt

   vi b.txt

   git add b.txt

   git commit -m "add b.txt"

   git checkout main

   git merge feature3 合并分支

   git push 

   git checkout feature1

   git push origin feature1 上传分支

   git push origin :feature1	删除上传的分支feature1

   git push origin feature1:f1	上传的分支叫f1,本地是feature1



# 4视频同步笔记：狂神聊Git

学习git之前,我们需要先明白一个概念

**版本控制！**

## 版本控制

什么是版本控制

版本控制（Revision control）是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史,方便查看更改历史记录,备份以便恢复以前的版本的软件工程技术.

- 实现跨区域多人协同开发
- 追踪和记载一个或者多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量
- 并行开发、提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担,节省时间,同时降低人为错误

简单说就是用于管理多人协同开发项目的技术.

没有进行版本控制或者版本控制本身缺乏正确的流程管理,在软件开发过程中将会引入很多问题,如软件代码的一致性、软件内容的冗余、软件过程的事物性、软件开发过程中的并发性、软件源代码的安全性,以及软件的整合等问题.

无论是工作还是学习,或者是自己做笔记,都经历过这样一个阶段！我们就迫切需要一个版本控制工具！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0C4qeLxMgoTg9B154ibahsUaibiaV7DgH9GTFQZj3Kyhf5fxrj6G2U5HFg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

多人开发就必须要使用版本控制！

## 常见的版本控制工具

我们学习的东西,一定是当下最流行的！

主流的版本控制器有如下这些：

- **Git**
- **SVN**（Subversion）
- **CVS**（Concurrent Versions System）
- **VSS**（Micorosoft Visual SourceSafe）
- **TFS**（Team Foundation Server）
- Visual Studio Online

版本控制产品非常的多（Perforce、Rational ClearCase、RCS（GNU Revision Control System）、Serena Dimention、SVK、BitKeeper、Monotone、Bazaar、Mercurial、SourceGear Vault）,现在影响力最大且使用最广泛的是Git与SVN

## 版本控制分类

**1、本地版本控制**

记录文件每次的更新,可以对每个版本做一个快照,或是记录补丁文件,适合个人用,如RCS.

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Dg3fHrbPqbNEOMO9GTjFhVaukMZWx54icS7eS2x8A7BEu0VB9ibwEhzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2、集中版本控制  SVN**

所有的版本数据都保存在服务器上,协同开发者从服务器上同步更新或上传自己的修改

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p00V4uLaibxtZI9RLpq7tkSdlWiaF92AVeZ0ib9DicqBkS2poo5u8sEU2mCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

所有的版本数据都存在服务器上,用户的本地只有自己以前所同步的版本,如果不连网的话,用户就看不到历史版本,也无法切换版本验证问题,或在不同分支工作.而且,所有数据都保存在单一的服务器上,有很大的风险这个服务器会损坏,这样就会丢失所有的数据,当然可以定期备份.代表产品：SVN、CVS、VSS

**3、分布式版本控制 	Git**

每个人都拥有全部的代码！安全隐患！

所有版本信息仓库全部同步到本地的每个用户,这样就可以在本地查看所有版本历史,可以离线在本地提交,只需在连网时push到相应的服务器或其他用户那里.由于每个用户那里保存的都是所有的版本数据,只要有一个用户的设备没有问题就可以恢复所有的数据,但这增加了本地存储空间的占用.

不会因为服务器损坏或者网络问题,造成不能工作的情况！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0ev8Q7qXjsTfeSwFexdA4tGjFAiaVEKQzAHdGcINXILKflI2cfk9BiawQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## Git与SVN的主要区别

SVN是集中式版本控制系统,版本库是集中放在中央服务器的,而工作的时候,用的都是自己的电脑,所以首先要从中央服务器得到最新的版本,然后工作,完成工作后,需要把自己做完的活推送到中央服务器.集中式版本控制系统是必须联网才能工作,对网络带宽要求较高.

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0qtEIDr2NG6rOGg1UgDu5c3ffRR8P7FD5D8BPLUEXp0hQoL7qfp3I6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Git是分布式版本控制系统,没有中央服务器,每个人的电脑就是一个完整的版本库,工作的时候不需要联网了,因为版本都在自己电脑上.协同的方法是这样的：比如说自己在电脑上改了文件A,其他人也在电脑上改了文件A,这时,你们两之间只需把各自的修改推送给对方,就可以互相看到对方的修改了.Git可以直接看到更新了哪些代码和文件！

**Git是目前世界上最先进的分布式版本控制系统.**

**
**





聊聊Git的历史

同生活中的许多伟大事物一样,Git 诞生于一个极富纷争大举创新的年代.

Linux 内核开源项目有着为数众广的参与者.绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上(1991－2002年间).到 2002 年,整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码.

Linux社区中存在很多的大佬！破解研究 BitKeeper ！

到了 2005 年,开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束,他们收回了 Linux 内核社区免费使用 BitKeeper 的权力.这就迫使 Linux 开源社区(特别是 Linux 的缔造者 Linus Torvalds)基于使用 BitKeeper 时的经验教训,开发出自己的版本系统.（2周左右！） 也就是后来的 Git！

**Git是目前世界上最先进的分布式版本控制系统.**

Git是免费、开源的,最初Git是为辅助 Linux 内核开发的,来替代 BitKeeper！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0XGLbyFDUiccCsib4L9Vkg7neJVWupfScbrjd7zm7apC8eYTzgQztNAnA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Linux和Git之父李纳斯·托沃兹（Linus Benedic Torvalds）1969、芬兰







## Git环境配置

软件下载

打开 [git官网] https://git-scm.com/,下载git对应操作系统的版本.

所有东西下载慢的话就可以去找镜像！

官网下载太慢,我们可以使用淘宝镜像下载：http://npm.taobao.org/mirrors/git-for-windows/

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0IXktseBR7lpvVF4bibFwiaibnGxkDm0wYicPIiaZxcUe2KuibAHj83MiaWFSQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下载对应的版本即可安装！

安装：无脑下一步即可！安装完毕就可以使用了！



## 启动Git

安装成功后在开始菜单中会有Git项,菜单下有3个程序：任意文件夹下右键也可以看到对应的程序！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0jaiaAfr2pAfWtFX57kGYqR3SlNxDlAZDkCU6IOB1YAicKxHib5yGbv9zQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Git Bash：**Unix与Linux风格的命令行,使用最多,推荐最多

**Git CMD：**Windows风格的命令行

**Git GUI**：图形界面的Git,不建议初学者使用,尽量先熟悉常用命令



## 常用的Linux命令

平时一定要多使用这些基础的命令！

1）、cd : 改变目录.

2）、cd . . 回退到上一个目录,直接cd进入默认目录

3）、pwd : 显示当前所在的目录路径.

4）、ls(ll):  都是列出当前目录中的所有文件,只不过ll(两个ll)列出的内容更为详细.

5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件.

6）、rm:  删除一个文件, rm index.js 就会把index.js文件删除.

7）、mkdir:  新建一个目录,就是新建一个文件夹.

8）、rm -r :  删除一个文件夹, rm -r src 删除src目录

```
rm -rf / 切勿在Linux中尝试！删除电脑中全部文件！
```

9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下.

10）、reset 重新初始化终端/清屏.

11）、clear 清屏.

12）、history 查看命令历史.

13）、help 帮助.

14）、exit 退出.

15）、#表示注释



## Git配置

所有的配置文件,其实都保存在本地！

查看配置 git config -l

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0GJANibs86DwYqoADdgZySGibmafR8p1XBq6ZG3t0J2wSg9icrIVVQo6dQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

查看不同级别的配置文件：

- #查看系统config
- git config --system --list
- 
- #查看当前用户（global）配置
- git config --global  --list

**Git相关的配置文件：**

1）、Git\etc\gitconfig  ：Git 安装目录下的 gitconfig   --system 系统级

2）、C:\Users\Administrator\ .gitconfig   只适用于当前登录用户的配置  --global 全局

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0hcJS0rxj3qoCVvfDKh3WxwQJlSV3P15EIZuejraOwXLdic6NCB8X8oQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里可以直接编辑配置文件,通过命令设置后会响应到这里.



## 设置用户名与邮箱（用户标识,必要）

当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址.这是非常重要的,因为每次Git提交都会使用该信息.它被永远的嵌入到了你的提交中：

- git config --global user.name "kuangshen"  #名称
- git config --global user.email 24736743@qq.com   #邮箱

只需要做一次这个设置,如果你传递了--global 选项,因为Git将总是会使用该信息来处理你在系统中所做的一切操作.如果你希望在一个特定的项目中使用不同的名称或e-mail地址,你可以在该项目中运行该命令而不要--global选项.总之--global为全局配置,不加为某个项目的特定配置.

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0zQZY37q1iaG0n7445X8YgPVvZH5AqyGvT4RgmoyIcZlJWiaLcxyDgSdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)asus@LAPTOP-7HTOEHI1 MINGW64 /d
$ git config --global --list
user.name=zhangjingqi
user.email=1779418049@qq.com
credential.https://gitee.com.provider=generic



## Git基本理论（重要）

> 三个区域

Git本地有三个工作区域：工作目录（Working Directory）、暂存区(Stage/Index)、资源库(Repository或Git Directory).如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域.文件在这四个区域之间的转换关系如下：

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0NJ4L9OPI9ia1MmibpvDd6cSddBdvrlbdEtyEOrh4CKnWVibyfCHa3lzXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- Workspace：工作区,就是你平时存放项目代码的地方
- Index / Stage：暂存区,用于临时存放你的改动,事实上它只是一个文件,保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库）,就是安全存放数据的位置,这里面有你提交到所有版本的数据.其中HEAD指向最新放入仓库的版本
- Remote：远程仓库,托管代码的服务器,可以简单的认为是你项目组中的一台电脑用于远程数据交换

本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0icz6X2aibIgUWzHxtwX8kicPCKpDrsiaPzZk04OlI2bzlydzicBuXTJvLEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- Directory：使用Git管理的一个目录,也就是一个仓库,包含我们的工作空间和Git的管理空间.
- WorkSpace：需要通过Git进行版本控制的目录和文件,这些目录和文件组成了工作空间.
- .git：存放Git管理信息的目录,初始化仓库的时候自动创建.
- Index/Stage：暂存区,或者叫待提交更新区,在提交进入repo之前,我们可以把所有的更新放在暂存区.
- Local Repo：本地仓库,一个存放在本地的版本库；HEAD会只是当前的开发分支（branch）.
- Stash：隐藏,是一个工作状态保存栈,用于保存/恢复WorkSpace中的临时状态.



## 工作流程

git的工作流程一般是这样的：

１、在工作目录中添加、修改文件；zjq.xml

２、将需要进行版本管理的文件放入暂存区域；git add.

３、将暂存区域的文件提交到git仓库.git commit

因此,git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p09iaOhl0dACfLrMwNbDzucGQ30s3HnsiaczfcR6dC9OehicuwibKuHjRlzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



## Git项目搭建

> 创建工作目录与常用指令

工作目录（WorkSpace)一般就是你希望Git帮助你管理的文件夹,可以是你项目的目录,也可以是一个空目录,建议不要有中文.

日常使用只要记住下图6个命令：

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0AII6YVooUzibpibzJnoOHHXUsL3f9DqA4horUibfcpEZ88Oyf2gQQNR6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 本地仓库搭建

创建本地仓库的方法有两种：一种是创建全新的仓库,另一种是克隆远程仓库.

1、创建全新的仓库,需要用GIT管理的项目的根目录执行：初始化git init

- 在当前目录新建一个Git代码库
- $ git init



2、执行后可以看到,仅仅在项目目录多出了一个.git目录,关于版本等的所有信息都在这个目录里面.

> 克隆远程仓库

1、另一种方式是克隆远程目录,由于是将远程服务器上的仓库完全镜像一份至本地！

```
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url] # https://gitee.com/kuangstudy/kuang_livenote.git
```

2、去 gitee 或者 github 上克隆一个测试！

## Git文件操作

> 文件的四种状态

版本控制就是对文件的版本控制,要对文件进行修改、提交等操作,首先要知道文件当前在什么状态,不然可能会提交了现在还不想提交的文件,或者要提交的文件没提交上.

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过`git add` 状态变为`Staged.`
- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为`Modified`. 如果使用`git rm`移出版本库, 则成为`Untracked`文件
- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过`git add`可进入暂存`staged`状态, 使用`git checkout` 则丢弃修改过, 返回到`unmodify`状态, 这个`git checkout`即从库中取出文件, 覆盖当前修改 !
- Staged: 暂存状态. 执行`git commit`则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为`Unmodify`状态. 执行`git reset HEAD filename`取消暂存, 文件状态为`Modified`

> 查看文件状态

上面说文件有4种状态,通过如下命令可以查看到文件的状态：

- #查看指定文件状态
- git status [filename]
- #查看所有文件状态
- git status
- git add .  添加所有文件到暂存区
- git commit -m "消息内容"    提交暂存区中的内容到本地仓库         -m 提交信息

> 忽略文件

有些时候我们不想把某些文件纳入版本控制中,比如数据库文件,临时文件,设计文件等

在主目录下建立".gitignore"文件,此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略.
2. 可以使用Linux通配符.例如：星号（*）代表任意多个字符,问号（？）代表一个字符,方括号（[abc]）代表可选字符范围,大括号（{string1,string2,...}）代表可选的字符串等.
3. 如果名称的最前面有一个感叹号（!）,表示例外规则,将不被忽略.
4. 如果名称的最前面是一个路径分隔符（/）,表示要忽略的文件在此目录下,而子目录中的文件不忽略.
5. 如果名称的最后面是一个路径分隔符（/）,表示要忽略的是此目录下该名称的子目录,而非文件（默认文件或目录都忽略）.

- #为注释
- *.txt       #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
- !lib.txt     #但lib.txt除外
- /temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
- build/       #忽略build/目录下的所有文件
- doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt



## 使用码云

> github 是有墙的,比较慢,在国内的话,我们一般使用 gitee ,公司中有时候会搭建自己的gitlab服务器



1、注册登录码云,完善个人信息

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0ebAqhteskG4GHwD01bX4lXYmxlmMGn8PRqn4aCXfaQdp3SnbBHdibtQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、设置本机绑定SSH公钥,实现免密码登录！（免密码登录,这一步挺重要的,码云是远程仓库,我们是平时工作在本地仓库！)

```
#进入 C:\Users\Administrator\.ssh 目录

#生成公钥 ssh-keygen -t rsa
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0YlK4ibQ0EMs3LmRmdiahpma8ssTQedkhyShNkibTyFBvaZWicicTfNicWQIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3、将公钥信息public key 添加到码云账户中即可！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0I5Zicrm4PEbnox9L5wjCPtPybCyrKI1JOkRWCYIY5zsX4FvI77LXXmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

4、使用码云创建一个自己的仓库！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0FSIwJb9g6Qbp99jY605xdPfh3N4l2rGpD44d6NCcdibankBUL60uODg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

许可证：开源是否可以随意转载,开源但是不能商业使用,不能转载,...  限制！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0S96XfGogNWVqRAexeybT7DXdyQhfcYJ1oEAgaH1RibRU0WZE0eczdxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

克隆到本地！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0PyKfGFd8UHSGIRbVLkXH5icQsgxh6K2RPibYeUER54UzuNVAYsgxXcfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

解决p12中用ssh-key后仍须输入密码的问题
1、使用ssh方式克隆 git clone git@gitee.com:Name/project.git
就是说,在项目克隆/下载处,选择ssh方式的下载地址
2、如果你已经用https方式克隆了仓库,不必删除仓库重新克隆,只需将当前项目中的 .git/config文件中的
url = https://gitee.com/Name/project.git
修改为
url = git@gitee.com:Name/project.git
再次提交就不需要密码了！
有用的话点个赞呗,让更多人看到,我也是被这个问题困扰好久![[笑哭]](https://i0.hdslb.com/bfs/emote/c3043ba94babf824dea03ce500d0e73763bf4f40.png)







## IDEA中集成Git

1、新建项目,绑定git.

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0D8LPGu2SNKXD01IMqDaSkBeP8ibtvnasBYiaReyuZWAl0EjEib8IYf7cQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注意观察idea中的变化

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Cs93BiaOia1Sdk8icdH7vQzPfzIjuoTNYquKzYtrEe5mklhg2b7KOYsow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、修改文件,使用IDEA操作git.

- 添加到暂存区
- commit 提交
- push到远程仓库

3、提交测试

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0tERIszdgLVlUWamyRapfN74aR8XeGFV2OYWiaeR9CkYlfoBefRh2AIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这些都是单个人的操作！

学习的方式最重要！学会学习！我上课的更多时候都是在教大家去学习一种理念和思想（学习方式）

有道无术、术尚可求.有术无道、止于术！

真正的教学,授人以渔！



## 说明：GIT分支

分支在GIT中相对较难,分支就是科幻电影里面的平行宇宙,如果两个平行宇宙互不干扰,那对现在的你也没啥影响.不过,在某个时间点,两个平行宇宙合并了,我们就需要处理一些问题了！

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0BOGzaG4QTc4JXO0hSlwcNtujNzAvxeibSrajLYLCT6otNnHDV9xYWwA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Ayn87woxfepOhSlUj4FQTFUsia4ic0j6aQy4Tz32PRuJ0HSVeGeUzURA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

git分支中常用指令：

```
# 列出所有本地分支git branch
# 列出所有远程分支git branch -r
# 新建一个分支,但依然停留在当前分支git branch [branch-name]
# 新建一个分支,并切换到该分支git checkout -b [branch]
# 合并指定分支到当前分支$ git merge [branch]
# 切换分支 git switch master  或者 git checkout master
# 删除分支$ git branch -d [branch-name]
# 删除远程分支$ git push origin --delete [branch-name]$ git branch -dr [remote/branch]
```

多个分支如果并行执行,就会导致我们代码不冲突,也就是同时存在多个版本！

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！









IDEA中操作

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0wHNIYeTHC8aHGASoDyZO64QicslqiaMb1OJ1Z1LPoic3LBGyDIYBa7XXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



master主分支应该非常稳定,用来发布新版本,一般情况下不允许在上面工作,工作一般情况下在新建的dev分支上工作,工作完后,比如上要发布,或者说dev分支代码稳定后可以合并到主分支master上来.

![image-20220823205919587](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220823205919587.png)

作业练习：找一个小伙伴,一起搭建一个远程仓库,来练习Git！

1、不要把Git想的很难,工作中多练习使用就自然而然的会了！

2、Git的学习也十分多,看完我的Git教程之后,可以多去思考,总结到自己博客！

> https://www.bilibili.com/video/BV1FE411P7B3?p=11&spm_id_from=pageDriver&vd_source=6bd00cd6e54940a78de98ff9856e72e0
>
> https://mp.weixin.qq.com/s/Bf7uVhGiu47uOELjmC5uXQ











# 5Youtube视频（前面几项只剩两项的时候再看）



# 6Markdown



