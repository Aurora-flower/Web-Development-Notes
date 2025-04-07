# 断言（Assert）

## 前言

`node:assert` 模块提供了一组用于验证不变量的断言函数。

---

### 严格断言模式

- 在严格断言模式下，非严格方法的行为与其对应的严格方法相同。

- 在严格断言模式下，对象的错误消息显示差异。在旧版断言模式下，对象的错误消息显示对象，通常被截断。



严格模式的使用:

```javascript
// 方式一
const assert = require('node:assert').strict;

// 方式二
const assert = require('node:assert/strict');
```



