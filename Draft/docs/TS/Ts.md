# TypeScript

## 引言

`TypeScript` 是 `JavaScript` 的超集，通过添加静态类型系统和面向对象编程特性，旨在解决 JavaScript 在大型项目中存在的类型松散、代码维护困难等问题。

其核心优势包括:

- **静态类型检查**:

  编译时捕捉类型错误，减少运行时崩溃风险。

- **代码可读性**:

  类型注解可以明确变量、函数参数和返回值的用途，有助于开发者理解代码的意图，提升团队协作效率，并让代码更易于维护。

- **生态兼容性**:

  完全兼容 JavaScript，支持渐进式迁移，，降低了学习和转换成本

- **面向对象编程特性**:

  TypeScript 提供了类、接口、继承、泛型等面向对象编程（OOP）的特性，使得开发者能够编写更符合现代开发范式的代码。

---

### 原始类型

- `boolean`: 布尔值，`true` 或 `false`。
- `number`: 数字，包括整数与浮点数。
- `string`: 字符串。
- `tuple`: 元组，固定长度和类型的数组，例如: `[number, string]`。
- `enum`: 枚举，定义一组命名的常量。
- `any`: 任何类型，可以赋值给任何变量。尽量避免使用，因为使用它会失去类型检查的优势。
- `void`: 没有返回值，通常用于函数。
- `null`: 空值。
- `undefined`: 未定义的值。
- `never`: 永不存在的值的类型，例如抛出异常的函数。
- `object`: 非原始类型，例如对象、数组和函数。
- `unkown`: unknown 是一种类型，它表示任何值的类型，但与 any 类型不同，它要求在使用之前进行类型检查。

---

### 联合类型与字面量

```typescript
const name: 'typescript' | 'javascript' = 'typescript';
```

---

### 枚举

定义命名常量集合，增强代码可读性

```typescript
enum Language  { ZH, EN };
const language: Language = Language.ZH;
```

---

### 函数类型与接口 - 规范代码的 "契约"。

1. 函数类型

   指定参数和返回值类型，避免意外行为。

    ```typescript
    function add(x: number, y: number): number {
        return x + y
    }
    ```

2. 接口

   定义对象结构，强制实现一致性。

    ```typescript
    interface User {
        /* 只读属性 */
        readonly id: number
        
        name: string
        username: string
        password: string
        
        /* 可选属性 */
        age?: number
        
        /* 广泛定义 */ 
        [key: string]: unknown
    }
    
    const user: User = {
        id: 802,
        name: '花楹一间',
        username: 'huaying',
        password: '123456789',
        age: 18,
        skill: 'code'
    };
    ```

---

### 类与面向对象编程 - 代码的 "组织艺术"

1. 类与继承

   支持 `public`、`private`、`protected` 访问修饰符。

    ```typescript
    class Animal {
        constructor(public name: string) {
        }
        
        move() {
            console.log('name:', this.name);
        }
    }
    
    class Dog extends Animal {
        bark() {
            console.log('woof!');
        }
    }
    ```

2. 实现接口

通过接口约束类行为。

```typescript
interface Loggable {
    log(): void
}

class Logger implements Loggable {
    log(): void {
        console.log('Log...')
    }
}
```

---

### 高级类型与工具 - 解锁高阶玩法

#### 泛型

泛型（Generics）是一种用于创建可重用组件的强大工具。它使得能够在定义函数、类、接口等时，提供一种方式来指定类型，而不需要预先指定具体的类型。

基本语法: 泛型使用尖括号 `<>` 来定义。

典型场景:
- **集合操作**：例如数组、链表等的操作，可以使用泛型来定义通用的集合处理函数。
- **表单处理**：在表单处理中，可能需要处理不同类型的字段和验证逻辑，泛型能够帮助保持类型安全并且避免重复代码。
- **API 请求响应**：对于不同的 API 请求，响应可能是不同的类型，泛型可以帮助处理不同类型的请求和响应。


- **泛型函数**

  在函数中，泛型允许在函数的参数和返回值中使用类型占位符

    ```typescript
    function identity<T>(id: T): T {
      return id
    }
    const id = identity(802); // 调用时，自动推断为 number 类型
    ```

- **泛型接口**

  泛型接口允许定义可以接受不同类型的函数签名或方法。

    ```typescript
    interface GenericIdentityFn<T> {
        (arg: T): T;
    }
    
    const identityFn: GenericIdentityFn<number> = (arg) => arg;
    ```

- **泛型类**

  类也可以使用泛型，这使得可以创建针对不同类型的实例化对象。

