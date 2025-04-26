# Vue3-Vite 模板的 Uni-app 引入 TailwindCSS

## 前言

根据 `cli` 创建 Uni-app 项目后，希望使用 TailwindCSS。

---
### 安装 tailwindcss (V3 版本)

Vite 自身已经集成 PostCSS，无需再次安装。
Vite 将自动在 `*.vue` 文件中所有的 `style` 标签以及所有导入的 `.css` 文件中应用 PostCSS。

```shell
# 安装依赖 (这里不需要 autoprefixer)
npm install -D tailwindcss 

# 会自动创建 tailwind.config.js 与 postcss.config.js 文件
npx tailwindcss init -p 
```

---

### 配置 tailwind.config.js

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
	  "./src/**/*.{vue,css}"
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

---

### 配置 vite.config.js

无需单独创建 PostCSS 配置文件，直接配置 `css.postcss` 选项即可。

```javascript
import { defineConfig } from "vite";
import tailwindcss from "tailwindcss";
import uni from '@dcloudio/vite-plugin-uni';

export default defineConfig({
    // ...其他一些配置
    plugins: [uni()],
    css: {
        postcss: {
            plugins: [tailwindcss()],
        }, 
    },
});
```

---

### 引入 tailwindcss 指令



```vue
<!-- App.vue -->
<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
```

注意📢:
如果是小程序，建议注释掉 `@import 'tailwindcss/base'`;
因为 Tailwind 的 base 模块中包含了一些使用 `*` 选择器的样式，这在小程序中会导致错误。
