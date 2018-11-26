---
title: 如何简单使用Git进行版本控制
date: 2018-11-25 20:54:14
tags:
 - Github
---

本文内容涵盖你在使用Git完成各种工作中将要使用的各种基本命令。 在学习完本章之后，你应该能够配置并初始化一个仓库(repository)、开始或停止跟踪 (track)文件、暂存(stage)或提交(commit)更改。
<!-- more -->

在保存和对待各种信息的时候与其它版本控制系统有很大差异，尽管操作起来的命令形式非常相近，理解这些差异将有助于防止你使用中的困惑。
### Git特点：直接记录快照，而非差异比较
Git和其它版本控制系统(包括Subversion和近似工具)的主要差别在于Git对待数据的方法。概念上来区分，其它大部分系统以文件变更列表的方式存储信息。这类系统(CVS、Subversion、Perforce、Bazaar等等)将它们保存的信息看作是一组基本文件和每个文件随时间逐步累积的差异。
Git不按照以上方式对待或保存数据。反之，Git更像是把数据看作是对小型文件系统的一组快照。每次你提交更新，或在Git中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。为了高效，如果文件没有修改，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件。Git对待数据更像是一个快照流。
### Git的三种状态
Git有三种状态，你的文件可能处于其中之一:已提交(committed)、已修改(modified)和已暂存(staged)。已提交表示数据已经安全的保存在本地数据库中。已修改表示修改了文件，但还没保存到数据库中。已暂存表示对一个已修改文件的当前 版本做了标记，使之包含在下次提交的快照中。

### 安装 Git
如果你想在Linux上用二进制安装程序来安装Git，可以使用发行版包含的基础软件包管理工具来安装在 Mac上安装Git有多种方式。最简单的方法是安装 Xcode Command Line Tools。在 Windows上安装Git也有几种安装方法。官方版本可以在Git官方网站下载。

### 初次运行 Git 前的配置
#### 用户信息
当安装完Git应该做的第一件事就是设置你的用户名称与邮件地址。 这样做很重要，因为每一个 Git 的提交都会 使用这些信息，并且它会写入到你的每一次提交中，不可更改:

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com

```
#### 检查配置信息
如果想要检查你的配置，可以使用git config --list命令来列出所有Git当时能找到的配置。你可能会看到重复的变量名，因为Git会从不同的文件中读取同一个配置(例如:/etc/gitconfig 与 ~/.gitconfig)。这种情况下Git会使用它找到的每一个变量的最后一个配置。

### 获取帮助
若你使用 Git 时需要获取帮助，有三种方法可以找到 Git 命令的使用手册:

```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>

```

### 获取 Git 仓库

有两种取得Git项目仓库的方法。 第一种是在现有项目或目录下导入所有文件到Git中; 第二种是从一个服务器克隆一个现有的Git仓库。
在现有目录中初始化仓库：

```
$ git init

```
克隆现有的仓库：

```
 $ git clone https://github.com/libgit2/libgit2
```
如果你想在克隆远程仓库的 时候，自定义本地仓库的名字，你可以使用如下命令:

```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

### 记录每次更新到仓库
#### 检查当前文件状态
要查看哪些文件处于什么状态，可以用 git status 命令。 如果在克隆仓库后立即使用此命令，会看到类似这 样的输出:

```
$ git status
On branch master
nothing to commit, working directory clean

```
#### 跟踪新文件
使用命令 git add 开始跟踪一个文件。 所以，要跟踪 README 文件，运行：

```
$ git add README

```
#### 暂存已修改文件
现在我们来修改一个已被跟踪的文件。如果你修改了一个名为CONTRIBUTING.md的已被跟踪的文件，要暂存这次更新，需要运行 git add 命令。

```
$ git add CONTRIBUTING.md

```

#### 状态简览
git status 命令的输出十分详细，但其用语有些繁琐。如果你使用 git status -s 命令或 git status --short命令，你将得到一种更为紧凑的格式输出。

#### 忽略文件
一般我们总会有些文件无需纳入Git的管理，也不希望它们总出现在未跟踪文件列表。在这种情况下，我们可以创建一个名为 .gitignore 的文件，列出要忽略的文件模式。来看一个实际的例子:

