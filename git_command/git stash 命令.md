# git stash 命令

## 压存 当前分支已修改的内容

```bash
git stash
```

如果需要自定义备注，用下面的命令

```bash
git stash save "自定义名字" 
```

## 查看目前已压存的列表

```bash
git stash list
```

出现内容为:
```bash
stash@{0}: WIP on 分支名: 哈希前9位
stash@{1}: WIP on ...
stash@{2}: WIP on ...
```
或者
```bash
stash@{0}: On 分支名: 自定义备注
```


## 弹出 最近一次 压存的内容

```bash
git stash pop
```
默认是弹出0号


## 弹出 任意一次 压存的内容

```bash
git stash pop stash@{n}
```
其中n是上面列表中的编号

如果是自定义备注，还是要找到编号，备注只不过是方便你辨认哪个是你需要的


## 删除 任意一次 压存的内容

```bash
git stash drop stash@{n}
```
