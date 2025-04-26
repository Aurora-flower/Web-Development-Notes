`patch-package` 是一个工具，允许你在项目中修改 `node_modules` 中的第三方库，并且把这些修改持久化为补丁文件（`.patch`）。这样，你在进行项目更新或重新安装依赖时，`patch-package` 会自动重新应用这些修改。这个工具对于处理那些不能通过常规方式解决的第三方库 bug 或不满足需求的情况特别有用。

### 安装和基本使用

1. **安装 `patch-package`**

   你需要首先安装 `patch-package` 和 `postinstall-postinstall`。后者是确保补丁在每次安装依赖后自动应用的工具。

   ```bash
   npm install patch-package postinstall-postinstall --save-dev
   ```

2. **配置 `package.json`**

   在 `package.json` 文件中添加一个 `postinstall` 钩子，确保每次安装后补丁都会被自动应用。

   ```json
   {
     "scripts": {
       "postinstall": "patch-package"
     }
   }
   ```

   这会在每次运行 `npm install` 或 `yarn install` 时自动调用 `patch-package`，并应用所有的补丁。

### 使用 `patch-package` 修改第三方库

1. **修改第三方库**

   找到你需要修改的第三方库所在的目录。通常这些库位于 `node_modules` 目录下。然后直接编辑你想修改的文件。

   比如，如果你要修改 `node_modules/some-package/someFile.js` 中的代码，直接编辑这个文件。

2. **创建补丁文件**

   在完成修改后，你可以使用 `patch-package` 创建补丁文件。运行以下命令：

   ```bash
   npx patch-package <package-name>
   ```

   例如，假设你修改了 `some-package`，你可以运行：

   ```bash
   npx patch-package some-package
   ```

   这将生成一个 `.patch` 文件，通常保存在 `patches/` 目录中，文件名类似于 `some-package+<version>.patch`。

3. **查看补丁文件**

   你可以在 `patches/` 文件夹中查看生成的 `.patch` 文件，里面包含了你对库所做的修改。

   ```bash
   patches/some-package+<version>.patch
   ```

   该文件内容会描述你对库中代码所做的所有更改。

4. **应用补丁文件**

   每次你执行 `npm install` 或 `yarn install` 时，`postinstall` 钩子会自动运行 `patch-package`，它会在安装依赖后应用所有存在的补丁文件。

   如果你只想手动应用补丁，而不重新安装依赖，你可以使用：

   ```bash
   npx patch-package
   ```

### 其他常用命令

- **检查补丁**

  如果你修改了 `node_modules` 中的文件，且想要确认补丁是否需要重新应用，可以通过以下命令来查看差异：

  ```bash
  npx patch-package --list
  ```

  它会列出哪些依赖包已经被修改，并需要补丁。

- **移除补丁**

  如果你想移除某个依赖的补丁，可以删除相应的 `.patch` 文件，或者运行：

  ```bash
  npx patch-package --remove <package-name>
  ```

  这将从 `patches/` 目录中删除指定库的补丁文件。

### 示例

假设你在 `node_modules/react-native` 中发现了一个 bug，想要修改它，并保存该修改为补丁。

1. 进入 `node_modules/react-native`，找到并修改文件。
2. 运行 `npx patch-package react-native`，这将会创建一个补丁文件，比如 `patches/react-native+0.64.0.patch`。
3. 之后，每次安装依赖时，`patch-package` 会自动将这些修改重新应用到 `react-native` 中。

### 需要注意的事项

- **补丁兼容性**：如果你修改的库版本发生了变化，生成的补丁可能会失效。你需要确保库版本和补丁版本保持一致。
- **Git 版本控制**：你应该将 `patches/` 目录添加到版本控制中（如 Git），这样其他开发者在获取代码时，也能应用相同的补丁。

### 总结

`patch-package` 是一个非常强大的工具，能够帮助你在不修改第三方库源代码的情况下修复 bug 或调整功能。通过生成和管理 `.patch` 文件，你可以在多次安装和更新中保留自定义的更改。