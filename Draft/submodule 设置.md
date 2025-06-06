# Git 子仓库（Submodules）

## 引言

Git 子模块（Submodule）是指在一个 Git 仓库中嵌套另一个 Git 仓库。
当克隆一个包含子模块的仓库时，子模块会被视为独立的仓库，并且需要单独进行初始化和更新。
这对于管理依赖关系或者将多个独立的项目组合在一起非常有用。


应用场景:

- **管理外部依赖**: 当使用其他仓库作为项目的一部分时，可以通过子模块来引入。
- **多仓库管理**: 在开发过程中，不同的组件或模块可能存放在不同的仓库中，可以通过子模块来管理。

---
### 添加子模块 


```shell
git submodule add <repository_url> [<path>]
```

```markdown
## 添加子模块

在你的 Git 仓库中，使用以下命令来添加一个子模块: 

- `<repository_url>`: 子模块仓库的 URL 地址。
- `<path>`: 指定子模块存放的路径。如果省略，子模块会默认存放在当前目录下。

例如: 

```shell
git submodule add https://github.com/some/repo.git external/repo
```

这会将 `repo.git` 仓库作为子模块添加到 `external/repo` 目录。

## 4. 克隆包含子模块的仓库

当你克隆一个包含子模块的 Git 仓库时，需要使用以下命令来初始化并更新子模块: 

```shell
git clone --recurse-submodules <repository_url>
```

如果已经克隆了仓库，并且忘记初始化子模块，可以使用以下命令: 

```shell
git submodule update --init --recursive
```

## 5. 更新子模块

当子模块的内容发生变化时，更新子模块可以确保你获取到最新版本。

```shell
git submodule update --remote
```

此命令会根据子模块的配置（通常是某个特定分支）更新子模块。

## 6. 提交对子模块的更改

1. 进入子模块目录: 

   ```shell
   cd <submodule_path>
   ```

2. 进行代码修改并提交: 

   ```shell
   git add .
   git commit -m "Update submodule"
   ```

3. 返回主仓库并提交对子模块的引用更改: 

   ```shell
   cd ..
   git add <submodule_path>
   git commit -m "Update submodule reference"
   ```

## 7. 删除子模块

要删除子模块，可以按以下步骤操作: 

1. 删除子模块的记录: 

   ```shell
   git submodule deinit <submodule_path>
   git rm <submodule_path>
   ```

2. 清理 `.gitmodules` 文件和 `.git/config` 中的子模块配置。

3. 删除子模块的物理文件夹: 

   ```shell
   rm -rf <submodule_path>
   ```

4. 提交更改: 

   ```shell
   git commit -m "Remove submodule"
   ```

## 8. 注意事项

- **子模块的独立性**: 子模块本身是一个独立的 Git 仓库，你可以在其中进行独立的提交、分支等操作。
- **子模块的版本控制**: 子模块的更新不会自动同步到主仓库中，你需要手动更新子模块的引用。
- **跨仓库协作**: 如果多个团队协作使用 Git 子模块，可能会遇到子模块不同步的问题，因此需要确保大家都正确更新子模块。

## 9. 常见命令总结

- **添加子模块**: `git submodule add <repository_url> [<path>]`
- **初始化并更新子模块**: `git submodule update --init --recursive`
- **更新子模块**: `git submodule update --remote`
- **删除子模块**: `git submodule deinit <submodule_path>`
- **查看子模块状态**: `git submodule status`
