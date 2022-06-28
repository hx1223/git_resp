# Git 简介

![image-20220628185837906](C:\Users\hx\AppData\Roaming\Typora\typora-user-images\image-20220628185837906.png)

命令如下：

clone（克隆）: 从远程仓库中克隆代码到本地仓库
checkout （检出）:从本地仓库中检出一个仓库分支然后进行修订
add（添加）: 在提交前先将代码提交到暂存区
commit（提交）: 提交到本地仓库。本地仓库中保存修改的各个历史版本
fetch (抓取) ： 从远程库抓取到本地仓库，不进行任何的合并动作，一般操作比较少。
pull (拉取) ： 从远程库拉到本地库，自动进行合并(merge)，然后放到到工作区，相当于
fetch+merge
push（推送） : 修改完成后，需要和团队成员共享代码时，将代码推送到远程仓库

# Git安装与基本使用

## 安装：

省略

## 基本使用：

### 1.设置用户信息

`git config --global user.name "XXX" # 设置用户名`
`git config --global user.email "XXXX" # 设置邮箱`

### 2.查看配置信息

`git config --global user.name`
`git config --global user.email`

### 3.为命令设置别名（非必要）

1.打开用户目录，创建 .bashrc 文件

`touch ~/.bashrc`

![image-20220628190741062](C:\Users\hx\AppData\Roaming\Typora\typora-user-images\image-20220628190741062.png)

2.在.bashrc输入以下内容

`#用于输出git提交日志` 

`alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'` 
`#用于输出当前目录所有文件及基本信息` 
`alias ll='ls -al'`

注：i编辑，vi退出编辑时，按esc，输入冒号（英文），然后切换到最后一行模式，最后一行模式决定是否保存文件。例如输入:wq保存并退出。

3.打开gitBash,执行

`source ~/.bashrc`

### 4.创建本地仓库

##### 1.在电脑的任意位置创建一个空目录（例如test）作为我们的本地Git仓库

##### 2.进入这个目录中，点击右键打开Git bash窗口

##### 3.执行命令`git init`

##### 4.如果创建成功后可在文件夹下看到隐藏的.git目录


![image-20220628200958216](C:\Users\hx\AppData\Roaming\Typora\typora-user-images\image-20220628200958216.png)

### 5.基本配置指令

##### 1.`git add` (工作区 —> 暂存区)

例如:`git add file.txt`

将所有修改加入暂存区 `git add .`

##### 2.`git commit` (暂存区 —> 本地仓库)

例如: `git commit -m ‘注释内容’`

##### 3.status查看修改的状态

`git status`

##### 4.log查看提交日志

配置的别名git-log就包含了这些参数，所以后续可以直接使用指令 git-log

作用:查看提交记录

命令形式：`git log [option] 或者 git-log`

`—all 显示所有分支`
`—pretty=oneline 将提交信息显示为一行`
`—abbrev-commit 使得输出的commitId更简短`
`—graph 以图的形式显示`

##### 5.版本回退

`git reset --hard commitID` 

`commitID 可以使用 git-log 或 git log 指令查看`

##### 6.添加文件至忽略列表

一般我们总会有些文件无需纳入Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以在工作目录中创建一个名为 .gitignore 的文件（文件名称固定），列出要忽略的文件模式。

`file02.txt`

`#也可以使用通配符，例如`

`*.txt`
`*.iml`
`...`

##### 6.分支

几乎所有的版本控制系统都以某种形式支持分支。 使用分支意味着你可以把你的工作从开发主线上分离开来进行重大的Bug修改、开发新的功能，以免影响开发主线。

###### 1.查看本地分支 

```
 `git branch`
```

###### 2.创建本地分支

```
git branch 分支名
```

###### 3.切换分支

```
git checkout 分支名
```

###### 4.创建并切换：

我们还可以直接切换到一个不存在的分支

```
git checkout -b 分支名
```

###### 5.合并分支

一个分支上的提交可以合并到另一个分支

```
git merge 分支名
```

###### 6.删除分支

不能删除当前分支，只能删除其他分支

```
git branch -d 分支名 # 删除分支时，需要做各种检查
```

```
git branch -D 分支名 # 不做任何检查，强制删除
```

###### 7.解决冲突

当两个分支上对文件的修改可能会存在冲突，例如同时修改了同一个文件的同一行，这时就需要手动解决冲突，解决冲突步骤如下：

1.处理文件中冲突的地方
2.将解决完冲突的文件加入暂存区(add)
3.提交到仓库(commit)

###### 8.开发中分支使用原则与流程

几乎所有的版本控制系统都以某种形式支持分支。 使用分支意味着你可以把你的工作从开发主线上分离开来进行重大的Bug修改、开发新的功能，以免影响开发主线。

在开发中，一般有如下分支使用原则与流程：

------

1.**master （生产） 分支**：线上分支，主分支，中小规模项目作为线上运行的应用对应的分支；

2.**develop（开发）分支**：是从master创建的分支，一般作为开发部门的主要开发分支，如果没有其他并行开发不同期上线要求，都可以在此版本进行开发，阶段开发完成后，需要是合并到master分支，准备上线。

