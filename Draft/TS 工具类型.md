# TypeScript 中的工具类型

## 前言

在 TypeScript 中，有许多实用的工具类型（Utility Types）帮助简化代码，特别是处理对象类型时，`Partial`、`Omit` 和类似的工具类型非常常用。

用于操作类型的内置类型，帮助开发者进行类型变换、构造新类型或限制现有类型的属性。这些工具类型极大简化了类型操作和变换的工作。

---

以下是 TypeScript 中常见的工具类型及其详细说明：

### 1. `Partial<T>`
**功能：** 将类型 `T` 的所有属性变为可选属性。

**用法：**
```typescript
interface Person {
  name: string;
  age: number;
}

const partialPerson: Partial<Person> = {
  name: "Alice"
};
```
**说明：** `Partial<T>` 使得 `Person` 类型中的 `name` 和 `age` 属性都变为可选，意味着你可以只提供部分属性。

### 2. `Required<T>`
**功能：** 将类型 `T` 的所有属性变为必需的属性。

**用法：**
```typescript
interface Person {
  name?: string;
  age?: number;
}

const person: Required<Person> = {
  name: "Alice",
  age: 25
};
```
**说明：** `Required<T>` 强制所有属性都变为必需，即使原本是可选的属性，也会变成必需。

### 3. `Readonly<T>`
**功能：** 将类型 `T` 的所有属性变为只读属性。

**用法：**
```typescript
interface Person {
  name: string;
  age: number;
}

const readonlyPerson: Readonly<Person> = {
  name: "Alice",
  age: 25
};

// Error: Cannot assign to 'name' because it is a read-only property.
readonlyPerson.name = "Bob";
```
**说明：** `Readonly<T>` 使得 `Person` 类型中的 `name` 和 `age` 属性变为只读，意味着你不能修改这些属性的值。

### 4. `Record<K, T>`
**功能：** 构造一个对象类型，键 `K` 的类型和值 `T` 的类型。

**用法：**
```typescript
type PersonInfo = Record<string, number>;

const info: PersonInfo = {
  Alice: 25,
  Bob: 30
};
```
**说明：** `Record<K, T>` 用于创建一个对象类型，所有键 `K` 对应的值都是类型 `T`。

### 5. `Pick<T, K>`
**功能：** 从类型 `T` 中选取一部分属性 `K`，构造一个新类型。

**用法：**
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type NameAndAge = Pick<Person, 'name' | 'age'>;

const person: NameAndAge = {
  name: "Alice",
  age: 25
};
```
**说明：** `Pick<T, K>` 根据给定的属性 `K` 创建一个新类型，包含 `T` 类型中的部分属性。

### 6. `Omit<T, K>`
**功能：** 从类型 `T` 中排除某些属性 `K`，构造一个新类型。

**用法：**
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type PersonWithoutAddress = Omit<Person, 'address'>;

const person: PersonWithoutAddress = {
  name: "Alice",
  age: 25
};
```
**说明：** `Omit<T, K>` 创建一个新类型，移除了类型 `T` 中的属性 `K`。

### 7. `Exclude<T, U>`
**功能：** 从类型 `T` 中排除 `U` 类型的所有成员。

**用法：**
```typescript
type Status = "success" | "error" | "pending";
type NonSuccessStatus = Exclude<Status, "success">; // "error" | "pending"
```
**说明：** `Exclude<T, U>` 会从 `T` 类型中去除与 `U` 类型相交的成员，返回一个新类型。

### 8. `Extract<T, U>`
**功能：** 提取 `T` 类型中与 `U` 类型相交的成员。

**用法：**
```typescript
type Status = "success" | "error" | "pending";
type SuccessStatus = Extract<Status, "success" | "error">; // "success" | "error"
```
**说明：** `Extract<T, U>` 提取出 `T` 和 `U` 类型之间的交集，返回一个新类型。

### 9. `NonNullable<T>`
**功能：** 排除类型 `T` 中的 `null` 和 `undefined`。

**用法：**
```typescript
type T1 = string | null | undefined;
type T2 = NonNullable<T1>; // string
```
**说明：** `NonNullable<T>` 会从类型 `T` 中去除 `null` 和 `undefined`，返回一个新类型。

### 10. `Awaited<T>`
**功能：** 如果类型 `T` 是 `Promise` 类型，提取出 `Promise` 内部的类型。

**用法：**
```typescript
type PromiseType = Promise<string>;
type ResolvedType = Awaited<PromiseType>; // string
```
**说明：** `Awaited<T>` 用来提取 `Promise<T>` 的解析结果类型。

### 11. `Infer`
**功能：** 用于条件类型中推断类型。

**用法：**
```typescript
type MyReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
```
**说明：** `infer` 用于条件类型的推断，通常用来提取函数返回类型或其他嵌套类型。

### 12. `ThisType<T>`
**功能：** 用于在对象字面量中标记 `this` 的类型。

**用法：**
```typescript
interface MyInterface {
  name: string;
  greet(): void;
}

const obj: MyInterface & ThisType<{ message: string }> = {
  name: "Alice",
  greet() {
    console.log(this.message);
  },
  message: "Hello"
};
```
**说明：** `ThisType<T>` 在对象中使用，指明 `this` 的类型。

---

这些工具类型在 TypeScript 中非常常用，能够帮助开发者在编写类型时减少重复代码，提升开发效率。掌握这些工具类型，将会大大提高 TypeScript 的类型安全性和灵活性。
