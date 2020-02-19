### Git是什么

Git是目前世界上最先进的分布式版本控制系统。

工作原理 / 流程：

![img](/img/流程图.png)

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



学习地址：https://www.yiibai.com/git