# Git 的常用命令

## 前言

---

### help

显示 Git 的帮助信息

```shell
git help [?command]
```

### log

显示本地仓库的提交记录

```shell
# --oneline 选项表示只显示一行
git log [?options]
```

### init

在所在的 **工作目录** 下初始化一个新的 Git 仓库

```shell
git init
```


### status

查看当前工作目录的修改

```shell
git status
```

### add

把工作区的修改保存到暂存区

```shell
# 目录路径、文件路径、或 '.' 表示所有的
git add [target]
```

### stash

临时保存当前工作目录和暂存区的修改

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

把暂存区的修改保存到本地仓库

```shell
# 提交当前暂存区修改
git commit -m "commit message"

# 提交当前暂存区修改，并覆盖上一次的本地提交
git commit --amend -m "commit message"
```

### push

把本地修改推送到远程仓库，第一次推送时，需要指定远程仓库的名称。

```shell
# 推送到远程仓库的对应分支
git push [remote] [branch]

# 初次推送本地修改，并跟踪远程分支修改
git push --set-upstream [remote] [branch]
```

### pull

从远程仓库拉取修改到本地并合并

```shell
git pull [remote] [branch]

# 拉取本地修改，并使用 rebase 策略合并远程修改
git pull --rebase [remote] [branch]
```

### remote

添加远程存储库

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

列出所有分支，使用指定名称创建一个新分支

```shell
# 列出所有分支
git branch 

# 创建一个新分支
git branch [name]
```

### fetch

从远程仓库拉取修改到本地，但不合并到当前分支

```shell
git fetch [remote] [branch]
```

### checkout

切换到指定分支

```shell
git checkout [branch]

# 切换到某一次提交
git checkout [commit_hash]
```

### merge

合并指定分支到当前分支

```shell
git merge [branch]
```

### reset

重置当前分支到指定提交

```shell
# 将 HEAD、暂存区、工作目录 全部重置 到指定提交
git reset --hard [commit_hash]

# 仅移动 HEAD 指针到指定提交，保留 暂存区和工作目录 的修改
git reset --soft [commit_hash]

# 回退到前 N 个提交（默认使用 --mixed 参数，保留工作目录修改）
git reset HEAD~[?num]
```

### rebase

将当前分支的提交重新应用到另一个基点上（重写提交历史）

- 与 `merge` 的区别: `merge` 保留分支结构，`rebase` 创造线性历史

- 注意: 不要对已推送的提交进行变基（会破坏协作）

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
