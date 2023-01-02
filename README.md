## 数据类型
> 任何对 NaN 的进一步数学运算都会返回 NaN，只有一个例外：NaN ** 0 结果为 1）。

## 类型转换
### 数字类型转换
|值|转换为|
|--|--|
|undefined|NaN|
|null|0|
|true false|1 0|
|string|去掉空白字符，如果只包含数字直接进行转换，如果字符为空，转换为0，否则返回 NaN|
### 布尔类型转换
|值|转换为|
|--|--|
|0, null, undefined, NaN, ""	|false|
|其他值|true|
### 运算符
> 只要任意一个运算元是字符串，那么另一个运算元也将被转化为字符串。

> 前置形式返回一个新的值，但后置返回原来的值（做加法/减法之前的值）。
## 值的比较
> A-Z 65-90 a-z 97-122 91-96 分别是 [ \ ] ^ _  ` 

> 当使用数学式或其他比较方法 < > <= >= 时： null/undefined 会被转化为数字：null 被转化为 0，undefined 被转化为 NaN。

> undefined 和 null 在相等性检查 == 中不会进行任何的类型转换，它们有自己独立的比较规则，所以除了它们之间互等外，不会等于任何其他的值。
## 函数
> 现代 JavaScript 引擎支持 空值合并运算符 ??，它在大多数假值（例如 0）应该被视为“正常值”时更具优势
```js
function showCount(count) {
  // 如果 count 为 undefined 或 null，则提示 "unknown"
  console.log(count ?? "unknown");
}
```
> 函数应该简短且只有一个功能。如果这个函数功能复杂，那么把该函数拆分成几个小的函数是值得的。
## 变量
> 同一个变量使用 `let` `const` 声明一个已经被声明的变量会触发报错，`SyntaxError: ... has already been declared`, 使用 `var` 可以多次声明。
## 函数表达式
> 函数表达式是在代码执行到达时被创建，并且仅从那一刻起可用。

> 在函数声明被定义之前，它就可以被调用。

> 在大多数情况下，当我们需要声明一个函数时，最好使用函数声明，因为函数在被声明之前也是可见的。这使我们在代码组织方面更具灵活性，通常也会使得代码可读性更高。
