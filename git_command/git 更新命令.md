# git 更新命令

## clone克隆远程仓库,可指定分支名

```bash
git clone <远程仓库地址> -b <分支名称>
//不指定的话就默认master
```

## fetch拉取远程仓库更新

```bash
git fetch <远程主机名>
//拉取所有远程分支的变更，但不更改本地对应分支
```

## pull拉取远程仓库更新并合并

```bash
git pull
//相当于fetch+merge，但只是对当前所在的分支merge
```

## 自建本地仓库初始化

```bash
git init
```

## 修改本地仓库对应的远程仓库url

- 查看目前远程仓库url
    ```bash
    git remote -v
    ```

- 把https地址改成git形式地址，便于使用ssh自动验证
    ```bash
    git remote set-url origin git@github.com:账户名/仓库名.git
    ```
    - 也可以自己修改`.git/config`文件