```
$ cat .gitignore
*.[oa]
*~
```
第一行告诉Git忽略所有以 .o 或 .a 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的。第二行告诉Git忽略所有以波浪符(~)结尾的文件，许多文本编辑软件(比如Emacs)都用这样的文件名保存副本。 

#### 提交更新
现在的暂存区域已经准备妥当可以提交了。 在此之前，请一定要确认还有什么修改过的或新建的文件还没有 git add 过，否则提交的时候不会记录这些还没暂存起来的变化。

```
$ git commit
```
这种方式会启动文本编辑器以便输入本次提交的说明。
另外，你也可以在 commit 命令后添加 -m 选项，将提交信息与命令放在同一行，如下所示:

```
$ git commit -m "Story 182: Fix benchmarks for speed"
master 463dc4f] Story 182: Fix benchmarks for speed
  2 files changed, 2 insertions(+)
  create mode 100644 README
   
```

#### 移除文件
要从Git中移除某个文件，就必须要从已跟踪文件清单中移除(确切地说，是从暂存区域移除)，然后提交。可以用git rm命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。

```
  $ git rm PROJECTS.md
  rm 'PROJECTS.md'
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    
      deleted:    PROJECTS.md

   
```
下一次提交时，该文件就不再纳入版本管理了。 如果删除之前修改过并且已经放到暂存区域的话，则必须要用 强制删除选项 -f(译注:即 force 的首字母)。这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被Git恢复。

#### 移动文件
```
$ git mv file_from file_to
```

### 远程仓库的使用
#### 查看远程仓库
如果想查看你已经配置的远程仓库服务器，可以运行 git remote 命令。你也可以指定选项 -v，会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。

```
$ git remote -v
origin  https://github.com/schacon/ticgit (fetch)
origin  https://github.com/schacon/ticgit (push)
  
```
#### 添加远程仓库
我在之前的章节中已经提到并展示了如何添加远程仓库的示例，不过这里将告诉你如何明确地做到这一点。 运 行git remote add <shortname> <url>添加一个新的远程Git仓库。

#### 从远程仓库中抓取与拉取
这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支 的引用，可以随时合并或查看。

```
$ git fetch [remote-name]
```

#### 推送到远程仓库
当你想分享你的项目时，必须将其推送到上游当你想要将 master 分支推送到 origin 服务器时(再次说明，克隆时通常会自动帮你设置好那两个 名字)，那么运行这个命令就可以将你所做的备份到服务器。

```
$ git push origin master
```
如果是想要把本地master分支推送远程仓库的hexo分支的话使用命令：
```
$ git push origin master:hexo
```
只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 

#### 查看远程仓库
如果想要查看某一个远程仓库的更多信息，可以使用 git remote show [remote-name] 命令。 如果想以 一个特定的缩写名运行这个命令，例如 origin，会得到像下面类似的信息:

```
$ git remote show origin
  * remote origin
    Fetch URL: https://github.com/schacon/ticgit
    Push  URL: https://github.com/schacon/ticgit
    HEAD branch: master
    Remote branches:
      master                               tracked
      dev-branch                           tracked
    Local branch configured for 'git pull':
      master merges with remote master
    Local ref configured for 'git push':
      master pushes to master (up to date)
     
```

#### 远程仓库的移除与重命名
如果想要重命名引用的名字可以运行 git remote rename 去修改一个远程仓库的简写名。 例如，想要将 pb 重命名为paul，可以用git remote rename这样做:

```
$ git remote rename pb paul
$ git remote
origin
paul

```
值得注意的是这同样也会修改你的远程分支名字。 那些过去引用 pb/master 的现在会引用 paul/master。

如果因为一些原因想要移除一个远程仓库 - 你已经从服务器上搬走了或不再想使用某一个特定的镜像了，又或者
某一个贡献者不再贡献了-可以使用git remote rm:

```
$ git remote rm paul
$ git remote
origin
```

### 总结
现在，你可以完成所有基本的 Git 本地操作-创建或者克隆一个仓库、做更改、暂存并提交这些更改。

**致谢：本文内容整理自《Pro Git》一书，作者Scott Chacon and Ben Straub。**









