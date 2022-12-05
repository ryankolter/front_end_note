# git 提交命令

## status查看当前状态

```bash
git status
//会列出当前分支，落后情况，暂存区内容，工作区变更，未跟踪的新文件
```

## add添加待提交文件

```bash
git add 文件名
//添加能被提交的单个文件

git add 文件夹/
//添加文件夹内所有能被提交的文件

git add -A
//添加所有文件

git add -u
//添加被修改和被删除的文件（不包括新文件）

git add .
//添加被修改的文件和新文件（不包括被删除的文件）
```
- 添加后，文件从 （working tree）工作区 进入到 （staged）暂存区

## commit提交本地仓库

```bash
git commit -m "备注的提交信息"

git commit -a -m "备注的提交信息"
//等于先调用了git add -u，把修改过的和删掉的文件添加了

git commit --amend
//修改上次提交的备注信息

git commit --allow-empty -m "空提交信息"
//提交一个没有变更的分支，用来重新触发CI构建
```
- 提交后，文件从 （staged）暂存区 进入到 （repository）仓库区

## push推送远程仓库

```bash
git push <远程主机名> <本地分支名>:<远程分支名>

git push origin
//指定远程主机，把本分支推到同名远程分支

git push -u origin master
//用-u表示指定默认主机，以后直接git push即可

git push -f
//慎用，在本地和远程分支有分叉时，强制推送，覆盖远程分支
```