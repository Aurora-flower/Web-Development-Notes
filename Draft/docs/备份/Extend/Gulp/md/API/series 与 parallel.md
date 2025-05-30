# Gulp API - series 与 parallel

## 前言

Gulp 提供了两种强大的组合方法，`series()` 和 `parallel()`，允许将单个任务组合成更大的操作。
两种方法都接受 **任意数量** 的 _任务函数_ 或 _组合_ 操作，并且可以自行嵌套或彼此嵌套 **任意深度**。

---

### series - 顺序执行

`series()` 函数接受一个或多个任务函数，返回一个任务函数，该任务函数将按顺序依次调用这些任务函数。

---

### parallel - 并发执行

`parallel()` 函数接受一个或多个任务函数，返回一个任务函数，该任务函数将并行调用这些任务函数。

