# File

`File` 是 `Blob` 的一个**子类**，表示用户本地文件。通常是通过文件输入框 (<input type="file">) 获取用户选择的文件。

注意📢: Node.js 本身并不原生支持 `File` 或 `Blob` 对象，而是使用 `Buffer` 来处理二进制数据。

---

###

```typescript
new File(['Hello, world!'], 'hello.txt', { type: 'text/plain' });
```