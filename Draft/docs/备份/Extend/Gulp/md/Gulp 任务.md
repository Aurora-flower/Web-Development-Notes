# Gulp Task

## 前言

> 任何导出的函数都将被注册到 gulp 的任务系统中。

每个 `gulp` 任务都是一个异步 `JavaScript` 函数 - 接受 `错误优先回调` 或
返回 `流`、`promise`、`事件触发器`、`子进程`或 `可观察对象的` **函数**。

**注意📢:
由于某些平台限制，不支持同步任务，尽管有一个非常漂亮的 `alternative`（可替代的）。**

---

### 私有任务与公有任务

任务可以被视为 **公共** 或 **私有**。

- 公共任务从 `gulpfile` 中导出，这允许它们通过 gulp 命令运行。
- 私有任务供内部使用，通常用作 `series()` 或 `parallel()` 组合的一部分。

私有任务的外观和行为与任何其他任务类似，但终端用户无法独立执行它。

---

### 任务注册

#### `gulpfile` 导出

任何导出的函数都将被注册到 gulp 的任务系统中。

```javascript
function test(cb) {
    cb()
}

exports.test = test
```

#### task API 注册
    
- **命令行**

```shell
gulp --task
```

- **`task()` 函数**

```javascript
async function dev() {
    console.log('dev task done...');
}

task('dev', dev);
```

过去，`task()` 用于将函数注册为任务。
虽然该 API 仍然可用，但导出应该是主要的注册机制，除非在导出不起作用的边缘情况下。
