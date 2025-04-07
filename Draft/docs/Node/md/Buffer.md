# Buffer

## 引言

`Buffer` 类是 `Node.js` 提供的一个全局对象，它类似于 `ArrayBuffer`，用于处理原始二进制数据。

主要特点: 
1. **在 Node.js 中用于处理二进制数据**: `Buffer` 使得 Node.js 可以高效地处理和操作原始二进制数据。
2. **不可变**: 一旦创建，`Buffer` 的内容不能被修改，它会在内存中保持原始数据。
3. **广泛用于 I/O 操作**: 例如，文件读取、网络请求和响应等，都经常使用 `Buffer` 来处理原始数据流。

---
### Buffer 构造函数 (已废弃)

`new Buffer()` 方法以前用于创建一个新的 `Buffer` 对象，它的行为根据不同的参数而有所不同: 

- **不带参数**: 创建一个零长度的 Buffer。
- **带一个数字参数**: 创建一个指定大小（字节数）的 Buffer，并且它的内容未被初始化，可能包含不安全的数据。
- **带一个字符串参数**: 将给定的字符串转换为 Buffer 对象。
- **带一个 Array 或 ArrayBuffer 参数**: 用给定的数据创建 Buffer。

```javascript
const buffer1 = new Buffer(10); // 创建一个 10 字节的 Buffer，内容未初始化
const buffer2 = new Buffer('Hello, World!', 'utf8'); // 从字符串创建 Buffer
```

注意📢: 由于 `new Buffer()` 存在内存未初始化的问题，尤其在大多数情况下它可能创建未初始化的内存区域，
这些内存中可能包含敏感数据，因此存在安全风险（比如泄露敏感信息）。
因此，Node.js 从 `v6.0.0` 开始弃用了 `new Buffer()`。
使用 `Buffer.alloc()` 和 `Buffer.from()` 可以确保内存的安全管理，避免潜在的安全漏洞。

### Buffer.alloc(size)

创建一个指定大小的 `Buffer`，并且所有字节都会初始化为零，保证了内存的安全。

```javascript
const buffer = Buffer.alloc(10); // 创建一个 10 字节的 Buffer，内容初始化为 0
```

### Buffer.from(array)

将给定的数组或 `ArrayBuffer` 转换为一个新的 `Buffer` 对象。

```javascript
const buffer = Buffer.from([1, 2, 3, 4, 5]); // 从数组创建 Buffer
```

### Buffer.from(string, encoding)

将给定的字符串和编码格式转换为 Buffer。

```javascript
const buffer = Buffer.from('Hello, World!', 'utf8'); // 从字符串创建 Buffer，指定编码格式
```


### Buffer 与 ArrayBuffer

`fs.readFile` 是 `Node.js` 中用于读取文件内容的异步方法，返回的结果类型通常是 `Buffer`。
返回的 Buffer 可以看作是对 ArrayBuffer 的一个封装，Buffer 继承了 ArrayBuffer，并提供了更多用于操作和处理二进制数据的 API。

```javascript
const fs = require('fs');

// 异步读取文件 
fs.readFile('example.txt', (err, data) => {
  if (err) throw err;

  // data 是一个 Buffer 对象
  console.log(data); // 输出 Buffer 对象
  console.log(data.buffer); // 获取底层的 ArrayBuffer
  console.log(data.toString()); // 输出文件内容作为字符串
});
```