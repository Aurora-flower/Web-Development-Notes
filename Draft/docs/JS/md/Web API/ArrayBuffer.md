# ArrayBuffer

## 引言

`ArrayBuffer` 是一种表示固定长度原始二进制数据的通用对象(**容器** 或 **数据缓冲区**)。
在 JavaScript 中，它用于表示原始的内存块，但不能直接操作数据。
可以通过其他视图（**views** - 如 `Uint8Array`）来操作 ArrayBuffer 中的数据。

---

### 应用场景

- **处理文件上传和下载**:

  通过 ArrayBuffer 可以读取和写入文件内容，进行文件上传或下载时，浏览器使用 ArrayBuffer 来存储和处理文件数据。

- **WebSockets**:

  在使用 WebSockets 进行二进制数据传输时，ArrayBuffer 可以存储传输的数据，并能高效地进行操作。

- **音频和视频处理**:

  如 Web Audio API 或 WebRTC，处理音频和视频流时，ArrayBuffer 是底层数据存储的主要工具。

- **图像处理**:

  例如处理图片数据，ArrayBuffer 可以用来存储图像的像素数据，然后通过视图将数据转换为可以显示的格式。

- **加密和解密**:

  在浏览器端进行加密或解密操作时，可以通过 ArrayBuffer 存储原始二进制数据。

### ArrayBuffer 构造函数

```javascript
/* 创建一个 16 字节的 ArrayBuffer */
let buffer = new ArrayBuffer(16);

/*  输出 ArrayBuffer 中存储的数据的字节长度 */
console.log(buffer.byteLength);
```

### ArrayBufferView 接口

`ArrayBufferView` 是一个接口，表示能够直接操作 `ArrayBuffer` 中数据的对象。
`ArrayBufferView` 本身不是一个直接创建的对象，而是通过具体的视图类型来实现的，用于对 `ArrayBuffer` 进行高效的数据访问。

#### 常见的 `ArrayBufferView` 类型

- `TypedArray` - 它们是表示二进制数据的数组，可以方便地读取和写入数据。
  - `Uint8Array`（无符号 8 位整数）
  - `Uint16Array`（无符号 16 位整数）
  - `Uint32Array`（无符号 32 位整数）
  - `Int8Array`（有符号 8 位整数）
  - `Int16Array`（有符号 16 位整数）
  - `Int32Array`（有符号 32 位整数）
  - `Float32Array`（32 位浮动点数）
  - `Float64Array`（64 位浮动点数）
- `DataView` - 提供更底层、灵活的访问方法，可以按照任意类型读取和写入数据。

这些视图对象允许以不同的方式（如按字节、按 16 位、按 32 位等）访问 ArrayBuffer 中的数据。

#### Uint8Array 示例

```javascript
// 创建一个 8 字节的 ArrayBuffer
const buffer = new ArrayBuffer(8);

// 使用 Uint8Array 视图访问这个 ArrayBuffer
const uint8View = new Uint8Array(buffer);

// 写入数据 - Uint8Array 用于处理 8 位无符号整数（字节数据）
uint8View[0] = 100;
uint8View[1] = 200;
```
