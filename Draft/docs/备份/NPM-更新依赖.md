---
layout: post
title: NPM-更新依赖
date: 2024-07-07 08:11:41
tags:
---

### 更新单个依赖

```
npm update <dependency_name>
```

### 更新所有的依赖项

1. **确保 npm 是最新版本**：

```shell
npm install -g npm@latest
```

2. **清理缓存（可选）**：

```shell
npm cache clean --force
```

_Tip: 清理 npm 的缓存有时可以帮助解决一些依赖项安装时的问题。_

3. **更新依赖项**：

```shell
npm update

# 更新所有的依赖项到最新主要版本（Major version）
npm update --major
```

Tip: 将会更新所有的依赖项到符合 `package.json` 中指定版本规则的最新版本。

4. **检查和解决冲突**：

   更新依赖项后，可能会出现依赖项之间的冲突或不兼容性。确保在更新后进行测试，查看项目是否仍然正常工作，并解决任何新出现的问题。
