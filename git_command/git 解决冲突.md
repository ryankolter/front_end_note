# git 解决冲突

## 拉取代码

```bash
git status

git stash
//暂存未提交的修改

git checkout new_branch

git pull

git stash pop
//弹出未提交的修改
```

## 出现冲突

冲突文件列在Unmerged paths:下面

## 解决办法

### 【如果要保留文件的修改】

```bash
vi 冲突文件
```
（如果vi打开后，随便用了ctrl+z关掉vi，其实本质是挂起，再次打开会因为存在swp后缀文件而无法打开，需要恢复挂起任务，查看挂起：jobs -l）

`/<<<<<<` 查找冲突的开始，可用n键找下一组冲突开始
`/>>>>>>` 查找冲突的结束
`/======` 查找前后冲突的分界线

决定哪部份需要采用，然后用d整行删掉上面三条线

`:wq`保存退出

`git add 解决后的冲突文件`，使其最终完成解决

`git reset HEAD .` 把所有文件恢复到unstage的状态，使其后续可以被git stash

### 【如果不保留文件修改】

`git reset HEAD .` 把所有文件恢复到unstage的状态

`git checkout xxx/xxx.xx` 把此文件直接放弃本地的改动，恢复到远程状态

