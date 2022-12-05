# git merge命令

## merge合并别人开发的other分支整个

```css
git merge other
//会自动生成合并信息

git merge -m "合并后的节点提交信息" other
//可用-m参数自己指定合并信息

git merge --abort
//放弃合并结果，回退到合并前的状态
```


### merge可加参数(一)

```css
--no-commit 合并后先不要自动提交
反之--commit合并后提交

--edit 在合并后有机会编辑自动生成的信息
反之--no-edit略过编辑
```

### merge可加参数(二)

```css
【当本分支master无修改（很少遇到）】
eg：master：C1 ← C2
　　　　　　　　　↑
　　 other：　　　C3 ← C4
      
--ff 默认选项，全称fast-forward模式
直接快进移动本分支master指针到other分支上，不产生新的commit节点
代价是本分支不干净，混进了很多other的提交记录
master：C1 ← C2 ← C3 ← C4
 other：C1 ← C2 ← C3 ← C4
 
--ff-only选项
仅在可快进移动时合并，这种情况ok，结果同上

--no-ff选项
再产生一个新的commit节点，继承自other分支，只添加了简单的merge记录
master：C1 ← C2 ← C3 ← C4 ← C6(merge记录) 
 other：C1 ← C2 ← C3 ← C4

--squash选项 压缩模式 与--no--ff冲突
压缩other分支的多个节点内容，形成新的单一节点
好处是本分支干净，不含other多余的提交记录
master：C1 ← C2 ← C6(含C3和C4内容，但丢失other的提交记录) 
 other：C1 ← C2 ← C3 ← C4
```

### merge可加参数(三)
```css
【当本分支有修改出C5】
eg：master：C1 ← C2 ← C5
　　　　　　　　　↑
　　 other：　　　C3 ← C4

--ff 默认选项，fast-forward模式
无法触发快进移动
master：C1 ← C2 ← C3 ← C4 ← C5 ← C6 (解决冲突的那次提交)
 other：C1 ← C2 ← C3 ← C4
 
--ff-only选项
无法快进移动，取消合并

--no-ff选项
结果同--ff，上面的无法触发就等于no-ff

--squash 
master：C1 ← C2 ← C5 ← C6 (解决冲突的那次提交)
 other：C1 ← C2 ← C3 ← C4
```