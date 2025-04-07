# Uni-App

## 前言

`uni-app` 简单来说是 **vue 的语法** + **小程序的 api**。
一个 `uni-app` 工程，就是一个 `Vue` 项目。
`uni-app` 代码编写，基本语言包括 `js`、`vue`、`css`，以及 `ts`、`scss` 等 `css` 预编译器。


---

### 安装与创建

除了 `HBuilderX` 可视化界面，也可以使用 `cli` 脚手架，可以通过 `vue-cli` 创建 `uni-app` 项目工程。

1. 创建 `vue3` 项目
   
   ```shell
   # 创建以 javascript 开发的工程
   npx degit dcloudio/uni-preset-vue#vite my-vue3-project # 正式版
   
   npx degit dcloudio/uni-preset-vue#vite-alpha my-vue3-project # alpha 版
   
   # 创建以 typescript 开发的工程
   npx degit dcloudio/uni-preset-vue#vite-ts my-vue3-project
   ```
   
   注意📢:
   - `Vue3/Vite` 版要求 `node` 版本  18+、20+

2. 创建 `vue2` 项目

   ```shell
   # 正式版 - 对应 HBuilderX 最新正式版
   vue create -p dcloudio/uni-preset-vue my-project
   
   # alpha 版  - 对应 HBuilderX 最新 alpha 版
   vue create -p dcloudio/uni-preset-vue#alpha my-alpha-project
   ```

---

### 更新依赖到指定版本

可以使用 `@dcloudio/uvm` 管理编译器的版本，此工具仅自动增加或更新 `uni-app` 编译器主要依赖。


```shell
# 更新到最新正式版
npx @dcloudio/uvm@latest

# 更新到最新 Alpha 版
npx @dcloudio/uvm@latest alpha

# 更新到正式版指定版本
npx @dcloudio/uvm@latest 3.2.0
```