```typescript
class GenericBox<T> {
    value: T;

    constructor(value: T) {
        this.value = value;
    }

    getValue(): T {
        return this.value;
    }
}

let boxNumber = new GenericBox<number>(123);
```

- **泛型约束**

  使用 `extends` 关键字来实现泛型约束，对泛型添加一些限制，确保符合特定的结构。

    ```typescript
    interface Person { 
        name: string 
    }
    
    // 泛型约束：T 必须是一个包含 name 属性的对象
    function greet<T extends Person>(person: T): string {
        return `Hello, ${person.name}`;
    }
    
    const person = { name: "John", age: 30 };
    console.log(greet(person));
    ```

- **默认泛型类型**

  可以为泛型提供一个默认类型，如果调用时没有提供类型参数，则使用默认类型。

    ```typescript
    function wrap<T = string>(value: T): T {
        return value;
    }
    console.log(typeof wrap(123));
    ```

- 泛型的多个类型参数

  可以为泛型函数、接口或类指定多个类型参数。

    ```typescript
    function merge<T, U>(object1: T, object2: U): T & U {
        return { ...object1, ...object2 };
    }
    
    const merged = merge({ name: "John" }, { age: 30 });
    console.log(merged);  // 输出 { name: 'John', age: 30 }
    ```

- 使用 `keyof` 和 `in` 限制泛型

    ```typescript
    // keyof 限制：T 必须是一个对象类型，并且 key 需要是对象的键
    function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
        return obj[key];
    }
    
    const person = { name: "John", age: 30 };
    console.log(getValue(person, "name"));  // 输出 "John"
    ```

#### 类型别名与交叉类型

```typescript
type Person = { name: string };
type Developer = Person & { expertise: string };
```

#### 类型断言

可以通过类型断言强制将一个值转换为特定的类型，而 TypeScript 不会对其进行进一步的类型检查。

- **尖括号语法**（只在 TSX 中不可用）

    ```typescript
    let someValue: unknown = "Hello, world!";
    const len: number = (<string>input).length;
    ```   

- **`as` 语法**（推荐）

    ```typescript
    const input: unknown = 'hello world!';
    const len: number = (input as string).length;
    ```

#### 类型守卫

类型守卫是 TypeScript 提供的一种方式，用于细化类型检查，并确保某个变量的类型符合预期。

类型守卫通常会使用 `typeof`、`instanceof` 或自定义的类型保护函数来做类型判断。

- **`typeof` 类型守卫**

  `typeof` 运算符用于判断原始类型（如 string、number、boolean、symbol、undefined）。

    ```typescript
    function printLength(value: string | number) {
        if (typeof value === "string") {
            console.log(value.length); // `value` 在这里被推断为 `string` 类型
        } else {
            console.log(value.toFixed(2)); // `value` 在这里被推断为 `number` 类型
        }
    }
    ``` 

- **`instanceof` 类型守卫**

  `instanceof` 运算符用于检查某个对象是否是某个类的实例，通常用来检查类的实例。

    ```typescript
    class Dog {
        bark() {
            console.log("Woof!");
        }
    }
    
    class Cat {
        meow() {
            console.log("Meow!");
        }
    }
    
    function makeSound(animal: Dog | Cat) {
        if (animal instanceof Dog) {
            animal.bark();  // `animal` 被推断为 `Dog` 类型
        } else {
            animal.meow();  // `animal` 被推断为 `Cat` 类型
        }
    }
    
    ```

---

### TS 项目配置文件

