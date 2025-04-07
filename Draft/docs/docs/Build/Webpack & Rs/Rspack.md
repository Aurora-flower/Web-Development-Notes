# Rspack

## 引言

> webpack 是目前最为成熟的构建工具，有着活跃的生态，灵活的配置和丰富的功能，
> 但是其最为人诟病的是其性能问题，尤其在一些大型项目上，构建花费的时间可能会达到几分钟甚至几十分钟，
> 性能问题是目前 webpack 最大的短板。
> 
> **因此 Rspack 解决的问题核心就是 webpack 的性能问题。**

`Rspack` （读音为 `/'ɑrespæk/`,）是 Rspack 是 **字节跳动** 开发的基于 Rust 编写的高性能 JavaScript 
打包工具，设计上兼容 `Webpack` 的配置结构和插件生态。
它提供对 webpack 生态良好的兼容性，能够无缝替换 webpack，并提供快速的构建速度。

---

## 安装

1. 脚手架

   `Rspack CLI` 是对标 `webpack CLI` 的工具，提供基础的 `serve` 和 `build` 构建命令。

   ```shell
   # Rspack CLI 示例项目
   npm create rspack@latest
   ```

2. 手动安装

   ```shell
   npm install -D @rspack/core @rspack/cli
   ```

3. 配置

    当运行 Rspack 的命令行工具时，Rspack 会自动读取当前路径下的 `rspack.config.*` 文件。
    
    基础的 Rspack 配置文件示例:
    
    ```javascript
    import { defineConfig } from '@rspack/cli';
    
    export default defineConfig({
      entry: {
        main: './src/index.js',
      },
    });
    ```



---

## 配置

### Mode （模式）

- **类型**： `production` | `development` | `none`
- **默认值**：`production`

该选项用于设置 Rspack 的 **_构建模式_** ，以启用对应模式下的默认优化策略。

### Entry （入口）

- **类型**： `string` | `string[]` | `Record<string, string | string[]` | EntryDescription> | Function
- **默认值**：`./src/index.js`

该选项用于设置 Rspack 构建的入口。