# git 日志命令

## log查看历史提交记录

```bash
git log
//详细信息

git log --oneline
//简略信息

git log -5
//指定查看数量为5个最新记录

git log --all --grep='keyword'
//在所有提交日志中查找包含 keyword 关键词的提交

git log --author="xxx"
//指定查看作者为xxx的记录
```

## reflog查看操作记录

```bash
git reflog
```
- 会出现`HEAD@{数字}`开头的每行操作，在误操作（比如重置丢失代码）想回去时配合reset命令有奇效

## 查看tag标签

```bash
git tag
```