```json5
/*
tsconfig.json
@link https://www.tslang.cn/docs/handbook/compiler-options.html
@link https://www.typescriptlang.org/tsconfig/
*/
{
  /* 继承其他配置 */
  //   "extends": "",

  /* 编译器选项 */
  "compilerOptions": {
    /* 
        启用严格模式 - 启用所有严格类型检查选项
        启用 --strict 相当于启用:
        --noImplicitAny, 
        --noImplicitThis, 
        --alwaysStrict,
        --strictNullChecks,
        --strictFunctionTypes,
        --strictPropertyInitialization
    */
    "strict": true,

    /* 禁用函数参数双向协变检查 */
    // "strictFunctionTypes": true,

    /* 在表达式和声明上有隐含的 any 类型时报错 */
    // "noImplicitAny": true,

    /* 当 this 表达式的值为 any 类型的时候，生成一个错误 */
    // "noImplicitThis": true,

    /* 以严格模式解析并为每个源文件生成 "use strict"语句 */
    // "alwaysStrict": true,

    /* 确保类的非 undefined 属性已经在构造函数里初始化若要令此选项生效，需要同时启用 --strictNullChecks */
    // "strictPropertyInitialization": true,

    /* 
        在严格的 null 检查模式下， null 和 undefined 值不包含在任何类型里，
        只允许用它们自己和 any来赋值（有个例外， undefined可以赋值到 void） 
    */
    // "strictNullChecks": true,

    /* 不对具有  @internal JSDoc 注解的代码生成代码 (实验性) */
    // "stripInternal": false,

    /* 重定向输出目录 */
    // "outDir": "",

    /* 仅用来控制输出的目录结构 */
    // "rootDir": "",

    /* 
        根（root）文件夹列表，表示运行时组合工程结构的内容 (tsconfig.json 配置)
        @link https://www.tslang.cn/docs/handbook/module-resolution.html#virtual-directories-with-rootdirs
    */
    // "rootDirs": [],

    /* 
        将输出文件合并为一个文件
        合并的顺序是根据传入编译器的文件顺序和 ///<reference``>和 import的文件顺序决定的 
        只有 "AMD"和 "System"能和 --outFile一起使用
    */
    // "outFile": "",

    /* 指定 ECMAScript 目标版本 - 指示 TypeScript 编译器生成符合指定标准的代码。 */
    "target": "ESNext",

    /* 是否允许编译 javascript 文件 */
    "allowJs": false,

    /* 启用 javascript 检查 - 与 allowJs 配合使用 */
    // "checkJs": false,

    /* 启用 ES 模块与 CommonJS 模块之间的相容性特性 */
    "esModuleInterop": true,

    /* 指定类型声明文件所在位置 - 要包含的类型声明文件路径列表 */
    "typeRoots": ["./types", "./node_modules/@types"],

    /* 指定包含的 @types 类型 - 要包含的类型声明文件名列表 */
    // "types": ["node", "express", "react", "react-dom", "react-router-dom"],

    /* 允许不报告执行不到的代码错误 */
    "allowUnreachableCode": true,

    /* 允许不报告未使用的标签错误 */
    "allowUnusedLabels": true,

    /* 若有未使用的局部变量则抛错 */
    "noUnusedLocals": true,

    /* 若有未使用的参数则抛错 */
    "noUnusedParameters": true,

    /* 解析非相对模块名的基准目录 */
    "baseUrl": ".",

    /* 生成相应的 .d.ts文件 */
    "declaration": true,

    /* 生成声明文件的输出路径 */
    // "declarationDir": "dist/types",

    /* 显示诊断信息 */
    "diagnostics": true,

    /* 显示详细的诊段信息 */
    "extendedDiagnostics": true,

    /* 禁用 JavaScript 工程体积大小的限制 */
    // "disableSizeLimit": false,

    /* 在输出文件的开头加入 BOM 头（UTF-8 Byte Order Mark） */
    // "emitBOM": false,

    /* 给源码里的装饰器声明加上设计类型元数据 (实验性) */
    // "emitDecoratorMetadata": false,

    /* 启用 ES 装饰器(实验性) */
    "experimentalDecorators": true,

    /* 
        禁止对同一个文件的不一致的引用
        文件名完全匹配，要求所有的导入语句中的文件路径（包括模块和类型声明文件）必须与实际文件系统中的文件名大小写完全匹配
    */
    "forceConsistentCasingInFileNames": true,

    /* 从 tslib 导入辅助工具函数（比如 __extends， __rest等） */
    // "importHelpers": false,

    /* 
        启用 JSX
        @link https://www.tslang.cn/docs/handbook/jsx.html
    */
    "jsx": "react",

    /* 指定生成目标为 react JSX 时，使用的 JSX 工厂函数，比如 React.createElement 或 h */
    "jsxFactory": "React.createElement",

    /* 生成单个 sourcemaps 文件，而不是将每 sourcemaps 生成不同的文件 */
    // "inlineSourceMap": false,

    /*  将代码与 sourcemaps 生成到一个文件中，要求同时设置了 --inlineSourceMap 或 --sourceMap 属性 */
    // "inlineSources": false,

    /* 将每个文件作为单独的模块 */
    "isolatedModules": true,

    /* 
        编译过程中需要引入的库文件的列表
        默认注入的库为:
        ► 针对于--target ES5：DOM，ES5，ScriptHost
        ► 针对于--target ES6：DOM，ES6，DOM.Iterable，ScriptHost
    */
    "lib": [
      "ESNext",
      "DOM",
      "DOM.Iterable",
      "WebWorker",
      "ScriptHost"
    ],

    /* 不使用默认的库文件 */
    "noLib": false,

    /* 打印出编译后生成文件的名字 */
    // "listEmittedFiles": false,

    /* 编译过程中打印文件名 */
    // "listFiles": false,

    /*
        为调试器指定指定 sourcemap 文件的路径，而不是使用生成时的路径
        当 .map 文件是在运行时指定的，并不同于 js 文件的地址时使用这个标记
        指定的路径会嵌入到 sourceMap 里告诉调试器到哪里去找它们 
    */
    // "mapRoot": "./map",

    /* 生成相应的 .map文件 */
    "sourceMap": true,

    /* 
        指定 TypeScript 源文件的路径，以便调试器定位
        当 TypeScript 文件的位置是在运行时指定时使用此标记
        路径信息会被加到 sourceMap里 
    */
    // "sourceRoot": "./src",

    /* 生成 .d.ts 文件相应的 map 映射文档 */
    // "declarationMap": true,

    /* 
        node_modules 依赖的最大搜索深度并加载 JavaScript 文件
        仅适用于 --allowJs 
    */
    // "maxNodeModuleJsDepth": 0,

    /* 指定生成（输出）目标模块系统代码 target === "ES6" ? "ES6" : "commonjs" */
    "module": "ESNext",

    /* 指定模块解析策略 - 决定如何处理模块 module === "AMD" or "System" or "ES6" ? "Classic" : "Node" */
    "moduleResolution": "node",

    /* 当生成文件时指定行结束符： "crlf"（windows）或 "lf"（unix） */
    "newLine": "lf",

    /* 不生成输出文件 */
    // "noEmit": false,

    /* 不在输出文件中生成用户自定义的帮助函数代码，如 __extends */
    // "noEmitHelpers": false,

    /* 报错时不生成输出文件 */
    "noEmitOnError": true,

    /* 不截短错误消息 */
    // "noErrorTruncation": false,

    /* 
        报告switch语句的fallthrough错误
        （即，不允许 switch 的 case 语句贯穿）
        在 switch 语句中，如果一个 case 后面没有 break 并且直接跟着另一个 case，编译器会发出错误 
    */
    "noFallthroughCasesInSwitch": true,

    /* 
        不是函数的所有返回路径都有返回值时报错
        在函数体中检查是否存在返回值，如果一个函数缺少显式的返回语句，或者某个执行路径没有返回值，TypeScript 将会发出警告或错误
    */
    "noImplicitReturns": true,

    /* 模块输出中不包含 "use strict"指令 */
    // "noImplicitUseStrict": false,

    /* 不把 /// <reference``>或模块导入的文件加到编译文件列表 */
    // "noResolve": false,

    /* 禁用在函数类型里对泛型签名进行严格检查 */
    // "noStrictGenericChecks": false,

    /* 	
        模块名到基于 baseUrl 的路径映射的列表 (tsconfig.json 配置)
        @link https://www.tslang.cn/docs/handbook/module-resolution.html#path-mapping
    */
    "paths": {
      //   "@e/*": ["./electron/*"],
      //   "@s/*": ["./src/*"],
      //   "@/*": ["./electron/*", "./src/*"]
    },

    /* 保留 const 和 enum 声明 */
    // "preserveConstEnums": false,

    /* 不把符号链接解析为其真实路径；将符号链接文件视为真正的文件 */
    // "preserveSymlinks": false,

    /* 保留 watch 模式下过时的控制台输出 */
    // "preserveWatchOutput": false,

    /* 给错误和消息设置样式，使用颜色和上下文 (实验性) */
    // "pretty": false,

    /* 
        编译指定目录下的项目
        这个目录应该包含一个 tsconfig.json 文件来管理编译 
    */
    // "project": "",

    /* 当目标为生成 "react" JSX时，指定 createElement 和 __spread 的调用对象 */
    // "reactNamespace": "React",

    /* 删除所有注释，除了以 /!*开头的版权信息 */
    "removeComments": true,

    /* 忽略库的默认声明文件的类型检查 */
    "skipDefaultLibCheck": true,

    /* 忽略所有的声明文件（ *.d.ts）的类型检查 */
    "skipLibCheck": true

    /* 阻止对对象字面量的额外属性检查 (实验性) */
    // "suppressExcessPropertyErrors": false,

    /* 阻止对缺少的属性检查 - 阻止 --noImplicitAny 对缺少索引签名的索引对象报错 */
    // "suppressImplicitAnyIndexErrors": false,

    /* 生成模块解析日志信息 */
    // "traceResolution": false
  }

  /* 指定编译的文件范围 */
  //   "include": ["source/**/*"],

  /* 排除不需要编译的文件夹 */
  //   "exclude": ["node_modules", "backup", "app"]
}
```

---

---

## 相关链接🔗

- [Ts 官网文档 - 中文](https://www.tslang.cn/)

