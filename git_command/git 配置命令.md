# git 配置命令

## 安装

- macOS
    ```bash
    brew install git
    ```
    - 配置在目录`~/.gitconfig`下

## 配置用户名和邮箱

```bash
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.com"
```

## 查看配置信息

```bash
git config --global -l  //全局配置
git config --system -l  //系统级配置
git config --local -l  //仓库级配置
```
- 出现"冒号"可输入空格继续查看下一页
- 出现<END>可输入q退出

## 配置ssh密钥

```bash
ssh-keygen -a 100 -t ed25519 -f ~/.ssh/github_ed25519 -C "your_email@youremail.com"
```
- 登录github官网，右上角Settings -> 左栏点击 SSH and GPG keys -> 点击 New SSH key

- 打开用户目录下的.ssh/github_ed25519.pub，复制其中的内容，粘贴到文本域

## 验证ssh密钥

```bash
ssh -T git@github.com
```
