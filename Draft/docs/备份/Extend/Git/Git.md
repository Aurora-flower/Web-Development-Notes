# Git

## 前言

---

### fetch

> fetch 是从远程仓库拉取最新版本的代码到本地仓库的操作。但是，不会将这些代码合并到当前分支中。

```shell
git fetch [remote-repo] [branch]
```

---

### push

```shell
# 初次本地提交，设置远程耿总分支
git push --set-upstream [remote-repo] [branch]
```

---

### clone

```shell
# 克隆远程仓库的指定分支到指定目录
git clone -b [branch] [remote-repo] [local-dir]
```

---

## 相关链接