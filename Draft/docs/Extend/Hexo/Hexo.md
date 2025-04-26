# Hexo

## 前言

> Hexo 是一个快速、简洁且高效的博客框架。
>
> Hexo 使用 Markdown（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

优点:

- **超快速度**: Node.js 所带来的超快生成速度。 上百个页面在几秒内完成渲染。
- **一键部署**: 只需一条指令即可部署到 `GitHub Pages`, `Heroku` 或其他平台。
- **支持 Markdown**: Hexo 支持 `GitHub Flavored Markdown` 的所有功能，甚至可以整合 `Octopress` 的大多数插件。
- **插件**: 支持数种模板引擎（`EJS`，`Pug`，`Nunjucks`等）。 可以与现有的 NPM 包 (`Babel`, `PostCSS`, `Less/Sass` 等) 轻松地集成。

---

### 安装与初始化

1. 安装

   ```shell
   # 全局安装（命令工具）
   npm install hexo-cli -g

   # 局部安装（hexo 包）
   npm install hexo

   # 执行 hexo 命令
   npx hexo [command]
   ```

2. 初始化

   ```shell
   hexo init blog
   ```

---

### 创建新文章

```shell
hexo new "我的新文章"
```

更多信息: [Writing](https://hexo.io/docs/writing.html)

---

### 使用草图

草图是未发布的文章，可以通过以下命令查看和发布草图:

```shell
# 创建草稿
hexo draft "草稿标题"

# 生成包含草稿的静态文件以预览
hexo generate --draft

# 发布草稿
hexo publish draft 草稿文件ID
```

---

### 启动服务器

```shell
hexo server
```

更多信息: [Server](https://hexo.io/docs/server.html)

---

### 生成静态文件

```shell
hexo generate
```

更多信息: [Generating](https://hexo.io/docs/generating.html)

---

### 部署到远程站点

```shell
hexo deploy
```

更多信息: [Deployment](https://hexo.io/docs/one-command-deployment.html)
