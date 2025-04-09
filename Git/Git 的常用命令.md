# Git 的常用命令

## 前言

Git 命令是用来与 Git 仓库交互的工具，常见的操作包括创建仓库、提交更改、查看历史、合并分支等。Git 的命令行操作是 Git 的核心。

PS：本文未详细列出 Git 命令的所有选项，仅介绍了常用的操作方式。更多详细信息请使用 git help 命令查看。

---

### help

显示 Git 的帮助信息

```shell
git help [?command]
```

### init

用于创建一个新的 Git 仓库，通常用于将现有项目转换为 Git 仓库。

**行为**: 在所在的 **工作目录** 下初始化一个新的 Git 仓库。

```shell
git init
```

### clone

克隆一个远程仓库到本地，通常用于获取远程项目的副本。

```
git clone [?-b [branch]] [reop-path] [?folder]
```

### log

查看提交历史。它列出了所有提交记录，包括作者、时间和提交信息。

```shell
# --oneline 选项表示只显示一行
git log [?options]
```

### status

查看当前工作目录和暂存区的状态。用来查看哪些文件已更改、哪些文件已暂存、哪些文件未追踪。

```shell
git status
```

### diff

显示工作目录与暂存区之间的差异，或者显示提交之间的差异。

```
git diff [commit-hash]
```

### clean

清理未跟踪的文件或目录。

```shell
git clean [file] -f
```

### add

将工作区的修改添加到暂存区，准备提交。这个命令告诉 Git 想提交哪些更改。

```shell
# 目录路径、文件路径、或 '.' 表示所有的
git add [target]
```

### stash

将未提交的更改保存到栈中，稍后可以恢复。这对于中途切换分支时非常有用。

**行为**: 临时保存当前工作目录和暂存区的修改

```shell
# 将当前修改（包括暂存区和工作目录的修改）存储到栈中，并回到最新的提交状态
git stash

# 恢复最近一次的 stash 并将其从栈中删除
git stash pop

# 恢复最近一次的 stash，但不会从栈中删除
git stash apply

# 列出所有保存的 stash
git stash list

# 删除指定的 stash
git stash drop <stash@{n}>

# 删除所有 stash
git stash clear
```

### commit

提交暂存区的更改，生成一个新的提交记录，通常会附带提交信息。

**行为**: 把暂存区的修改保存到本地仓库，并未上传到远程仓库。

```shell
# 提交当前暂存区修改
git commit -m "commit message"

# 提交当前暂存区修改，并覆盖上一次的本地提交
git commit --amend -m "commit message"
```

### push

将本地的更改推送到远程仓库，通常是将本地提交上传到共享仓库。第一次推送时，需要指定远程仓库的名称。

```shell
# 推送到远程仓库的对应分支
git push [remote] [branch]

# 初次推送本地修改，并跟踪远程分支修改
git push --set-upstream [remote] [branch]
```

### pull

从远程仓库拉取最新的更改并与本地合并。

```shell
git pull [remote] [branch]

# 拉取本地修改，并使用 rebase 策略合并远程修改
git pull --rebase [remote] [branch]
```

### remote

管理远程仓库，包括查看、添加或删除远程仓库。远程仓库通常是团队共享的版本库。

```shell
# 显示远程存储库的配置
git remote -v

# 添加远程存储库
git remote add [remote] [url]

# 删除远程存储库
git remote rm [remote]

# 修改远程存储库的 URL
git remote set-url [remote] [url]

# 重命名远程存储库
git remote rename [old] [new]
```

### branch

查看本地的所有分支，或创建新的分支。分支是 Git 的核心概念之一，允许在多个开发路径上并行工作。

```shell
# 列出所有分支
git branch 

# 创建一个新分支
git branch [name]
```

### fetch

从远程仓库获取最新的更改，但不自动合并，可以先查看更改后再决定如何合并。

```shell
git fetch [remote] [branch]
```

### checkout

切换分支，或者恢复文件到某个历史版本。

```shell
git checkout [branch]

# 切换到某一次提交
git checkout [commit_hash]
```

### merge

将其他分支的更改合并到当前分支。

```shell
git merge [branch]
```

### reset

撤销暂存区的更改或历史提交，常用于撤销某些操作或回退到之前的状态。

**行为**: 重置当前分支到指定提交。

```shell
# 将 HEAD、暂存区、工作目录 全部重置 到指定提交
git reset --hard [commit_hash]

# 仅移动 HEAD 指针到指定提交，保留 暂存区和工作目录 的修改
git reset --soft [commit_hash]

# 回退到前 N 个提交（默认使用 --mixed 参数，保留工作目录修改）
git reset HEAD~[?num]
```

### rebase

将一个分支的更改移到另一个分支上，它可以帮助保持清晰的提交历史。

**行为**: 将当前分支的提交重新应用到另一个基点上（重写提交历史）

- 与 `merge` 的区别: `merge` 保留分支结构，`rebase` 创造线性历史

- **注意**: 不要对已推送的提交进行变基（会破坏协作）

```shell
# 将当前分支变基到目标分支（常用于同步上游修改）
git rebase [target_branch]

# 交互式变基（合并多个本地提交，可修改、合并、删除提交）
git rebase -i [commit_hash]

# 解决冲突后继续变基操作
git rebase --continue

# 跳过引发冲突的提交（慎用）
git rebase --skip

# 终止变基操作（恢复到变基前状态）
git rebase --abort
```

### tag

查看、创建或删除标签。标签用于标记特定的提交点，通常用于发布版本。

详情查看: [Git 标签操作](./标签操作.md)
