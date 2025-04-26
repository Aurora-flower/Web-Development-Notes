# FileReader

## 前言

`FileReader` 是一个浏览器提供的接口（**专门为浏览器环境设计的**），用于异步地读取用户本地文件的内容。
通常与 `<input type="file">` 元素一起使用。它支持读取多种格式的数据，
包括文本、二进制数据、Data URL 等，并且非常适用于文件上传或处理本地文件的场景。

---

### `FileReader` 的主要方法和参数

#### 1. **`FileReader.readAsText(file, encoding)`**
该方法用于将文件内容读取为文本。

- `file`：要读取的文件对象（通常是通过 `<input type="file">` 获取的）。
- `encoding`（可选）：指定文件的字符编码，默认为 UTF-8。如果未指定，它会自动使用默认编码。

**示例：**
```javascript
const file = document.querySelector('input[type="file"]').files[0];
const reader = new FileReader();
reader.onload = function(event) {
  console.log('文件内容：', event.target.result);  // 输出文件的文本内容
};
reader.readAsText(file);
```

#### 2. **`FileReader.readAsDataURL(file)`**
该方法用于将文件读取为 Data URL，通常用于显示图像或音频文件的预览。

- `file`：要读取的文件对象。

**示例：**
```javascript
const file = document.querySelector('input[type="file"]').files[0];
const reader = new FileReader();
reader.onload = function(event) {
  console.log('文件的 Data URL：', event.target.result);  // 输出 Data URL，通常用于图片预览
};
reader.readAsDataURL(file);
```

#### 3. **`FileReader.readAsArrayBuffer(file)`**
该方法将文件读取为原始二进制数据（`ArrayBuffer`），常用于处理二进制文件（如音频或视频文件）。

- `file`：要读取的文件对象。

**示例：**
```javascript
const file = document.querySelector('input[type="file"]').files[0];
const reader = new FileReader();
reader.onload = function(event) {
  console.log('文件的二进制数据：', event.target.result);  // 输出文件的二进制数据
};
reader.readAsArrayBuffer(file);
```

#### 4. **`FileReader.readAsBinaryString(file)`**（已废弃）
该方法以前用于将文件读取为二进制字符串，但由于安全原因，现代浏览器已经不推荐使用该方法，建议使用 `readAsArrayBuffer` 来代替。

---

### `FileReader` 的事件
- `onload`：当文件读取成功时触发。
- `onerror`：当文件读取失败时触发。
- `onloadstart`：在文件读取开始时触发。
- `onloadend`：在文件读取完成时触发（无论成功或失败）。

**示例：**
```javascript
const file = document.querySelector('input[type="file"]').files[0];
const reader = new FileReader();
reader.onload = function(event) {
  console.log('读取完成:', event.target.result);
};
reader.onerror = function(event) {
  console.error('读取错误:', event.target.error);
};
reader.readAsText(file);
```