### 合并两个git仓库

有2个git仓库：A、B；

想将A中的文件移入B；

A的历史日志要保留；

**1、将A作为远程仓库，添加到B中，设置别名为other**

git remote add other + A的远程仓库地址

**2、从A仓库中抓取数据到本仓库**

git fetch other

**3、将A仓库抓去的master分支作为新分支checkout到本地，新分支名设定为dev**

git checkout -b dev other/master

**4、切换回B的master分支**

git checkout master

**5、将dev合并入master分支**

git merge dev

如果报 fatal: refusing to merge unrelated histories

可执行：git merge dev --allow-unrelated-histories