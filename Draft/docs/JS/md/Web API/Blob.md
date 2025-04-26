# Blob

## 前言

`Blob`（Binary Large Object）是用于表示原始数据的类，Blob 表示`二进制大对象`（Binary Large Object），
它可以包含任意数据，通常用于存储图片、音频、视频或其他文件类型。它在浏览器的 Web API 中非常常见。

注意 📢: Node.js 本身并不原生支持 `File` 或 `Blob` 对象，而是使用 `Buffer` 来处理二进制数据。

---

###

```typescript
new Blob(["Hello, world!"], { type: "text/plain" });
```
