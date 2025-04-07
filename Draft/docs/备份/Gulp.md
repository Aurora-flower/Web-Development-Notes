---
title: Gulp
tags: [Gulp]
categories: [Build]
date: 2025-03-10 11:37:05
---

## 引言

> 在 `Gulp 4.x` 中，任务可以是异步的，支持多种处理方式，包括 `Promise`、`async/await`、`Stream` 等。
> 当任务完成时，必须通知 Gulp，否则任务会挂起，导致后续任务无法执行。

Gulp 是基于 Node.js 的任务运行器，使用 **_异步_** 操作来处理文件流。自动化并增强工作流程的工具包。
利用 Gulp 和 JavaScript 的灵活性来自动执行缓慢、重复的工作流，并将其组合成高效的构建管道。

---

### 安装

```shell
# 安装 gulp 命令行工具
npm install --global gulp-cli

# 安装 gulp 作为开发时依赖项
npm install --save-dev gulp

# 验证版本
gulp --version
```

---

### 配置文件

1. 示例

   在项目根目录中创建一个名为 `gulpfile.js` 的文件。任何导出的函数都将被注册到 gulp 的任务系统中。

   ```javascript
   function defaultTask(cb) {
     cb();
   }
   
   /* 默认任务导出 */ 
   exports.default = defaultTask
   ```

   ```shell
   # 执行默认任务
   gulp 
   ```

   **注意📢: 将所有逻辑添加到 gulpfile 中，如果文件太大，可以将其重构为单独的文件。
   每个任务都可以拆分成自己的文件，然后导入到 gulpfile 中进行组合。**

2. **`gulpfile`** 详解

   - `gulpfile` 是项目目录下名为 `gulpfile.js` （或者首字母大写 `Gulpfile.js`）的文件，在运行 `gulp` 命令时会被自动加载。
   - Node 的模块的解析功能允许将 `gulpfile.js` 文件替换为同样命名为 `gulpfile.js` 的目录，
     该目录中包含了一个名为 `index.js` 的文件，该 `index.js` 文件将被当作 `gulpfile.js` 使用。
   - 如果使用了转译器（`transpiler`），需要给文件夹和目录相应地命名。

3. 配置文件转移

   > Node 的大多数新版本都支持 TypeScript 或 Babel 所提供的大多数功能，但 `import`/`export` 语法除外。
   >
   > 如果只需要改语法的话，重命名为 `gulpfile.esm.js` 并安装 [esm](https://www.npmjs.com/package/esm) 模块。

   当使用 TypeScript 或 Babel 编写 gulpfile 文件时，需要进行转译。
   通过修改 `gulpfile.js` 文件的扩展名来表明所用的编程语言并安装对应的转译模块。

   - 对于 TypeScript，重命名为 `gulpfile.ts` 并安装 `ts-node` 模块。
   - 对于 Babel，重命名为 `gulpfile.babel.js` 并安装 `@babel/register` 模块。
   - 使用 ESModule 语法，重命名为 `gulpfile.esm.js` 并安装 `esm` 模块。

   ```shell
   # 安装 ts-node 模块
   npm install --save-dev ts-node
   
   # 安装 @babel/register 模块
   npm install --save-dev @babel/register
   
   # 安装 esm 模块
   npm install --save-dev esm
   ```
