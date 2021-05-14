---
title: git
date: 2017/7/14 15:01:39
tags: 
	- Git
categories: 
	- Command
	- Git
---

### 安装 Git

Linux 上使用如下命令安装

```
$ sudo apt-get install git
```

Mac OS 上可以使用 HomeBrew 安装，命令如下

```
$ brew install git
```

安装完成后，需要设置用户名和邮箱

```
$ git config --global user.name <your name>
$ git config --global user.email <email@example.com>
```

注意，使用 `--global` 参数后，表示你这台机器上所有的 Git 仓库都会使用这个配置，你也可以为某个仓库指定不同的用户名和邮箱

<!-- more -->

### 初始化本地仓库

进入项目目录后

```
$ git init
```

创建完成后当前目录下会多出一个 `.git` 的目录，这个目录是用来跟踪管理版本库的，千万不要手动修改这个目录里面的文件

### 查看本地文件状态

```
$ git status
```

`git status` 命令可以让我们随时查看本地仓库的当前状态。

```
$ git diff
```

`diff` 顾名思义就是 `difference` ，可以查看某文件先后作了什么修改

### 添加文件到仓库

使用以下命令可以指定文件添加到暂存区

```
$ git add <name>
```

如果将输入名称的位置用 `.` 代替，则会添加当前目录下所有有改动的文件（包括新建和删除）到暂存区

```
$ git add .
```

提交到仓库

```
$ git commit -m "commit info"
```

在 `-m` 参数后面添加本次提交信息的概要，可以帮助自己或他们理解本次提交作了什么工作

### 版本回退

使用 `git log` 命令可以查看提示历史，例如

```
$ git log
commit 1741e2b6b792f88f4da47905409e1ced7bf4214a
Author: 39 <admin@aixieluo.com>
Date:   Sun Jul 16 15:42:40 2017 +0800

    创建 Demo Repository 和 Interface

commit 2c933d4ab6813030699fc4f0209e0ddfebbee7fa
Author: 39 <admin@aixieluo.com>
Date:   Fri Jul 14 17:23:35 2017 +0800

    创建 study 项目
```

`git log` 命令显示从近到远的提交日志，我们可以看到 2 次提交 “创建 study 项目”、“创建 Demo Repository 和 Interface”，如果不想显示太多信息，可以使用 `--pretty=oneline`

```
$ git log --pretty=oneline
1741e2b6b792f88f4da47905409e1ced7bf4214a 创建 Demo Repository 和 Interface
2c933d4ab6813030699fc4f0209e0ddfebbee7fa 创建 study 项目
```

如例子中显示的 `2c933...e7fa` 这串字符串是 `commit id` （即版本号）

当我们需要回到第一个版本时，可以使用 `git reset` 命令

```
$ git reset --hard HEAD^
```

用 `HEAD` 表示当前版本的话，那上个版本就是 `HEAD^` ，上上个版本就是 `HEAD^^` ， 如果是 39 个版本前，可以写成 `HEAD~39` 。

当你想要回到当时回退前的版本时，只要找到那个版本的 `commit id` ，就可以回到那个版本了

比如上面例子的第二个版本

```
$ git reset --hard 1741e2b
```

这样就可以回到第二个版本了，版本不需要写全，只需要写最前面几位即可， `Git` 会自己去匹配对应的版本（但是也不能太短哟），当已经找不到之前回退的版本号时，可以使用 `git reflog` ，这个命令记录了你每一次版本修改命令

```
$ git reflog
2c933d4 (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
1741e2b HEAD@{1}: commit: 创建 Demo Repository 和 Interface
2c933d4 (HEAD -> master) HEAD@{2}: commit (initial): 创建 study 项目
```

`1741e2b` 就是我们当时第二个版本的 `commit id`

如果想要放弃对某个文件的修改

```
$ git checkout -- <name>
```

`name` 为想要放弃修改的文件的名称，此处分为两种情况
如果该文件自修改后还没有放到暂存区，此时修改会回到和版本库一模一样的状态
另一种情况是该文件已经添加到暂存区，又作了修改，此时撤销修改就会回到暂存区后的状态
总之，就是让这个文件回到最近一次的 `git commit` 或者 `git add` 时的状态

`git checkout -- <name>` 中的 `--` 非常重要不可省略，因为没有 `--` 就会变成另一个命令了

当要删除项目中一个文件时，可以直接使用 `rm` 或者在 `IDE` 中直接删除，此时 Git 会知道你删除了文件，因为工作区和版本库之间不一致了，使用 `git status` 命令可以查看那些文件被删除了

