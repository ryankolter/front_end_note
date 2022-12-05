# git cherry-pick命令

## cherry-pick撷取别人开发的other分支的某几个提交

```bash
git cherry-pick <otherCommitHash>
//撷取一个提交，应用到当前分支上

git cherry-pick <HashA> <HashB> <HashC>
//撷取多个提交

git cherry-pick <HashA>..<HashC>
//可以用 两个点号，指定连续的一系列提交（但不包含A）

git cherry-pick <HashA>^..<HashC>
//可以用 ^加两个点号 ，指定连续的一系列提交（包含A）

git cherry-pick --abort
//放弃撷取结果，回退到撷取前的状态
```

## 注意几个问题

- 如果指定的Hash是一个合并出来的节点，那么会失败，因为git不知道应该采用哪个分支的代码变动
    - 办法
        - 使用`-m 1` （表示接受变动的分支）
        - 或者 `-m 2`（表示变动来源的分支）

- 如果出现代码冲突，就会停下来
    - 办法
        - 解决完冲突后，先重新add到暂存区，然后执行`git cherry-pick --continue`

### cherry-pick 可加参数(一)

```css　
--no-commit 撷取后先不要自动提交，简写为-n

--edit 在撷取后有机会编辑自动生成的信息，简写为-e

-x 在提交末尾自动添加cherry picked from...方便追溯
```

