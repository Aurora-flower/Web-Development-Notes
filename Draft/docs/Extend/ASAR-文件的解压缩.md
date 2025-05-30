# ASAR 文件的解压缩

## 引言

> ASAR（`Archive for ASar`）归档是一种专为 Electron 应用设计的简单扩展存档格式。
> 它旨在缓解 Windows 平台上的长路径名问题，提升`require`速度，并保护源代码不被轻易修改。

- ASAR 通过将文件夹结构打包成一个二进制文件，简化了 Electron 应用的资源文件管理。
  这种格式便于分发和部署应用，同时也提供了性能和安全性方面的改善。
- 使用 ASAR 格式的主要好处包括减少文件数量和大小，加快文件访问速度。
  在 Electron 应用中，由于模块加载机制，使用 ASAR 格式可以减少文件 I/O 操作，从而提高`require`速度。
- ASAR 格式通过打包资源文件，可以防止用户直接修改应用的内部文件，从而提高安全性。
  然而，这并不意味着 ASAR 提供了高级别的安全防护，有经验的用户或攻击者仍然可能找到绕过的方法。

---

### 安装

```shell
# 全局安装
npm install -g asar

# 局部安装
npm install -D asar
```

---

---

### 常用命令

#### 解压缩

1. **解压**:

   ```shell
   #  extract|e <archive>(asar 文件) <dest>(目标解压文件夹)
   asar extract [archive] [dest]
   ```

2. **压缩**:

   ```shell
   #  pack|p [options] <dir>(目标解压文件夹) <output>(asar 文件)
   asar pack [dir] [output]
   ```

#### 其他命令

1. **列出归档文件与目录**:

   ```shell
   #  list|l [options] <archive>(asar 文件)
   asar list [archive]
   ```

2. **提取单个文件**:

   ```shell
   #  extract-file|ef <archive> <filename>(目标文件)
   asar extract-file [archive] [filename]
   ```

---

## 相关链接 🔗

- [Electron 官网 - 中文 - Asar 归档](https://electron.nodejs.cn/docs/latest/tutorial/asar-archives/)