```
$ rm demo.txt
$ git stautus
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    demo.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

现在你有两个选择，一个是确实要删除这个文件，那就使用 `git rm` 删除，并且 `git commit`
现在这个文件确实从版本库中删除了。
另一种就是删错了，因为版本库中还在，所以可以轻松的把误删的文件恢复到最新版本

```
$ git checkout -- demo.txt
```

这样文件就回来了

### 远程仓库

同一个 Git 仓库可以分布到不同的电脑上，可以找一台电脑充当服务器的角色，可以把各种提交推送到服务器仓库中，也可以从服务器仓库中拉取别人的提交。

如果没有服务器，可以使用 [GitHub](https://github.com) 免费提供的远程仓库

第一步：创建 SSH Key 。在用户主目录下，检查是否有 `.ssh` 目录，如果有，在看看该目录有没有 `id_rsa` 和 `id_rsa.pub` 这两个文件，如果已经有了，可以直接跳到下一步，如果没有，请使用以下命令创建 SSH Key

```
$ ssh-keygen -t rsa -C <your email>
```

一切顺利的话，可以在 `.ssh` 目录下找到 `id_rsa` 和 `id_rsa.pub` 这两个文件， `id_rsa` 是私匙，不可以泄露出去， `id_rsa.pub` 是公匙，可以放心告诉别人。

第二部：登录 GitHub ，打开 “Account settings” 中的 “SSH Key” 页面
点 “Add SSH Key” ，填上任意 Title ，在 Key 文本框中粘贴 `id_rsa.pub` 文件的内容

#### 添加远程仓库

首先在 GitHub 上建立一个名为 study 的仓库，保持默认设置，点击 “Create repository” 按钮，就成功的建立了一个新的 Git 仓库
目前这个 study 仓库还是空的，Github 告诉我们可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到 GitHub 仓库。

现在根据提示，对本地仓库运行命令

```
$ git remote add origin git@github.com:aixieluo/study.git
```

此处注意，上面的 `aixieluo` 是我的 Github 名称，使用时请使用自己的账户名
添加后 `origin` 就是远程仓库的名字了，这是 Git 默认的叫法，可以自定义

下一步就是将本地仓库的内容推送到远程库上：

```
$ git push -u origin master
Counting objects: 136, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (115/115), done.
Writing objects: 100% (136/136), 226.80 KiB | 0 bytes/s, done.
Total 136 (delta 16), reused 0 (delta 0)
remote: Resolving deltas: 100% (16/16), done.
To github.com:aixieluo/study.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

把本地库的内容推送到远程，用 `git push` 命令，实际上是把当前分支 master 推送到远程。

由于远程库是空的，我们第一次推送 `master` 分支时，加上了 `-u` 参数，Git 不但会把本地的 `master` 分支内容推送的远程新的 `master` 分支，还会把本地的 `master` 分支和远程的 `master` 分支关联起来，在以后的推送或者拉取时就可以简化命令。

### 分支管理

首先我们创建 `dev` 分支，然后切换到 `dev` 分支

```
$ git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout` 命令加上 `-b` 参数，表示创建并且切换，相当于以下两条命令

```
$ git branch dev
$ git checkout dev
Switched to a new branch 'dev'
```

使用 `git branch` 可以查看当前分支，当前分支前面会表示一个 `*` 号

```
$ git branch
* dev
  master
```

删除文件 `demo.txt`

```
$ git rm demo.txt
rm 'demo.txt'
```

然后提交

```
$ git commit -m "delete demo.txt"
```

然后切换回 `master` 分支，发现删除掉的 `demo.txt` 出现了。

现在我们把 `dev` 分支的工作成果合并到 `master` 分支上

```
$ git merge dev
Updating dead195..e9ed3d4
Fast-forward
 demo.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 demo.txt
```

`git merge` 命令用于合并指定分支到当前分支，合并后可以放心的删除 `dev` 分支
注意到上面的 `Fast-forward` 信息， Git 告诉我们，这次合并是“快进模式”，也就是直接把 `master` 指向 `dev` 的当前提交，所以合并速度非常快。

`Fast-foward` 模式下，删除分支后，会丢失分支信息。如果要强制禁用 `Fast-foward` 模式， Git 就会在 merge 模式时生成一个新的 commit ，这样，从分支历史上就可以看到分支信息了。
`--no-ff` 参数强制禁用 `Fast-foward` 模式，使用 `--no-ff` 参数时，合并要创建一个新的 commit ，所以要带上 `-m` 参数

`git log` 使用 `--graph` 参数可以查看分支历史， `abbrev-commit` 参数可以查看缩略版的 `commit id`

#### 删除分支 `dev`

```
$ git branch -d dev
Deleted branch dev (was e9ed3d4).
```

#### 强制删除未合并分支

要删除未合并的分支时，需要强行删除，使用 `-D` 参数

```
$ git branch -D dev
Deleted branch dev (was e9ed3d4).
```

#### 拉取远程分支到本地

将远程分支 `branch_name` 拉取到本地，并创建同名分支并切换到此分支，此命令会使远程分支与本地分支建立映射关系

```
git checkout -b branch_name origin branch_name
```

#### 删除远程分支

删除远程分支的方式比较无厘头

```
$ git push origin :feature/page3
To https://github.com/aixieluo/xyd.git
 - [deleted]         feature/page3
```