3.**feature/xxxx分支**：从develop创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完成后合并到develop分支，之后该分支可以删除。

4.**hotfix/xxxx分支**：从master派生的分支，一般作为线上bug修复使用，修复完成后需要合并到master、test、develop分支。

5.还有一些**其他分支**，在此不再详述，例如test分支（用于代码测试）、pre分支（预上线分支）等
等。

------


![image-20220628205235132](C:\Users\hx\AppData\Roaming\Typora\typora-user-images\image-20220628205235132.png)

### 6.Git远程仓库

**常用的托管服务**

前面我们已经知道了Git中存在两种类型的仓库，即本地仓库和远程仓库。那么我们如何搭建Git远程仓库呢？我们可以借助互联网上提供的一些代码托管服务来实现，其中比较常用的有GitHub、码云、GitLab等。

- GitHub（ 地址：https://github.com/ ）是一个面向开源及私有软件项目的托管平台，因为只支持Git 作为唯一的版本库格式进行托管，故名GitHub


- 码云（地址： https://gitee.com/ ）是国内的一个代码托管平台，由于服务器在国内，所以相比于 GitHub，码云速度会更快


- GitLab （地址： https://about.gitlab.com/ ）是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并在此基础上搭建起来的web服务，一般用于在企业、学校等内部网络搭建git私服。


##### 1.操作远程仓库

此操作是先初始化本地库，然后与已创建的远程库进行对接。

**命令：**

- 远端名称：默认是origin，取决于远端服务器设置
- 仓库地址：从远端服务器获取此url

```
git remote add <远端名称> <仓库地址>
```

```
例如：git remote add origin git@gitee.com:czbk_zhang_meng/git_test.git
```

##### 2.查看远程仓库

```
git remote
```

##### 3.推送到远程仓库

```
git push [-f] [--set-upstream] [远端名称] [本地分支名][:远端分支名]
```

注意:如果远程分支名和本地分支名相同，则可以只写本地分支名

- `-f`  表示强制推送，**一般在公司内没有这个的使用权限**，否则容易冲掉远程仓库的所有代码
- `--set-upstream` 推送到远端的同时，建立起和远端分支的关联关系。用于第一次推送时。
-   如果当前分支已经和远端分支关联，则可以省略分支名和远端名
- git push 将master分支推送到已关联的远端分支

##### 4.从远程仓库克隆

如果已经有一个远端仓库，我们可以直接clone到本地。

```
git clone <仓库地址> [本地目录]
```

##### 5.从远程仓库中抓取和拉取

远程分支和本地的分支一样，我们可以进行merge操作，只是需要先把远端仓库里的更新都下载到本地，再进行操作。

**抓取：**

抓取指令就是将仓库里的更新都抓取到本地，不会进行合并

如果不指定远端名称和分支名，则抓取所有分支。

```
git fetch [remote name] [branch name]
```

**拉取：**

- 拉取指令就是将远端仓库的修改拉到本地并自动进行合并，等同于fetch+merge

- 如果不指定远端名称和分支名，则抓取所有并更新当前分支。

```
git pull [remote name] [branch name]
```

##### 6.解决合并冲突

- 在一段时间，A、B用户修改了同一个文件，且修改了同一行位置的代码，此时会发生合并冲突。

- A用户在本地修改代码后优先推送到远程仓库，此时B用户在本地修订代码，提交到本地仓库后，也需要推送到远程仓库，此时B用户晚于A用户，故需要先拉取远程仓库的提交，经过合并后才能推送到远端分支，如下图所示。
- 在B用户拉取代码时，因为A、B用户同一段时间修改了同一个文件的相同位置代码，故会发生合并冲突。
- 远程分支也是分支，所以合并时冲突的解决方式也和解决本地分支冲突相同相同



![image-20220628211357964](C:\Users\hx\AppData\Roaming\Typora\typora-user-images\image-20220628211357964.png)

## Idea中使用GIt

场景：本地已经有一个项目，但是并不是git项目，我们需要将这个放到码云的仓库里，和其他开发人员继续一起协作开发。


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119181425292.png)

### 1.初始化本地仓库

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119181801881.png)

### 2.选择本项目

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119181854045.png)

### 3.设置远程仓库

- ### 查找选项

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119182056750.png)

- ### 输入远程仓库地址

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119182153941.png)

###  4.提交到本地仓库

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119182359136.png)

### 5.推送到远程仓库

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119182651297.png)

### 6.创建分支

- 方法一：最常规的方式

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119190427959.png)

- 方法2：最强大的方式

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img8/image-20220119190603175.png)

### 7.总结

- 在IDEA的终端中可使用git命令来完成以上所有功能

- 切换分支前先提交本地的修改
- 代码及时提交，提交过了就不会丢

# GIt知识点补充

### 1.HEAD的理解

- HEAD 指向当前所在的分支，类似一个活动的指针，表示一个「引用」。

