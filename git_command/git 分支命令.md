# git 分支命令

## 查看分支

```bash
git branch -v
//查看本地分支

git branch -a
//查看所有分支，包括本地和远程分支
```

## 创建分支

```bash
git branch test
//创建test分支
```

## 切换分支

```bash
git checkout test
//切换到已有的test分支

git checkout -b test2
//创建并切换到新的test2分支

git checkout -
//切换到上一次所在的分支
```

## 修改分支名

```bash
git branch -m xxxx
//分支名从test2改为xxxx
```

## 删除本地分支

```bash
git branch -d xxxx
//删除本地xxxx分支
```

## 删除远程分支

```bash
git push origin :xxxx
或
git push origin --delete xxxx
//删除远程xxxx分支
```

## diff比较分支差异
```bash
git diff
//比较出所有还没add暂存起来的更改(已经add的不会显示)

git diff 文件名
//比较出单个文件还没add暂存起来的更改(已经add的无法查看)

git diff HEAD
//比较当前和上次commit的差异(已经add的也可以查看)

git diff <commit ID>
//比较当前和某次commit的差异

git diff <分支1名称> <分支2名称>
//比较某两个分支的差异
```
按q可退出查看

