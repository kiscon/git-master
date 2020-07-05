### Git是什么

Git是目前世界上最先进的分布式版本控制系统。

工作原理 / 流程：

![img](https://github.com/kiscon/git-master/blob/master/img/flow-chart.png)

- Workspace：工作区
- Index / Stage：暂存区
- Repository：仓库区（或本地仓库）
- Remote：远程仓库

### 理解工作区与暂存区的区别

工作区：就是你在电脑上看到的目录，比如目录下testgit里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。

版本库(Repository)：工作区有一个隐藏目录.git，这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD。

### git初始配置

#### ssh的提交方式

1. 先创建公钥和私钥

2. **ssh-keygen -t rsa**

3. c盘->用户->计算机的登陆名->.ssh文件夹 找到**.pub**结尾的文件，用词本打开，复制里面的内容， 然后到github的setting设置里面，找到SSH and GPG keys这一项，添加公钥就可以了

#### 设置用户名和邮箱

- git config --global user.email "you@example.com"

- git config --global user.name "Your Name"

### 分支的使用

- git init
- git add *
- git commit -m '初始化仓库'
- git branch + 分支名 
- git branch 查看分支名(同时可以知道当前所在的分支)
- git checkout + 分支名 切换到所要进入的分支

- - 例：git checkout dev 切换到dev分支

- git checkout -b + 分支名 创建并切换分支
- git merge + 分支名 将dev分支合并到master分支上来

- - 例： git merge dev 将dev分支合并到master分支上来

- git pull + 地址 拉取更新文件
- git push + 地址 + master 提交上传文件
- git clone + 地址 + (文件夹名称) 从远程服务器下载文件(包含git内容)
- git branch -d 分支名称 删除本地分支

- - 例：git branch -d hotfix

- git push origin  -d 分支名称 删除远程分支

- git config --list 查看配置

- gitk 内建的图形化git

### tag号操作常用命令

- git tag -a '0.3.0' -m '0.3.0版本' 	打tag号
- git push origin '0.3.0'	推送新的tag号
- git tag -d 0.2
- git push origin :refs/tags/0.2
- git push origin refs/tags/v.0.3:refs/tags/0.3.0
- git push origin :refs/tags/v.0.3

### remote

`git remote`命令管理一组跟踪的存储库

git remote -v

- 查看当前的远程仓库

git remote add origin + 仓库地址

- 添加远程仓库地址

git remote set-url origin + 新的仓库地址

- 更换远程仓库

git remote update origin -p(--prune)

- 获取远程分支列表

### log

git log

- 查看版本提交信息

- - 这是查看完整的版本信息 由提交的信息，作者和日期，还有版本号
  - 能够看到的内容，就有提交的记录 有消息，日期

git log --oneline

- 简化的提交操作信息 只有版本号和提交信息
- git log –pretty=oneline

git config format.pretty oneline

- 历史记录时只显示一行注释信息 —pretty＝：使用其他格式显示历史提交信息，可选项有：oneline,short,medium,full,fuller,email,raw以及format

git log --author=xxx

- 只查看xxx的提交记录

git log --name-status

- 看看哪些文件改变了

git log --pretty --name-status 文件名

- 查看某个文件的修改历史

git log -p 文件名

- 查看某个文件的修改内容

git reflog

- 查看所有的操作信息记录，包括回退版本的信息

git log file

- 可以看到一个文件的改动，以commit的形式展现


### add

git add -A

- 是将所有的文件提交到仓库的暂存区里面

git add .

git add *

- 将当前目录的所有修改添加到暂存区

### 子模块

1.在现有仓库中增加子模块：

 git submodule add + 地址

- 查看上面命令执行后现有仓库根目录有哪些变化 ：增加了1个文件和一个目录：.gitmodules和DbConnector文件夹

2.更新子模块的devlop分支

- 初始化子模块：git submodule init 
-  更新子模块：git submodule update
- 拉取所有子模块：git submodule foreach git pull origin devlop

### 回退和反做

git reset --hard + 提交的版本号

- 由当前版本回退到之前的任意版本
- git reset --hard HEAD^ 回退上个版本

git revert -n + 需要反做的版本号

git checkout --  文件名

- 丢弃工作区的修改

**区别**

1. git reset的作用是修改HEAD的位置，即将HEAD指向的位置改变为之前存在的某个版本
2. git revert的作用通过反做创建一个新的版本，这个版本的内容与我们要回退到的目标版本一样，但是HEAD指针是指向这个新生成的版本，而不是目标版本。

### 工作流

在Git中有以下[几种常见工作流](https://www.cnblogs.com/butterflybay/p/10348011.html)

- 集中式工作流
  - 对于集中式工作流，最好是使用[rebase ](http://gitbook.liuhui998.com/4_2.html)而不是生成一个合并提交
- 功能开发工作流
  - 这种工作流关注功能开发，不直接往master提交代码保证它是稳定并且干净的，而是从master拉取feature分支进行功能开发，团队成员根据分工拉取不同的功能分支来进行不同的功能开发，这样就可以完全隔离开每个人的工作。当功能开发完成后，会向master分支发起Pull Request，只有审核通过的代码才真正允许合入master，这样就加强了团队成员之间的代码交流，也就是我们常说的Code Review。
- Gitflow工作流
  - `develop`常驻分支，功能分支和提测分支都从此分支拉取。用于日常开发，包括代码优化、功能性开发。
  - `master`常驻分支，用于归档已上线代码，热修复分支从此分支拉取。每个版本上线后需在此分支打一个 tag 来标记版本。
  - `feature`功能开发和提测分支，用完即删。从develop分支拉取，特性开发会在其上进行，开发完毕合后并到develop分支。
  - `release`大版本提测分支，用完即删。分支从develop分支拉取，用于回归测试，完成后打tag并合入master和develop。
  - `hotfixes`热修复分支，用于紧急修复线上 bug。修复后打tag并合入master和develop。
- Forking工作流
  - 常用于开源项目，它有一个公开的中央仓库，其他贡献者可以Fork（克隆）这个仓库作为你自己的私有仓库，开源项目维护者可以直接往中央仓库push代码，而代码贡献者只能将代码push到自己的私有仓库，只有项目维护者接受代码贡献者往中央仓库发起的pull request才会真正合入。
 

### git diff查看本地改动

- git diff 
  - 可以查看本地的改动，即git status看到的文件的具体改动
- git diff commit-id1 commit-id2 --stat
  - 这个指令可以看两个版本之间有哪些文件改动
- git diff branch1 branch2 --stat
  - 这个指令可以看两个分支之间有哪些文件差异
- git diff tag1 tag2 --stat
  - 这个指令可以看两个tag之间有哪些文件差异或者改动

### cherry-pick
  git cherry-pick可以理解为”挑拣”提交，可以将A分支的某一次提交合入到本地当前分支上，那么就要使用git cherry-pick + commitId了。

  - 遇到冲突时
    - 先解决冲突
    - git add 将解决了冲突的文件添加到暂存区
    - git cherry-pick --continue就行

### fetch
  从远程获取最新版本到本地（只会将本地库所关联的远程库的commit id更新至最新），不会自动merge。

![img](https://github.com/kiscon/git-master/blob/master/img/fetch-pull.jpg)

- 与git pull 区别
  - git pull：操作是将本地仓库和远程仓库（本地的）更新到远程的最新版本。
  - git pull = git fetch + git merge
  - git pull的运行过程：首先，基于本地的FETCH_HEAD记录，比对本地的FETCH_HEAD记录与远程仓库的版本号，然后git fetch 获得当前指向的远程分支的后续版本的数据，然后再利用git merge将其与本地的当前分支合并。（FETCH_HEAD：是一个版本链接，记录在本地的一个文件中，指向着目前已经从远程仓库取下来的分支的末端版本。）
 
- git fetch origin dev
  - 执行上命令，会切换到`* branch  dev   -> FETCH_HEAD`
  - 指定远程remote和FETCH_HEAD，并且只拉取dev分支的提交。

- git merge origin/dev 
  - 合并远程仓库（本地的）到本地仓库

### git教程

学习地址：https://www.yiibai.com/git