可以用此方式删除远程分支

#### 储藏工作场景

软件开发过程中，当前分支开发到一半，不能提交，然后又有一个急需修复的 bug ，使用 `git stash` 可以先将当前工作场景“储藏”起来，等以后恢复现场后急需工作，处理完 bug 后，使用 `git stash list` 查看刚才保存的工作场景，`git stash apply` 指令可以恢复以前的工作场景，但是并不会删除 stash 内容，需要额外使用 `git stash drop` 删除，如果想恢复同时删除，可以使用 `git stash pop` ，在恢复的同时把 stash 内容也删除了。
你可以多次 stash ，恢复的时候使用 `git stash list` 然后恢复指定的 stash

```
$ git stash list
stash@{0}: WIP on master: cf1b7e8 add megre
$ git stash apply stash@{0}
```

#### 小结

查看分支列表 `git branch`

创建分支 `git branch <name>`

切换分支 `git checkout <name>`

创建+切换分支 `git checkout -b <name>`

合并某分支到当前分支 `git merge <name>`

删除分支 `git branch -d <name>`

强行删除未合并分支 `git branch -D <name>`

隐藏当前工作场景 `git stash`

显示以前隐藏的工作场景列表 `git stash list`

恢复以前的工作场景 `git stash apply`

删除以前的工作场景 `git stash drop`

恢复并删除以前的工作场景 `git stash pop`

### 标签管理

在 Git 中打标签非常的容易，首先，切换到需要打标签的分支上

```
$ git branch
* dev
master
$ git checkout master
Switched to branch 'master'
$ git tag v1.0
```

然后使用 `git tag` 可以查看所有标签列表

默认标签是打在最新提交的 commit 上的，如果想要打到以前提交的 commit 上，只要找到对应的 `commit id` 就可以了

```
$ git log --pretty=oneline --abbrev-commit
cf1b7e8 (HEAD -> master) add megre
2eb259e (dev) create the demo.txt
e9ed3d4 (origin/dev) delete the demo.txt
dead195 (origin/master) Create README.md
f4f1eba create a txt file
2c933d4 创建 study 项目
```

比如要给第一次提交的 commit 打上标签

```
$ git tag v0.1 2c933d4
$ git tag
v0.1
```

注意标签不是按时间顺序给出的，而是按照字母排序的，可以用 `git show <tagname>` 查看标签信息

```
$ git show v0.1
commit 2c933d4ab6813030699fc4f0209e0ddfebbee7fa (tag: v0.1)
Author: 39 <admin@aixieluo.com>
Date:   Fri Jul 14 17:23:35 2017 +0800

    创建 study 项目
...
```

使用 `-a` 指定标签名，可以加上 `-m` 指定说明文字

```
$ git tag -a v0.2 -m "这是 0.2 版本" 2eb259e
$ git show v0.2
tag v0.2
Tagger: 39 <admin@aixieluo.com>
Date:   Mon Jul 17 13:31:30 2017 +0800

这是 0.2 版本

commit 2eb259e26d4242db3c2c8627043d11ffbda3cfc3 (tag: v0.2, dev)
Author: 39 <admin@aixieluo.com>
Date:   Mon Jul 17 13:02:33 2017 +0800

    create the demo.txt
...
```

如果不想要标签或者打错标签时，也是可以删除的

```
$ git tag -d v0.1
Deleted tag 'v0.1' (was 2c933d4)
```

因为标签只存储在本地，不会自动推送到远程，所以打错的标签可以安全的在本地删除

如果要推送某个标签到远程，可以使用 `git push origin <tagname>`

```
$ git push origin v0.2
Counting objects: 1, done.
Writing objects: 100% (1/1), 173 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To github.com:aixieluo/study.git
 * [new tag]         v0.2 -> v0.2
```

如果标签已经从本地推送到远程，删除起来比较麻烦一点，先从本地删除，然后从远程删除

```
$ git tag -d v0.2
Deleted tag 'v0.2' (was d4c4ece)
$ git push origin :refs/tags/v0.2
To github.com:aixieluo/study.git
 - [deleted]         v0.2
```

### 配置 Git 指令别名

有没有感觉 Git 指令单词过多，不容易记住，就算记住，每次都要敲一遍是不是也挺麻烦的
如 `git status` 自定义为 `git st` 是不是就变得很简单了

创建别名的方法如下， `--global` 代表当前电脑下所有 Git 仓库都适用这个配置

```
$ git config --global alias.st status
$ git config --global alias.co checkout
$ git config --global alias.cm commit
$ git config --global alias.br branch
```

以后提交就可以简写为

```
$ git cm -m `...`
```

每个仓库的 Git 配置都放在 `.git/config` 文件中，公共的 Git 配置文件放在用户主目录下的隐藏文件 `.gitconfig` 中

我的别名列表

st = status
co = checkout
cm = commit

### 搭建自己的 Git 服务器






