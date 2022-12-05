# git revert命令

## revert逆向重做，通过叠加一个逆提交，使 当前分支 变成 前面的某个commit

```bash
git revert HEAD
//逆向重做上一次commit

git revert HEAD^
//逆向重做前两次commit

git cherry-pick <HashA> <HashB> <HashC>
//逆向重做多个提交

git revert <HashA>^...<HashC>
//可以用 ^加三个点号 ，指定连续的一系列重做（包含A到C）
```

效果与reset差不多，但是reset会直接删掉历史，往后退，而revert会保留历史，同时逆向操作也会进入历史，向前进
