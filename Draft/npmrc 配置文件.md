---
layout: post
title: .npmrc 配置文件
date: 2025-01-19 22:00
categories: [扩展]
tags: [npm]
---

## 前言

`npmrc` 文件，全称为 `npm running configuration`，是 `npm` 的运行时配置文件。可以通过各种配置选项来定制 `npm`的行为。

这个文件可以位于项目根目录、用户目录或全局目录。不同位置的 `.npmrc` 配置会覆盖其他位置的配置。

常见的配置项包括 **设置代理**、**代理认证**、**缓存路径**、**版本规则**、**日志级别**、以及 **控制版本锁定** 和 **依赖管理** 等。

---

### 代理 (registry) 

`registry`  设置 npm 使用的默认包仓库。例如，将默认仓库改为淘宝镜像，以提高下载速度。  (个人建议使用原镜像。  )  

``` ini 
registry=https://registry.npm.taobao.org/
```

### 请求代理 (proxy)

**`proxy` 和 `https-proxy`**   设置 HTTP 和 HTTPS 请求的代理。如果需要在公司内部网络中使用代理，可以配置这两个选项。(一般使用 proxy)

```ini
proxy=http://proxy.example.com:8080   
https-proxy=https://proxy.example.com:8080
```



### 引擎限制 (engine)



**`engine-strict`**   强制 npm 检查 `package.json` 中的 `engines` 字段，确保所使用的 Node.js 和 npm 版本符合要求。这个选项与 `package.json` 中的 `engines` 配置配合使用。      



```ini
engine-strict=true 
```

### 版本规则 (version)

**`save-exact`**   控制在 `npm install` 时，是否使用精确版本号（例如：`1.2.3`），而不是使用范围（如：`^1.2.3`）。   

``` ini
save-exact=true
```

### 认证 (auth)

**`auth` 和 `always-auth`**   用于配置认证信息（如：私有 `npm registry` 的认证）。

`always-auth` 确保每次 npm 请求都需要认证。 适用于私有注册表（即每次执行 `npm install` 时都要进行认证）。

```ini
//registry.npmjs.org/:_authToken=[token]
always-auth=true
```

 ### 缓存 (cache)

`cache` 设置 npm 使用的缓存目录路径，可以将缓存存储在自定义位置。

```ini
cache=[custom-path]
```

### SSL

**`strict-ssl`** 设置是否启用严格的 SSL 验证。如果在公司内部使用自签名证书，可以关闭 SSL 验证（不推荐）。

```ini
strict-ssl=false
```

### 日志级别

`loglevel` 设置日志级别，控制 npm 输出的详细程度。常用的日志级别有：`silent`, `error`, `warn`, `http`, `info`, `verbose`，`silly`。默认是 `warn`。

```ini
loglevel=verbose
```

### 自定义脚本设置

`scripts-prepend-node-path` 设置是否将 Node.js 添加到 `PATH` 环境变量的前面。通常需要用来确保执行自定义脚本时能够正确使用 Node.js。

```ini
scripts-prepend-node-path=true
```

### package-lock 

`package-lock` 允许或禁止使用 `package-lock.json` 文件（锁定依赖版本）。

`no-package-lock` 禁用 `package-lock.json` 文件的生成和使用。

```ini
package-lock=false
no-package-lock=true
```

### 依赖前缀

设置依赖包版本前缀，指定在 `package.json` 中安装依赖时使用的版本范围符号（`^`, `~`）。

```ini
save-prefix=~
```

### 全局路径

设置全局安装包的路径。你可以改变全局包的安装目录，通常用于避免使用 `sudo` 权限进行全局安装。

```ini
prefix=[global-path]
```



### 全局设置

`global` 设置是否使用全局模式。启用全局模式时，npm 会将所有的安装包安装到全局目录，而不是当前项目中。

```ini
global=true
```

### 依赖安装默认行为

**`save` 和 `save-dev`** 设置是否默认将依赖保存到 `dependencies` 或 `devDependencies`。

`legacy-peer-deps` 使用此选项来跳过 `peerDependencies` 的自动安装。默认情况下，npm 会自动安装 `peerDependencies`，但有时可能会导致冲突，这时可以通过设置此选项来禁用。

```ini
save=true
save-dev=true
legacy-peer-deps=true
```

---

## 补充

### 依赖版本符号

在 `npm` 中，`~` 和 `^` 都是用来指定依赖版本范围的符号

| 符号 | 允许的版本范围                                               |
| ---- | ------------------------------------------------------------ |
| `~`  | 只允许升级补丁版本（例如 `1.2.3` -> `1.2.4`，但不包括 `1.3.0`） |
| `^`  | 允许升级补丁版本和次版本（例如 `1.2.3` -> `1.3.0`，但不包括 `2.0.0`） |