- HEAD 既可以指向「当前分支」的最新 commit，也可以指向历史中的某一次 commit (「分离头指针」的情况)。归根结底，HEAD 指向的就是某个提交点。

- 当我们做分支切换时，HEAD 会跟着切换到对应分支。


### 2.fast-forward 与 —no-ff 的区别

假如有一个场景：有两个分支，master 分支和 feature 分支。现在，feautre 分支需要合并回 master 分支。


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228134116327.png)

- **fast-forward** 合并方式是条件允许的情况，通过将 master 分支的 HEAD 位置移动到 feature 分支的最新提交点上，这样就实现了快速合并。这种情况，是不会新生成 commit 的。（快进模式）

```
git checkout master
# 先切换到master分支
git merge feature 
# 将feature分支合并到当前分支上（master）
```


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228134238702.png)

- **--no-ff** 的方式进行合并，master 分支就会新生成一次提交记录。

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228134456687.png)

```
git checkout master 
# 先切换到master分支
git merge --no-ff feature 
# 将feature分支合并到当前分支上（master）
```

注意：

如果条件满足时，merge 默认采用的 **fast-forward** 方式进行合并，除非你显示的加上 **--no-ff** 选项；而条件不满足时，merge 也是无法使用 fast-forward 合并成功的！

### 3.merge操作

- git merge 操作是区分上下文的。当前分支始终是目标分支，其他一个或多个分支始终合并到当前分支。这个注意点记住了，方便记忆！所以，当需要将某个分支合并到目标分支时，需要先切到目标分支上。


**注意：**

- 快进模式能够进行的条件是：源分支和目标分支之间没有分叉。下图则是无法通过 HEAD 的快速移动实现分支的合并。


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228135612743.png)

- 如果执行合并操作，默认会尝试 fast-forward 的方式进行合并，但是因为分叉了，所以此时会采用 no-ff 的方式进行合并，有新的 commit 生成了。最终的结果图如下：


```
git checkout master 
# 先切换到目标分支
git merge feature
```


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228135749975.png)

### 4.rebase操作

- rebase 合并往往又被称为 「变基」。这里的「基」就是一个「基点」、「起点」的意思。`git rebase` 命令通常称为向前移植（forward porting）。

- 「变基」就是改变当前分支的起点。注意，是当前分支！ rebase 命令后面紧接着的就是「基分支」。与merge操作相反。

  **变基前：**


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228140250490.png)

```
git checkout feature # 切换到当前分支，或待变基分支
git rebase master # 变基

# 可合并为下面的语句
git rebase master feature
```

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228140717295.png)

**解释：**rebase，变基，可以直接理解为改变基底。**feature分支**是基于master分支的B拉出来的分支，feature的基底是B。而master在B之后有新的提交，就相当于此时要用master上新的提交来作为feature分支的新基底。实际操作为把B之后feature的提交存下来，然后删掉原来这些提交，再找到master的最新提交位置，把存下来的提交再接上去（新节点新commit id），如此feature分支的基底就相当于变成了E而不是原来的B了。（注意，如果master上在B以后没有新提交，那么就还是用原来的B作为基，rebase操作相当于无效，此时和git merge就基本没区别了，差异只在于git merge会多一条记录Merge操作的提交记录）

- 往公共分支上合代码的时候，推荐使用merge。

- 拉公共分支最新代码的时候，推荐使用rebase，也就是git pull -r或git pull --rebase，但有个缺点就是rebase以后我就不知道我的当前分支最早是从哪个分支拉出来的了，因为基底变了嘛。


### 5.示例

从Develop分支分出两个分支，分属两个人员进行开发。F1分支开发完毕后，push到总分支。F2分支开发到F2_5时需要拉取最新代码。

**1.如果F2分支采用git pull拉取最新代码：**

- F1分支的视角（F1分支的commit记录）：

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228144950474.png)

- F2分支的视角：这将会把F1分支的修改直接拉下来于本地代码merge，且产生一个commit F2_5，也就是merge commit。


![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228145053996.png)

**2.如果F2分支采用git pull --rebase 拉取最新代码：**

F1分支视角不变

F2分支视角：

![img](https://kisugitakumi.oss-cn-chengdu.aliyuncs.com/img11/image-20220228150132439.png)

### 6.强制拉取到本地仓库

有些时候本地仓库提交管理混乱，需要从远程仓库强制拉取，以刷新本地仓库，覆盖所有add和commit操作。可执行以下代码：

```
git fetch --all  
git reset --hard origin/master 
git pull
```

### 7.远程分支合并

该项职责由git管理员来完成。例如当开发分支Develop上的所有功能已经完成时，需要合并到master上时：

- 
  代码clone到本地仓库

```
git clone
```

- 在本地创建dev分支并与远程dev分支对应

```
git checkout -b dev origin/dev
```

- 切换到master分支

```
git checkout master
```

- 本地的dev合并到master上（遇到冲突解决完后再次提交）

```
git merge dev
```

- 推送到远程的master上（执行这项操作时，需要有操作远程master分支的权限）

```
git push origin master
```

