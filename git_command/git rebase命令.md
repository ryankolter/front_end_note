# git rebase命令

## rebase变基，把 别人开发的other分支内容 栽种到 本分支上

```bash
git checkout other
git rebase master
//此时other分支被栽种到master上面

//如果遇见冲突，则会暂停
可选择手动解决后，输入
git rebase --continue 
或者选择放弃，输入
git rebase --abort

//要记得把master快速移动到other上完成合并
git checkout master
git merge other
```

【比较】
merge会有很多个分支交叉在一起，很凌乱
rebase永远都是一条线，很清爽

## rebase变基，精简合并多个commit

```js
git log --oneline
//显示从最近到最远信息
————————————————
27f6ed6 (HEAD -> master) add dog 2
2bab3e7 add dog 1
ca40fc9 add 2 cats
1de2076 add cat 2
cd82f29 add cat 1
382a2a5 add database settings
bb0c9c2 init commit
————————————————

git rebase -i bb0c9c2
//基于最远的变基，显示多个commit如下，进入可编辑模式
//这里有6个，也可以用等价命令 git rebase -i HEAD~6
————————————————
pick 382a2a5 add database settings
pick cd82f29 add cat 1
pick 1de2076 add cat 2
pick ca40fc9 add 2 cats
pick 2bab3e7 add dog 1
pick 27f6ed6 add dog 2
————————————————

pick默认，
第一行的可保留
后面几行的可编辑改成：
squash或s，把当前commit要融到上面一个commit中，用于精简合并
reword，把当前commit记录为要更改，用于重写此次提交信息
```