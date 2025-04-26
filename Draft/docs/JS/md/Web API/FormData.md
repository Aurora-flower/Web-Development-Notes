# FormData

## 前言

`FormData` 是一个用于构造和操作表单数据的对象，通常用于通过 JavaScript 构建 `HTTP` 请求，
特别是在处理文件上传时非常有用。它模拟了 HTML 表单中的数据，并允许以编程方式创建和提交表单。

主要特点:

- **构造表单数据**: 可以通过 FormData 构造一个表单数据对象，可以从现有的 `<form>` 元素创建，也可以手动添加键值对数据。
- **文件上传**: 支持将文件附加到表单数据中，非常适合实现文件上传的功能。
- **与 fetch 和 XMLHttpRequest 配合使用**: 通常与 `fetch` 或 `XMLHttpRequest` API 配合发送数据到服务器。

---

### FormData 构造函数

form 参数的类型为 `HTMLFormElement` 或 `null`。
这个参数是一个 HTML 表单元素，表示提取表单数据的表单。
如果提供了这个参数，FormData 会自动填充该表单中的所有输入字段（如文本框、选择框、文件上传字段等）的值。
不提供参数，FormData 就是一个空的表单数据对象，之后可以通过编程的方式手动添加数据。

```javascript
new FormData(form);
```

### form 表单元素

```html
<form id="myForm">
  <input type="text" name="username" value="John" />
  <input type="file" name="profilePicture" />
</form>
```

会从 `<form>` 元素中自动提取所有输入字段的值，并将其存储在 `FormData` 对象中。

```javascript
const form = document.getElementById("myForm");
const formData = new FormData(form);

// 使用 Fetch API 提交表单数据
fetch("/submit", {
  method: "POST",
  body: formData
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

### 手动创建 FormData 对象并添加数据

```javascript
const formData = new FormData();
formData.append("username", "John");
formData.append("age", 30);

// 创建一个 XMLHttpRequest 请求，发送数据
const xhr = new XMLHttpRequest();
xhr.open("POST", "/submit", true);
xhr.send(formData);
```

### FormData 的常用方法

1. **`append(name, value)`**

   - 用于向 `FormData` 对象添加一个新的字段或更新现有字段的值。
   - **参数**:
     - `name`: 字段的名称。
     - `value`: 字段的值，可以是字符串、`Blob` 对象或 `File` 对象。

   示例:

   ```javascript
   formData.append("username", "John");
   formData.append("profilePicture", fileInput.files[0]);
   ```

2. **`delete(name)`**

   - 删除指定名称的字段。
   - **参数**:
     - `name`: 要删除的字段的名称。

   示例:

   ```javascript
   formData.delete("username");
   ```

3. **`get(name)`**

   - 获取指定名称的字段的值。
   - **参数**:
     - `name`: 字段的名称。

   示例:

   ```javascript
   const username = formData.get("username");
   console.log(username); // 'John'
   ```

4. **`has(name)`**

   - 检查是否存在指定名称的字段。
   - **参数**:
     - `name`: 字段的名称。

   示例:

   ```javascript
   if (formData.has("username")) {
     console.log("Username is present.");
   }
   ```

5. **`set(name, value)`**

   - 设置指定名称的字段的值。如果该字段已经存在，则会更新其值。
   - **参数**:
     - `name`: 字段的名称。
     - `value`: 字段的新值。

   示例:

   ```javascript
   formData.set("username", "Jane");
   ```

6. **`forEach(callback)`**

   - 遍历 `FormData` 中的所有字段，并对每个字段执行回调函数。
   - **参数**:
     - `callback`: 回调函数，接受以下参数:
       - `value`: 字段的值。
       - `name`: 字段的名称。
       - `formData`: 当前的 `FormData` 对象。

   示例:

   ```javascript
   formData.forEach((value, name) => {
     console.log(`${name}: ${value}`);
   });
   ```
