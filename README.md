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

## 空值合并运算符
`a ?? b`
> 如果第一个参数不是 null/undefined，则 ?? 返回第一个参数。否则，返回第二个参数。

> || 返回第一个 真 值。 || 无法区分 false、0、空字符串 "" 和 null/undefined。它们都一样 —— 假值（falsy values）。如果其中任何一个是 || 的第一个参数，那么我们将得到第二个参数作为结果。

> ?? 返回第一个 已定义的 值。

> 如果没有明确添加括号，不能将其与 || 或 && 一起使用。

## 循环
> continue 指令是 break 的“轻量版”。它不会停掉整个循环。而是停止当前这一次迭代，并强制启动新一轮循环（如果条件允许的话）。

## switch 语句
> 如果没有 break，程序将不经过任何检查就会继续执行下一个 case。 

> 共享同一段代码的几个 case 分支可以被分为一组：

> switch/case 有通过 case 进行“分组”的能力，其实是 switch 语句没有 break 时的副作用。

> 这里的相等是严格相等。被比较的值必须是相同的类型才能进行匹配。

## 对象
[zh.javascript.info](https://zh.javascript.info/object)
对象是具有一些特殊特性的关联数组。

### 创建
```js
let user = new Object(); // 构造函数
let user = {}; // 字面量
```

### 访问属性
> 点符号要求 key 是有效的变量标识符。这意味着：不包含空格，不以数字开头，也不包含特殊字符（允许使用 $ 和 _）。

> 使用方括号，可用于任何字符串，计算属性
```js
let key = prompt("What do you want to know about the user?", "name");
console.log(user[key]);
```
> 属性命名没有限制。属性名可以是任何字符串或者 symbol

> 其他类型会被自动地转换为字符串。

> 一个名为 __proto__ 的属性。我们不能将它设置为一个非对象的值：

> 属性名简写：如果属性名和变量名一样，则可以简写。
```js
function makeUser(name, age) {
  return {
    name: name,
    age: age,
  };
}

// 可以简写为以下
function makeUser(name, age) {
  return {
    name,
    age,
  };
}
```

> 属性存在性测试 `in` 操作符，大多数情况可以通过判断属性值是否为`undefined` 判断属性是否存在，因为读取不到的属性只会得到 `undefined`。
> 如果属性存在，但存储的值是 `undefined`，那么此时无法通过上述方法判断，所以要使用 `in` 操作符。

> 为了遍历一个对象的所有键（key），可以使用一个特殊形式的循环：for..in。

> 整数属性会被进行排序，其他属性则按照创建的顺序显示。

> 这里的“整数属性”指的是一个可以在不做任何更改的情况下与一个整数进行相互转换的字符串。

> 为了解决电话号码的问题，我们可以使用非整数属性名来 欺骗 程序。只需要给每个键名加一个加号 "+" 前缀就行了。

### 对象的引用与复制
> 对象与原始类型的根本区别之一是，对象是“通过引用”存储和复制的，而原始类型：字符串、数字、布尔值等 —— 总是“作为一个整体”复制。 

> 使用 const 声明的对象也是可以被修改的

#### 浅层克隆  
> 创建一个新对象，通过遍历已有对象的属性，并在原始类型值的层面复制它们，以实现对已有对象结构的复制。  
``` js
let user = {
  name: "John",
  age: 30
};

let clone = {}; // 新的空对象

// 将 user 中所有的属性拷贝到其中
for (let key in user) {
  clone[key] = user[key];
}

// 现在 clone 是带有相同内容的完全独立的对象
clone.name = "Pete"; // 改变了其中的数据

alert( user.name ); // 原来的对象中的 name 属性依然是 John
```

> 使用 `Object.assign()`  
  `Object.assign(dest, [src1, src2, src3...])`  

> 使用 `spread` 语法：`clone = {...user}`  
### 深层克隆  
> 浅层克隆无法处理属性是对象的情况。  

``` js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);

alert( user.sizes === clone.sizes ); // true，同一个对象

// user 和 clone 分享同一个 sizes
user.sizes.width++;       // 通过其中一个改变属性值
alert(clone.sizes.width); // 51，能从另外一个获取到变更后的结果
```
可以使用 `structuredClone` [参见](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)  

``` js
const mushrooms1 = {
  amanita: ["muscaria", "virosa"],
};

const mushrooms2 = structuredClone(mushrooms1);

mushrooms2.amanita.push("pantherina");
mushrooms1.amanita.pop();

console.log(mushrooms2.amanita); // ["muscaria", "virosa", "pantherina"]
console.log(mushrooms1.amanita); // ["muscaria"]
```
