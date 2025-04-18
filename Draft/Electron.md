# Electron

## 前言

Electron 是一个框架，使开发者能够将 Web 技术(HTML、JavaScript、CSS、Web Assembly)、[Node.js](https://nodejs.org/) 及原生代码相结合，（内部嵌入 [Chromium](https://www.chromium.org/) ）构建适用于 macOS、Windows 和 Linux 的跨平台桌面应用程序。

---

### 使用场景

**嵌入轻量级网站**： Electron 应用通常以 Web 应用为主，只在必要时嵌入一些原生代码。 计算密集型的 Electron 应用往往采用 HTML/CSS 编写 UI，而用 Rust、C++ 或其他原生语言构建后端。

### 初始化项目

Electron 应用基于 npm 搭建，以 `package.json` 文件作为入口点。*author*、*license* 和 *description* 可以是任何值，但在稍后的打包过程中是必需的。

在 package.json 中指定的 `main` 文件是 Electron 应用的入口。 这个文件控制 **主程序 (main process)**，它运行在 Node.js 环境里，负责控制您应用的生命周期、显示原生界面、执行特殊操作并管理渲染器进程 (renderer processes)。

