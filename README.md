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

### 对象方法,this
[zh.javascript.info](https://zh.javascript.info/object-methods)  
> this 的值是在代码运行时计算出来的，它取决于代码上下文。  
  
> 严格模式下的 this 值为 undefined。  
  
> 在非严格模式的情况下，this 将会是 全局对象  
  
> 箭头函数有些特别：它们没有自己的 this。如果我们在这样的函数中引用 this，this 值取决于外部“正常的”函数。  
  
> 以“方法”的语法调用函数时：object.method()，调用过程中的 this 值是 object。  

``` js
let user = {
  name: "Hehoku",
  age: 18,
  sayHi() {
    let arrow = () => console.log(this.name);
    arrow();
  },
  sayHiInObject: function () {
    console.log(this.name);
  },
  arrowFunction: () => console.log(this)
};

function sayHi() {
  console.log(this.name);
}

user.sayHi = sayHi;

user.sayHi(); // Hehoku

user.arrowFunction(); // undefined
```

### 构造器和操作符 "new"
[zh.javascript.info](https://zh.javascript.info/constructor-new)
> 当一个函数被使用 new 操作符执行时，它按照以下步骤： 
1. 一个新的空对象被创建并分配给 this。 
2. 函数体执行。通常它会修改 this，为其添加新的属性。 
3. 返回 this 的值。

> 构造器的主要目的 —— 实现可重用的对象创建代码。

> 从技术上讲，任何函数（除了箭头函数，它没有自己的 this）都可以用作构造器。

> “首字母大写”是一个共同的约定，以明确表示一个函数将被使用 new 来运行。

> 在一个函数内部，我们可以使用 new.target 属性来检查它是否被使用 new 进行调用了。 对于常规调用，它为 undefined，对于使用 new 的调用，则等于该函数

### 可选链 `?.`
obj?.prop —— 如果 obj 存在则返回 obj.prop，否则返回 undefined。
obj?.[prop] —— 如果 obj 存在则返回 obj[prop]，否则返回 undefined。
obj.method?.() —— 如果 obj.method 存在则调用 obj.method()，否则返回 undefined。

### 数字类型
> 如果我们想直接在一个数字上调用一个方法，比如上面例子中的 toString，那么我们需要在它后面放置两个点 ..。

> 值 “NaN” 是独一无二的，它不等于任何东西，包括它自身：

> 它们可以从字符串中“读取”数字，直到无法读取为止。如果发生 error，则返回收集到的数字。函数 parseInt 返回一个整数，而 parseFloat 返回一个浮点数：

> Math.random() 返回一个从 0 到 1 的随机数（不包括 1）

### 字符串
| 方法      | 选择方式 | 负值参数 |
| ----------- | ----------- | ----------- |
| `slice(start, end)` | 从 start 到 end，不含 end | 允许 |
| `substring(start, end) | 从 start 到 end，不含 end | 负值被视为 0 |
| `substr(start, length)` | 从 start 开始获取长为 length 的字符串 | 允许 start 为负数 |

> `str.repea(n)` 重复字符串 n 次

### 数组
[zh.javascript.info](https://zh.javascript.info/array)
> 数组是存储有序的集合

> arr.at(i)： 
>   
>   如果 i >= 0，则与 arr[i] 完全相同。 
>   对于 i 为负数的情况，它则从数组的尾部向前数。

> 队列 queue 是最常见的使用数组的方法之一。在计算机科学中，这表示支持两个操作的一个有序元素的集合： 
>   
>   push 在末端添加一个元素
>   shift 取出队列首端的一个元素，整个队列往前移，这样原先排第二的元素现在排在了第一。

> 数据结构 栈。 
>  它支持两种操作： 
>   
>   push 在末端添加一个元素. 
>   pop 从末端取出一个元素.

> shift 
>    
>    
>    取出数组的第一个元素并返回它：

> unshift 
>    
>    
>    在数组的首端添加元素：

> 数组是一种特殊的对象。

> 数组真正特殊的是它们的内部实现。JavaScript 引擎尝试把这些元素一个接一个地存储在连续的内存区域，就像本章的插图显示的一样，而且还有一些其它的优化，以使数组运行得非常快。

> 如果我们不像“有序集合”那样使用数组，而是像常规对象那样使用数组，这些就都不生效了。

> 数组误用的几种方式: 
>   
>   添加一个非数字的属性，比如 arr.test = 5。 
>   制造空洞，比如：添加 arr[0]，然后添加 arr[1000] (它们中间什么都没有)。 
>   以倒序填充数组，比如 arr[1000]，arr[999] 等等。

> push/pop 方法运行的比较快，而 shift/unshift 比较慢。

> for..of 不能获取当前元素的索引，只是获取元素值

> 技术上来讲，因为数组也是对象，所以使用 for..in 也是可以的：

> for..in 循环会遍历 所有属性，不仅仅是这些数字属性。

> for..in 循环适用于普通对象，并且做了对应的优化。但是不适用于数组，因此速度要慢 10-100 倍。

> 通常来说，我们不应该用 for..in 来处理数组。 
>  

> 当我们修改数组的时候，length 属性会自动更新。准确来说，它实际上不是数组里元素的个数，而是最大的数字索引值加一。 
>  

> length 属性的另一个有意思的点是它是可写的。 
>  

> 如果我们手动增加它，则不会发生任何有趣的事儿。但是如果我们减少它，数组就会被截断。该过程是不可逆的

> 清空数组最简单的方法就是：arr.length = 0;。

> 如果使用单个参数（即数字）调用 new Array，那么它会创建一个 指定了长度，却没有任何项 的数组。 
>  

> 数组有自己的 toString 方法的实现，会返回以逗号隔开的元素列表。 
>  

> 数组没有 Symbol.toPrimitive，也没有 valueOf，它们只能执行 toString 进行转换，所以这里 [] 就变成了一个空字符串，[1] 变成了 "1"，[1,2] 变成了 "1,2"。
>
```js
alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```

### 数组方法
[zh.javascript.info](https://zh.javascript.info/array-methods)
> `arr.splice(start[, deleteCount, elem1, ..., elemN])`
> 
> 它从索引 start 开始修改 arr：删除 deleteCount 个元素并在当前位置（如果没有删除，就是在当前位置之前）插入 elem1, ..., elemN。最后返回被
> 删除的元素所组成的数组。

> `arr.slice([start], [end])`
>   
>  它会返回一个新数组，将所有从索引 start 到 end（不包括 end）的数组项复制到一个新的数组。start 和 end 都可以是负数

> 也可以不带参数地调用它：arr.slice() 会创建一个 arr 的副本。

> arr.concat 创建一个新数组，其中包含来自于其他数组和其他项的值。 
>  

> 如果类数组对象具有 Symbol.isConcatSpreadable 属性，那么它就会被 concat 当作一个数组来处理：此对象中的元素将被添加：

> indexOf 和 includes 使用严格相等 === 进行比较。

> 方法 includes 的一个次要但值得注意的特性是，它可以正确处理 NaN，这与 indexOf 不同： 

> find 方法搜索的是使函数返回 true 的第一个（单个）元素。 
>  如果需要匹配的有很多，我们可以使用 arr.filter(fn)。

> arr.map 对数组的每个元素都调用函数，并返回结果数组。

> arr.sort 方法对数组进行 原位（in-place） 排序，更改元素的顺序, 这些元素默认情况下被按字符串进行排序。

> 比较函数只需要返回一个正数表示“大于”，一个负数表示“小于”。

> 对于许多字母，最好使用 str.localeCompare 方法正确地对字母进行排序

```js
let value = arr.reduce(function(accumulator, item, index, array) {
  // ...
}, [initial]);
```
>  该函数一个接一个地应用于所有数组元素，并将其结果“搬运（carry on）”到下一个调用。 

> 第一个参数本质上是累加器，用于存储所有先前执行的组合结果。最后，它成为 reduce 的结果。

> 如果数组为空，那么在没有初始值的情况下调用 reduce 会导致错误,所以建议始终指定初始值。 

> 数组是基于对象的，不构成单独的语言类型, 所以 typeof 不能帮助从数组中区分出普通对象：

> thisArg 参数的值在 func 中变为 this。 
>
>


#### 练习题
1. 编写函数 camelize(str) 将诸如 “my-short-string” 之类的由短划线分隔的单词变成骆驼式的 “myShortString”。
即：删除所有短横线，并将短横线后的每一个单词的首字母变为大写。
```js
// 先将短划线去除，将短横线后的每一个首字母变成大写，再拼接
function camelize(str) {
  const result = str.split("-").map((item, index) => {
    if (index === 0) {
      return item;
    } else {
      const newItem = item[0].toUpperCase() + item.slice(1);
      return newItem;
    }
  }).join("")
  console.log(result);
  return result;
}
```

2. 写一个函数 filterRange(arr, a, b)，该函数获取一个数组 arr，在其中查找数值大于或等于 a，且小于或等于 b 的元素，并将结果以数组的形式返回。该函数不应该修改原数组。它应该返回新的数组。
```js
function filterRange(arr, a, b) {
  const result = arr.filter((item) => {
    if (item >= a && item <= b) {
      return item;
    }
  });
  return result;
}
```

3. 写一个函数 filterRangeInPlace(arr, a, b)，该函数获取一个数组 arr，并删除其中介于 a 和 b 区间以外的所有值。检查：a ≤ arr[i] ≤ b。该函数应该只修改数组。它不应该返回任何东西。
```js
function filterRangeInPlace(arr, a, b) {
  for (let i = 0; i < arr.length; i++) {
    let item = arr[i];
    if (item < a || item > b) {
      arr.splice(i, 1);
      i--
    }
  }
}
```

4. 降序排列
```js
let arr = [1, 3, 5, 0];
arr.sort((a, b) => b - a);
```

5. 我们有一个字符串数组 arr。我们希望有一个排序过的副本，但保持 arr 不变。创建一个函数 copySorted(arr) 返回这样一个副本。
```js
function copySorted(arr) {
  return arr.slice().sort()
}
```

6. 创建一个构造函数 Calculator，以创建“可扩展”的 calculator 对象。
   1) 首先，实现 calculate(str) 方法，该方法接受像 "1 + 2" 这样格式为“数字 运算符 数字”（以空格分隔）的字符串，并返回结果。该方法需要能够理解加号 + 和减号 -。
      
      用法示例：
      ```js
      let calc = new Calculator;
      alert( calc.calculate("3 + 7") ); // 10
      ```
   2) 然后添加方法 addMethod(name, func)，该方法教 calculator 进行新操作。它需要运算符 name 和实现它的双参数函数 func(a,b)。

      例如，我们添加乘法 *，除法 / 和求幂 **：
      ```js
      let powerCalc = new Calculator;
      powerCalc.addMethod("*", (a, b) => a * b);
      powerCalc.addMethod("/", (a, b) => a / b);
      powerCalc.addMethod("**", (a, b) => a ** b);

      let result = powerCalc.calculate("2 ** 3");
      alert( result ); // 8
      ```
    - 此任务中没有括号或复杂的表达式。
    - 数字和运算符之间只有一个空格。
    - 你可以自行选择是否添加错误处理功能。
  ```js
  function Calculate() {
    this.method = {
      "+": (a, b) => a + b,
      "-": (a, b) => a - b
    };

    this.calculate = function (str) {
      // 将 str 提取出来
      const splitItem = str.split(" ");
      const a = +splitItem[0];
      const op = splitItem[1];
      const b = +splitItem[2];

      if (!this.method[op] || isNaN(a) || isNaN(b)) {
        return NaN;
      }

      return this.method[op](a, b)
    }

    this.addMethod = function(name, func) {
      this.method[name] = func
    }
  }

  const calculator = new Calculate();

  let result = calculator.calculate("2 + 1");
  console.log(result)

  result = calculator.calculate("2 - 1");
  console.log(result);

  calculator.addMethod("*", (a, b) => a * b);
  result = calculator.calculate("2 * 1");
  console.log(result);

  calculator.addMethod("**", (a, b) => a ** b);
  result = calculator.calculate("2 ** 3");
  console.log(result);
  ```

7. 映射到Names，你有一个 user 对象数组，每个对象都有 user.name。编写将其转换为 names 数组的代码。
示例：
```js
let john = { name: "John", age: 25 };
let pete = { name: "Pete", age: 30 };
let mary = { name: "Mary", age: 28 };

let users = [ john, pete, mary ];

let names = users.map(item => item.name)

alert( names ); // John, Pete, Mary
```

8. 映射到对象，你有一个 user 对象数组，每个对象都有 name，surname 和 id。
编写代码以该数组为基础，创建另一个具有 id 和 fullName 的对象数组，
其中 fullName 由 name 和 surname 生成。
```js
let john = { name: "John", surname: "Smith", id: 1 };
let pete = { name: "Pete", surname: "Hunt", id: 2 };
let mary = { name: "Mary", surname: "Key", id: 3 };

let users = [ john, pete, mary ];

let usersMapped = users.map((item) => ({
  fullName: `${item.name} ${item.surname}`,
  id: item.id,
}));

/*
usersMapped = [
  { fullName: "John Smith", id: 1 },
  { fullName: "Pete Hunt", id: 2 },
  { fullName: "Mary Key", id: 3 }
]
*/

alert( usersMapped[0].id ) // 1
alert( usersMapped[0].fullName ) // John Smith
```

9. 编写函数 sortByAge(users) 获得对象数组的 age 属性，并根据 age 对这些对象数组进行排序。
```js
let john = { name: "John", age: 25 };
let pete = { name: "Pete", age: 30 };
let mary = { name: "Mary", age: 28 };

let arr = [ pete, john, mary ];

function sortByAge(arr) {
  arr.sort((a, b) => a.age - b.age)
}

sortByAge(arr);

// now: [john, mary, pete]
alert(arr[0].name); // John
alert(arr[1].name); // Mary
alert(arr[2].name); // Pete
```

10. 随机排列数组, 编写函数 shuffle(array) 来随机排列数组的元素。所有元素顺序应该具有相等的概率。
```js
let arr = [1, 2, 3];

function shuffle(arr) {
  // 逆向遍历数组，并将每个元素与前面的随机的一个元素交换位置
  for (let i = arr.length - 1; i > 0; i--) {
    // 从 0 到 i 之间随机选择一个元素
    let j = Math.floor(Math.random() * (i + 1));
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }
}

shuffle(arr);
```

11. 编写 getAverageAge(users) 函数，该函数获取一个具有 age 属性的对象数组，并返回平均年龄。
```js
let john = { name: "John", age: 25 };
let pete = { name: "Pete", age: 30 };
let mary = { name: "Mary", age: 29 };

let arr = [ john, pete, mary ];

function getAverageAge(arr) {
  return arr.reduce((prev, item) => prev + item.age, 0) / arr.length;
}

alert( getAverageAge(arr) ); // (25 + 30 + 29) / 3 = 28
```

12. 数组去重，创建一个函数 unique(arr)，返回去除重复元素后的数组 arr。
```js
function unique(arr) {
  let arrObj = {};
  for (let i = 0; i < arr.length; i++) {
    arrObj[arr[i]] = true;
  }
  return Object.keys(arrObj);
}

let strings = ["Hare", "Krishna", "Hare", "Krishna",
  "Krishna", "Krishna", "Hare", "Hare", ":-O"
];

alert( unique(strings) ); // Hare, Krishna, :-O
```

13. 从数组创建键对象：假设我们收到了一个用户数组，形式为：{id:..., name:..., age:... }。
创建一个函数 groupById(arr) 从该数组创建对象，以 id 为键（key），数组项为值。在这个任务里
我们假设 id 是唯一的。没有两个具有相同 id 的数组项。请在解决方案中使用数组的 .reduce 方法。
```js
let users = [
  {id: 'john', name: "John Smith", age: 20},
  {id: 'ann', name: "Ann Smith", age: 24},
  {id: 'pete', name: "Pete Peterson", age: 31},
];

function groupById(users) {
  return users.reduce((obj, item) => {
    obj[item.id] = item;
    return obj;
  }, {})
}

let usersById = groupById(users);

/*
// 调用函数后，我们应该得到：

usersById = {
  john: {id: 'john', name: "John Smith", age: 20},
  ann: {id: 'ann', name: "Ann Smith", age: 24},
  pete: {id: 'pete', name: "Pete Peterson", age: 31},
}
*/
```

### Iterable Object(可迭代对象)
[zh.javascript.info](https://zh.javascript.info/iterable)
> 可迭代（Iterable） 对象是数组的泛化。这个概念是说任何对象都可以被定制为可在 for..of 循环中使用的对象。

> 为了让 range 对象可迭代（也就让 for..of 可以运行）我们需要为对象添加一个名为 Symbol.iterator 的方法（一个专门用于使对象可迭代的内建 symbol）。

> 当 for..of 循环启动时，它会调用这个方法（如果没找到，就会报错）。这个方法必须返回一个 迭代器（iterator） —— 一个有 next 方法的对象。

> 当 for..of 循环希望取得下一个数值，它就调用这个对象的 next() 方法。

> next() 方法返回的结果的格式必须是 {done: Boolean, value: any}，当 done=true 时，表示循环结束，否则 value 是下一个值。

```js
let range = {
  from: 1,
  to: 5,
};

range[Symbol.iterator] = function () {
  return {
    current: this.from,
    last: this.to,
    next() {
      if (this.current <= this.last) {
        return {
          done: false,
          value: this.current++,
        };
      } else {
        return { done: true };
      }
    },
  };
};

for (let num of range) {
  console.log(num);
}
```

> Iterable 如上所述，是实现了 Symbol.iterator 方法的对象。

> Array-like 是有索引和 length 属性的对象，所以它们看起来很像数组。

> 字符串即是可迭代的（for..of 对它们有效），又是类数组的（它们有数值索引和 length 属性）。

> Array.from 可以接受一个可迭代或类数组的值，并从中获取一个“真正的”数组。

> `obj[Symbol.iterator]()` 的结果被称为 迭代器（iterator）

## Map and Set
[zh.javascript.info](https://zh.javascript.info/map-set)
> Map 是一个带键的数据项的集合，就像一个 Object 一样。 但是它们最大的差别是 Map 允许任何类型的键（key）。

> 与对象不同，键不会被转换成字符串。键可以是任何类型。

> Map 使用 SameValueZero 算法来比较键是否相等。它和严格等于 === 差不多，但区别是 NaN 被看成是等于 NaN。所以 NaN 也可以被用作键。

> 每一次 map.set 调用都会返回 map 本身，所以我们可以进行“链式”调用：

> map.keys() —— 遍历并返回一个包含所有键的可迭代对象， 
>   map.values() —— 遍历并返回一个包含所有值的可迭代对象， 
>   map.entries() —— 遍历并返回一个包含所有实体 [key, value] 的可迭代对象，for..of 在默认情况下使用的就是这个。

> 如果我们想从一个已有的普通对象（
>         plain
>          object）来创建一个 Map，那么我们可以使用内建方法 Object.entries(obj)，该方法返回对象的键/值对数组，该数组格式完全按照 Map 所需的格式。

> Object.fromEntries 方法的作用是相反的：给定一个具有 [key, value] 键值对的数组，它会根据给定数组创建一个对象：

> Set 是一个特殊的类型集合 —— “值的集合”（没有键），它的每一个值只能出现一次。 
>  

> Set 内部对唯一性检查进行了更好的优化。

> 可以使用 for..of 或 forEach 来遍历 Set：

> forEach 的回调函数有三个参数：一个 value，然后是 同一个值 valueAgain，最后是目标对象。

> new Map([iterable]) —— 创建 map，可选择带有 [key,value] 对的 iterable（例如数组）来进行初始化。

### 练习题
1. 定义 arr 为一个数组。创建一个函数 unique(arr)，该函数返回一个由 arr 中所有唯一元素所组成的数组。
```js
function unique(arr) {
  return Array.from(new Set(arr));
}

let values = ["Hare", "Krishna", "Hare", "Krishna",
  "Krishna", "Krishna", "Hare", "Hare", ":-O"
];

alert( unique(values) ); // Hare, Krishna, :-O
```

2. 过滤字谜
Anagrams 是具有相同数量相同字母但是顺序不同的单词。如：
```md
nap - pan
ear - are - era
cheaters - hectares - teachers
```
写一个函数 aclean(arr)，它返回被清除了字谜（anagrams）的数组。
对于所有的字谜（anagram）组，都应该保留其中一个词，但保留的具体是哪一个并不重要。
```js
let arr = ["nap", "teachers", "cheaters", "PAN", "ear", "era", "hectares"];

function aclean(arr) {
  // 遍历数组，将数组的每一项的字符串大小写进行排序，然后作为 map 的 key，
  // 将该项的字符串本身作为 value 保存
  // 然后返回 map 的 values
  let map = new Map();
  arr.map(item => {
    let sortedStringArrOfItem = item.toLowerCase().split("").sort("").join("");
    map.set(sortedStringArrOfItem, item);
  });
  return Array.from(map.values());
}

alert( aclean(arr) ); // "nap,teachers,ear" or "PAN,cheaters,era"
```

3. 我们期望使用 map.keys() 得到一个数组，然后使用例如 .push 等特定的方法对其进行处理。
修复下面代码
```js
let map = new Map();

map.set("name", "John");

let keys = Array.from(map.keys());

// Error: keys.push is not a function
keys.push("more");

console.log(keys);
```

## WeakMap and WeakSet
为什么称之为 `Weak*`，因为它是弱引用，不会阻止垃圾回收机制对作为键的对象的回收。
[zh.javascript.info](https://zh.javascript.info/weakmap-weakset)
> JavaScript 引擎在值“可达”和可能被使用时会将其保持在内存中。

> WeakMap 在这方面有着根本上的不同。它不会阻止垃圾回收机制对作为键的对象（key object）的回收。

> WeakMap 和 Map 的第一个不同点就是，WeakMap 的键必须是对象，不能是原始值：

> 如果我们在 weakMap 中使用一个对象作为键，并且没有其他对这个对象的引用 —— 该对象将会被从内存（和map）中自动清除。

> WeakMap 不支持迭代以及 keys()，values() 和 entries() 方法。所以没有办法获取 WeakMap 的所有键或值。

> WeakMap 只有以下的方法： 
>   
>   weakMap.get(key) 
>   weakMap.set(key, value) 
>   weakMap.delete(key) 
>   weakMap.has(key)

> 从技术上讲，WeakMap 的当前元素的数量是未知的。JavaScript 引擎可能清理了其中的垃圾，可能没清理，也可能清理了一部分。因此，暂不支持访问 WeakMap 的所有键/值的方法。

> WeakMap 的主要应用场景是 额外数据的存储。

> 我们可以存储（“缓存”）函数的结果，以便将来对同一个对象的调用可以重用这个结果。

### 练习题
1. 存储 unread 标识，你的代码可以访问它，但是 message 是由其他人的代码管理的。该代码会定期添加新消息，
删除旧消息，但是你不知道这些操作确切的发生时间。现在，你应该使用什么数据结构来保存关于消息“是否已读”的
信息？该结构必须很适合对给定的 message 对象给出“它读了吗？”的答案。
P.S. 当一个消息被从 messages 中删除后，它应该也从你的数据结构中消失。
P.S. 我们不能修改 message 对象，例如向其添加我们的属性。因为它们是由其他人的代码管理的，我们修改该数据
可能会导致不好的后果。
```js
let messages = [
  { text: "Hello", from: "John" },
  { text: "How goes?", from: "John" },
  { text: "See you soon", from: "Alice" },
];

let readMessage = new WeakSet();

// 假如消息已读
readMessage.add(messages[0]);
readMessage.add(messages[1]);
readMessage.add(messages[0]);

console.log("Read message 0: " + readMessage.has(messages[0]));
```

2. 与上题类似，现在的问题是：你建议采用什么数据结构来保存信息：“消息是什么时候被阅读的？”。
```js
let messages = [
  { text: "Hello", from: "John" },
  { text: "How goes?", from: "John" },
  { text: "See you soon", from: "Alice" },
];

let readDate = new WeakMap();
readDate.set(messages[0], new Date());
```

## Object.keys, values, entries
[zh.javascript.info](https://zh.javascript.info/keys-values-entries)
> Object.keys(obj) —— 返回一个包含该对象所有的键的数组。 
>   Object.values(obj) —— 返回一个包含该对象所有的值的数组。 
>   Object.entries(obj) —— 返回一个包含该对象所有 [key, value] 键值对的数组。

> Object.* 方法返回的是“真正的”数组对象，而不只是一个可迭代对象。

> 对象缺少数组存在的许多方法，例如 map 和 filter 等。 
>  如果我们想应用它们，那么我们可以使用 Object.entries，然后使用 Object.fromEntries： 
>   
>   使用 Object.entries(obj) 从 obj 获取由键/值对组成的数组。 
>   对该数组使用数组方法，例如 map，对这些键/值对进行转换。 
>   对结果数组使用 Object.fromEntries(array) 方法，将结果转回成对象。
```js
let user = {
  name: "John",
  age: 30
};

// 遍历所有的值
for (let value of Object.values(user)) {
  alert(value); // John, then 30
}

let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

let doublePrices = Object.fromEntries(
  // 将价格转换为数组，将每个键/值对映射为另一对
  // 然后通过 fromEntries 再将结果转换为对象
  Object.entries(prices).map(entry => [entry[0], entry[1] * 2])
);

alert(doublePrices.meat); // 8
```

### 练习题
1. 有一个带有任意数量薪水的 salaries 对象。
编写函数 sumSalaries(salaries)，该函数使用 Object.values 和 for..of 循环返回所有薪水的总和。
如果 salaries 是空对象，那么结果必须是 0。
```js
let salaries = {
  John: 100,
  Pete: 300,
  Mary: 250,
};

function sumSalaries(salaries) {
  let result = 0;
  for (let item of Object.values(salaries)) {
    result += item;
  }
  return result;
}

console.log(sumSalaries(salaries)); // 650
```

2. 计算属性数量，写一个函数 count(obj)，该函数返回对象中的属性的数量：
```js
let user = {
  name: 'John',
  age: 30
};

function count(obj) {
  return Object.keys(obj).length;
}

console.log( count(user) ); // 2
```

## 解构赋值
[zh.javascript.info](https://zh.javascript.info/destructuring-assignment)
> 等号右侧可以是任何可迭代对象

> 可以在等号左侧使用任何“可以被赋值的”东西。

> 使用解构赋值来交换两个变量的值

> 如果数组比左边的列表长，那么“其余”的数组项会被省略。

> 如果我们还想收集其余的数组项 —— 我们可以使用三个点 "..." 来再加一个参数以获取其余数组项：

> 如果数组比左边的变量列表短，这里不会出现报错。缺少对应值的变量都会被赋 undefined： 

> 如果我们想要一个“默认”值给未赋值的变量，我们可以使用 = 来提供： 

> 如果我们想把一个属性赋值给另一个名字的变量，那么我们可以使用冒号来设置变量名称：

> 对于可能缺失的属性，我们可以使用 "=" 设置默认值

### 练习题
1. 我们有一个对象：写一个解构赋值语句使得：
name 属性赋值给变量 name。
years 属性赋值给变量 age。
isAdmin 属性赋值给变量 isAdmin（如果属性缺失则取默认值 false）。
```js
let user = { name: 'John', years: 30 };

let { name, years, isAdmin = false } = user;

console.log(name);
console.log(years);
console.log(isAdmin);
```

2. 最高薪资，这儿有一个 salaries 对象：新建一个函数 topSalary(salaries)，返回收入最高的人的姓名。

如果 salaries 是空的，函数应该返回 null。
如果有多个收入最高的人，返回其中任意一个即可。
P.S. 使用 Object.entries 和解构语法来遍历键/值对。
```js
let salaries = {
  John: 100,
  Pete: 300,
  Mary: 250,
};

function isEmpty(obj) {
  for (let key in obj) {
    return false;
  }
  return true;
}

function topSalary(salaries) {
  if (isEmpty(salaries)) {
    return null;
  }

  let salariesArr = Object.entries(salaries);
  let [topPerson, topSalary] = salariesArr[0];

  for (let [person, salary] of salariesArr) {
    if (topSalary < salary) {
      topPerson = person;
      topSalary = salary;
    }
  }
  return topPerson;
}

console.log(topSalary(salaries));
```

## 日期与时间
[zh.javascript.info](https://zh.javascript.info/date)
> new Date() 
>    不带参数 —— 创建一个表示当前日期和时间的 Date 对象

> new Date(milliseconds) 
>    创建一个 Date 对象，其时间等于 1970 年 1 月 1 日 UTC+0 之后经过的毫秒数

> 在 01.01.1970 之前的日期带有负的时间戳

> 如果只有一个参数，并且是字符串，那么它会被自动解析。该算法与 Date.parse 所使用的算法相同

> new Date(year, month, date, hours, minutes, seconds, ms) 
>    使用当前时区中的给定组件创建日期。只有前两个参数是必须的。

> year 应该是四位数

> month 计数从 0（一月）开始，到 11（十二月）结束。

> date 是当月的具体某一天，如果缺失，则为默认值 1。

> 如果 hours/minutes/seconds/ms 缺失，则均为默认值 0。

> getFullYear() 
>    
>   
>     获取年份（4 位数） 
>    
>    getMonth() 
>    
>   
>     获取月份，从 0 到 11。 
>    
>    getDate() 
>    
>   
>     获取当月的具体日期，

> getHours()，getMinutes()，getSeconds()，getMilliseconds() 
>    
>   
>     获取相应的时间组件。

> getDay() 
>    
>   
>     获取一周中的第几天，从 0（星期日）到 6（星期六）

> 自动校准 是 Date 对象的一个非常方便的特性。我们可以设置超范围的数值，它会自动校准。

> Date.now()，它会返回当前的时间戳。 
>  它相当于 new Date().getTime()，但它不会创建中间的 Date 对象。因此它更快，而且不会对垃圾回收造成额外的压力。

### 练习题
1. 创建一个 Date 对象，日期是：Feb 20, 2012, 3:12am。时区是当地时区。
```js
let date = new Date(2012, 1, 20, 3, 12);
console.log(date);
```

2. 编写一个函数 getWeekDay(date) 以短格式来显示一个日期的星期数：
‘MO’，‘TU’，‘WE’，‘TH’，‘FR’，‘SA’，‘SU’。
```js
let date = new Date(2012, 0, 3); // 3 Jan 2012

function getWeekDay(date) {
  let dayNum = date.getDay();
  let dayStringArr = ["SU", "MO", "TU", "WE", "TH", "FR", "SA"];
  return dayStringArr[dayNum];
}

console.log(getWeekDay(date));
```

3. 欧洲国家的星期计算是从星期一（数字 1）开始的，然后是星期二（数字 2），直到星期日（数字 7）。
编写一个函数 getLocalDay(date)，并返回日期的欧洲式星期数。
```js
let date = new Date(2023, 0, 15);

function getLocalDay(date) {
  let dayNum = date.getDay();
  if (dayNum === 0) {
    return 7;
  } else {
    return dayNum;
  }
}

console.log(getLocalDay(date));
```

4. 写一个函数 getDateAgo(date, days)，返回特定日期 date 往前 days 天是哪个月的哪一天。
```JavaScript
let date = new Date(2015, 0, 2);

function getDateAgo(date, days) {
  let dateCopy = new Date(date);
  dateCopy.setDate(date.getDate() - days);
  return dateCopy.getDate();
}

console.log(getDateAgo(date, 1)); // 1, (1 Jan 2015)
console.log(getDateAgo(date, 2)); // 31, (31 Dec 2014)
console.log(getDateAgo(date, 365)); // 2, (2 Jan 2014)
```

5. 写一个函数 getLastDayOfMonth(year, month) 返回 month 月的最后一天。
时候是 30，有时是 31，甚至在二月的时候会是 28/29。
```js
function isLeapYear(year) {
  if (year % 4 === 0) {
    if (year % 100 === 0) {
      if (year % 400 === 0) {
        return true;
      } else {
        return false;
      }
    } else {
      return true;
    }
  } else {
    return false;
  }
}

function getLastDayOfMonth(year, month) {
  switch (month + 1) {
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
      return 31;
    case 4:
    case 6:
    case 9:
    case 11:
      return 30;
    case 2:
      if (isLeapYear(year)) {
        return 29;
      } else {
        return 28;
      }
  }
}

console.log(getLastDayOfMonth(2023, 1));
```

6. 写一个函数 getSecondsToday()，返回今天已经过去了多少秒？
```js
function getSecondsToday() {
  let now = new Date();
  let today = new Date(now.getFullYear(), now.getMonth(), now.getDate());
  let diff = now - today;
  return Math.round(diff / 1000);
}

console.log(getSecondsToday());
```

7. 写一个函数 getSecondsToTomorrow()，返回距离明天的秒数。
```js
function getSecondsToTomorrow() {
  let now = new Date();
  let tomorrow = new Date(now.getFullYear(), now.getMonth(), now.getDate() + 1);
  let diff = tomorrow - now;
  return Math.round(diff / 1000);
}

console.log(getSecondsToTomorrow());
```

8. 写一个函数 formatDate(date)，能够对 date 进行如下格式化：

如果 date 距离现在不到 1 秒，输出 "right now"。
否则，如果 date 距离现在不到 1 分钟，输出 "n sec. ago"。
否则，如果不到 1 小时，输出 "m min. ago"。
否则，以 "DD.MM.YY HH:mm" 格式输出完整日期。即："day.month.year hours:minutes"，
全部以两位数格式表示，例如：31.12.16 10:00。
```js
function formatDate(date) {
  let now = new Date();
  let diff = now - date;
  if (diff < 1000) {
    return "right now";
  } else if (diff < 60 * 1000) {
    return `${Math.round(diff / 1000)} sec. ago`;
  } else if (diff < 60 * 60 * 1000) {
    return `${Math.round(diff / (60 * 1000))} min. ago`;
  } else {
    let y = (date.getFullYear() % 100).toString().padStart(2, "0");
    let month = (date.getMonth() + 1).toString().padStart(2, "0");
    let d = date.getDate().toString().padStart(2, "0");
    let h = date.getHours().toString().padStart(2, "0");
    let minute = date.getMinutes().toString().padStart(2, "0");

    return `${d}.${month}.${y} ${h}:${minute}`;
  }
}

console.log(formatDate(new Date(2023, 0, 20)));
```

## JSON 方法，toJSON
[zh.javascript.info](https://zh.javascript.info/json)
> JSON.stringify 将对象转换为 JSON

> JSON.parse 将 JSON 转换回对象。

> 方法 JSON.stringify(student) 接收对象并将其转换为字符串。

> JSON 编码的对象与对象字面量有几个重要的区别： 
>   
>   字符串使用双引号。JSON 中没有单引号或反引号。

> 对象属性名称也是双引号的。这是强制性的。

> JSON 是语言无关的纯数据规范，因此一些特定于 JavaScript 的对象属性会被 JSON.stringify 跳过。

> 函数属性（方法）。 
>   Symbol 类型的键和值。 
>   存储 undefined 的属性。

> 重要的限制：不得有循环引用。
> JSON.stringify(value, replacer, spaces) 的第三个参数是用于优化格式的空格数量。

### 练习题
1. 将 user 转换为 JSON，然后将其转换回到另一个变量。
```js
let user = {
  name: "John Smith",
  age: 35,
};

let userJSON = JSON.stringify(user);
console.log(userJSON);

let userValue = JSON.parse(userJSON);
console.log(userValue);
```

2. 在简单循环引用的情况下，我们可以通过名称排除序列化中违规的属性。
但是，有时我们不能只使用名称，因为它既可能在循环引用中也可能在常规属性中使用。因此，我们可以
通过属性值来检查属性。编写 replacer 函数，移除引用 meetup 的属性，并将其他所有属性序列化：
```js
let room = {
  number: 23,
};

let meetup = {
  title: "Conference",
  occupiedBy: [{ name: "John" }, { name: "Alice" }],
  place: room,
};

// 循环引用
room.occupiedBy = meetup;
meetup.self = meetup;

console.log(
  JSON.stringify(meetup, function replacer(key, value) {
    /* your code */
    return key !== "" && value === meetup ? undefined : value;
  })
);

/* 结果应该是：
{
  "title":"Conference",
  "occupiedBy":[{"name":"John"},{"name":"Alice"}],
  "place":{"number":23}
}
*/
```

# 函数进阶内容
## 递归和堆栈
[zh.javascript.info](https://zh.javascript.info/recursion)
> 当一个函数解决一个任务时，在解决的过程中它可以调用很多其它函数。在部分情况下，函数会调用 自身。这就是所谓的 递归。

> 递归的另一个重要应用就是递归遍历。

> 任何递归函数都可以被重写为迭代（译注：也就是循环）形式。有时这是在优化代码时需要做的。但对于大多数任务来说，递归方法足够快，并且容易编写和维护。

```js
let company = { // 是同一个对象，简洁起见被压缩了
  sales: [{name: 'John', salary: 1000}, {name: 'Alice', salary: 1600 }],
  development: {
    sites: [{name: 'Peter', salary: 2000}, {name: 'Alex', salary: 1800 }],
    internals: [{name: 'Jack', salary: 1300}]
  }
};

// 用来完成任务的函数
function sumSalaries(department) {
  if (Array.isArray(department)) { // 情况（1）
    return department.reduce((prev, current) => prev + current.salary, 0); // 求数组的和
  } else { // 情况（2）
    let sum = 0;
    for (let subdep of Object.values(department)) {
      sum += sumSalaries(subdep); // 递归调用所有子部门，对结果求和
    }
    return sum;
  }
}

alert(sumSalaries(company)); // 7700
```

### 练习题
1. 编写一个函数 sumTo(n) 计算 1 + 2 + ... + n 的和。
```js
function sumTo(n) {
  if (n === 1) {
    return 1;
  } else {
    return n + sumTo(n - 1);
  }
}
```

2. 编写一个函数 factorial(n) 使用递归调用计算 n!。
```js
function factorial(n) {
  if (n === 1) {
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}

console.log(factorial(5));
```

3. 斐波那契数 序列有这样的公式： Fn = Fn-1 + Fn-2。换句话说，下一个数字是前两个数字的和。
前两个数字是 1，然后是 2(1+1)，然后 3(1+2)，5(2+3) 等：1, 1, 2, 3, 5, 8, 13, 21...。
编写一个函数 fib(n) 返回第 n 个斐波那契数。
```js
function fib(n) {
  if (n === 1) {
    return 1;
  } else if (n == 2) {
    return 1;
  } else {
    return fib(n - 1) + fib(n - 2);
  }
}

console.log(fib(9));
```

## Rest 参数与 Spread 语法
[zh.javascript.info](https://zh.javascript.info/rest-parameters-spread)  
> ...变量名，这将会声明一个数组并指定其名称，其中存有剩余的参数。这三个点的语义就是“收集剩余的参数并存进指定数组中”。  

  
> ...rest 必须写在参数列表最后。  

  
> 有一个名为 arguments 的特殊类数组对象可以在函数中被访问，该对象以参数在参数列表中的索引作为键，存储所有参数。  

  
> 尽管 arguments 是一个类数组，也是可迭代对象，但它终究不是数组。它不支持数组方法，因此我们不能调用 arguments.map(...) 等方法。  

  
> 箭头函数没有 "arguments"   
  
如果我们在箭头函数中访问 arguments，访问到的 arguments 并不属于箭头函数，而是属于箭头函数外部的“普通”函数。  

  
> 箭头函数没有自身的 this。现在我们知道了它们也没有特殊的 arguments 对象。  

  
> Spread 语法 可以解决这个问题！它看起来和 rest 参数很像，也使用 ...，但是二者的用途完全相反。  

  
> Array.from(obj) 和 [...obj] 存在一个细微的差别：   
  
Array.from 适用于类数组对象也适用于可迭代对象。   
Spread 语法只适用于可迭代对象。   
  
因此，对于将一些“东西”转换为数组的任务，Array.from 往往更通用。  
> 复制 array/object  

  ``` js
      let arr = [1, 2, 3];
      
      let arrCopy = [...arr]; 
      
      let obj = { a: 1, b: 2, c: 3 };
      
      let objCopy = { ...obj }; 
  ```
> 若 ... 出现在函数参数列表的最后，那么它就是 rest 参数，它会把参数列表中剩余的参数收集到一个数组中。   
若 ... 出现在函数调用或类似的表达式中，那它就是 spread 语法，它会把一个数组展开为列表。  

  
> Rest 参数用于创建可接受任意数量参数的函数。  

  
> Spread 语法用于将数组传递给通常需要含有许多参数的函数。

## 变量作用域，闭包  
 [zh.javascript.info](https://zh.javascript.info/closure)  
 > 函数可以访问其外部的变量。  

   
 > 但是，如果在函数被创建之后，外部变量发生了变化会怎样？函数会获得新值还是旧值？  

   
 > 如果将函数作为参数（argument）传递并在代码中的另一个位置调用它，该函数将访问的是新位置的外部变量吗？  

   
 > 用 const 声明的变量的行为也相同（译注：与 let 在作用域等特性上是相同的），因此，本文也涉及用 const 进行变量声明。   
 旧的 var 与上面两个有着明显的区别  

   
 > 如果在代码块 {...} 内声明了一个变量，那么这个变量只在该代码块内可见。  

   
 > 对于 if，for 和 while 等，在 {...} 中声明的变量也仅在内部可见：  

   
 > 词法环境对象由两部分组成：   
   
    - 环境记录（Environment Record） —— 一个存储所有局部变量作为其属性（包括一些其他信息，例如 this 的值）的对象。   
    - 对外部词法环境 的引用，与外部代码相关联。  

   
 > 函数声明的初始化会被立即完成。  

   
 > 当创建了一个词法环境（Lexical Environment）时，函数声明会立即变为即用型函数（不像 let 那样直到声明处才可用）。  

   
 > 当代码要访问一个变量时 —— 首先会搜索内部词法环境，然后搜索外部环境，然后搜索更外部的环境，以此类推，直到全局词法环境。  

   
 > 所有的函数在“诞生”时都会记住创建它们的词法环境。从技术上讲，这里没有什么魔法：所有函数都有名为 [[Environment]] 的隐藏属性，该属性保存了对创建该函数的词法环境的引用。  

   
 > 闭包 是指一个函数可以记住其外部变量并可以访问这些变量。  

``` js
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
```
> JavaScript 中的函数会自动通过隐藏的 [[Environment]] 属性记住创建它们的位置，所以它们都可以访问外部变量。  
  
> 但在实际中，JavaScript 引擎会试图优化它。它们会分析变量的使用情况，如果从代码中可以明显看出有未使用的外部变量，那么就会将其删除。  

``` js
let name = "John";

function sayHi() {
  alert("Hi, " + name);
}

name = "Pete";

sayHi(); // 会显示什么："John" 还是 "Pete"？
// Pete
// 函数将从内到外依次在对应的词法环境中寻找目标变量，它使用最新的值。

// 旧变量值不会保存在任何地方。当一个函数想要一个变量时，它会从自己的词法环境
// 或外部词法环境中获取当前值。
```
``` js
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
let counter2 = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1

alert( counter2() ); // 0
alert( counter2() ); // 1
// 函数 counter 和 counter2 是通过 makeCounter 的不同调用创建的。

// 因此，它们具有独立的外部词法环境，每一个都有自己的 count。
```

``` js
let phrase = "Hello";

if (true) {
  let user = "John";

  function sayHi() {
    alert(`${phrase}, ${user}`);
  }
}

sayHi(); // error
// 函数 sayHi 是在 if 内声明的，所以它只存在于 if 中。外部是没有 sayHi 的。
```

``` js
// 编写一个像 sum(a)(b) = a+b 这样工作的 sum 函数。
function sum(a) {
  return function (b) {
    return a + b;
  };
}

console.log(sum(5)(-4));
```

``` js
// 变量死区
// 下面的代码会报错 error，ReferenceError: Cannot access 'x' before initialization
let x = 1;

function func() {
  console.log(x); // ?

  let x = 2;
}

func();

// 引擎从函数开始就知道局部变量 x，
// 但是变量 x 一直处于“未初始化”（无法使用）的状态，直到结束 let（“死区”）
// 因此答案是 error
```

``` js
// 闭包与Arr.filter(f)
/* 
我们有一个内建的数组方法 arr.filter(f)。它通过函数 f 过滤元素。如果它返回 true，
那么该元素会被返回到结果数组中。

制造一系列“即用型”过滤器：

inBetween(a, b) —— 在 a 和 b 之间或与它们相等（包括）。
inArray([...]) —— 包含在给定的数组中。
用法如下所示：

arr.filter(inBetween(3,6)) —— 只挑选范围在 3 到 6 的值。
arr.filter(inArray([1,2,3])) —— 只挑选与 [1,2,3] 中的元素匹配的元素。
*/
let arr = [1, 2, 3, 4, 5, 6, 7];

function inBetween(a, b) {
  return function (value) {
    return value >= a && value <= b;
  };
}

function inArray(array) {
  return function (value) {
    return array.includes(value);
  };
}

console.log(arr.filter(inBetween(3, 6))); // 3,4,5,6

console.log(arr.filter(inArray([1, 2, 10]))); // 1,2
```

``` js
// 闭包与 sort，按字段排序
let users = [
  { name: "John", age: 20, surname: "Johnson" },
  { name: "Pete", age: 18, surname: "Peterson" },
  { name: "Ann", age: 19, surname: "Hathaway" },
];

function byField(key) {
  return function (a, b) {
    return a[key] > b[key] ? 1 : -1;
  };
}

users.sort(byField("name"));
console.log(users);
users.sort(byField("age"));
console.log(users);
```

``` js
// 闭包与循环
function makeArmy() {
  let shooters = [];

  let i = 0;
  while (i < 10) {
    let shooter = function () {
      // 创建一个 shooter 函数，
      console.log(i); // 应该显示其编号
    };
    shooters.push(shooter); // 将此 shooter 函数添加到数组中
    i++;
  }

  // ……返回 shooters 数组
  return shooters;
}

let army = makeArmy();
// ……所有的 shooter 显示的都是 10，而不是它们的编号 0, 1, 2, 3...
army[0](); // 编号为 0 的 shooter 显示的是 10
army[1](); // 编号为 1 的 shooter 显示的是 10
army[2](); // 10，其他的也是这样。
/*
这是因为 shooter 使用的 i 是在 shooter 函数以外，调用时，循环函数已运行结束。
此时 i 等于 10；
两种改法：
1. 让 shooter 拥有和自己位于同一词法环境的 i
2. 使用 for 循环代替 while
*/
// 1. 让 shooter 拥有和自己位于同一词法环境的 i
while (i < 10) {
  let j = i;
  let shooter = function () {
    // 创建一个 shooter 函数，
    console.log(j); // 应该显示其编号
  };
  shooters.push(shooter); // 将此 shooter 函数添加到数组中
  i++;
}

// 2. 使用 for 循环代替 while
for (let i = 0; i < 10; i++) {
  let shooter = function () {
    console.log(i);
  };
  shooters.push(shooter);
}
```

## 老旧的 `var`
[zh.javascript.info](https://zh.javascript.info/var)  
> ar 声明的变量只有函数作用域和全局作用域，没有块级作用域

> 对于循环也是这样的，var 声明的变量没有块级作用域也没有循环局部作用域：

> 如果一个代码块位于函数内部，那么 var 声明的变量的作用域将为函数作用域

> 使用 var，我们可以重复声明一个变量  

> “var” 声明的变量，可以在其声明语句前被使用   

> var 声明的变量会在函数开头被定义，与它在代码中定义的位置无关  

> 声明会被提升，但是赋值不会。   

> 声明在函数刚开始执行的时候（“提升”）就被处理了，但是赋值操作始终是在它出现的地方才起作用。  
``` js
function sayHi() {
  var phrase; // 在函数刚开始时进行变量声明

  alert(phrase); // undefined

  phrase = "Hello"; // ……赋值 — 当程序执行到这一行时。
}

sayHi();
```
> 在之前，JavaScript 中只有 var 这一种声明变量的方式，并且这种方式声明的变量没有块级作用域，程序员们就发明了一种模仿块级作用域的方法。这种方法被称为“立即调用函数表达式”  

## 全局对象
[zh.javascript.info](https://zh.javascript.info/global-object)
> 在浏览器中，它的名字是 “window”，对 Node.js 而言，它的名字是 “global”，其它环境可能用的是别的名字。

> 最近，globalThis 被作为全局对象的标准名称加入到了 JavaScript 中，所有环境都应该支持该名称。所有主流浏览器都支持它。

> 在浏览器中，使用 var（而不是 let/const！）声明的全局函数和变量会成为全局对象的属性。

> 函数声明（特指在主代码流中具有 function 关键字的语句，而不是函数表达式）也有这样的效果。

## 函数对象，NFE
- [zh.javascript.info](https://zh.javascript.info/function-object)  
> 在 JavaScript 中，函数的类型是对象。

> 函数的名字可以通过属性 “name” 来访问

> 内建属性 “length”，它返回函数入参的个数

> rest 参数不参与计数  

> 我们可以把函数当作对象，在它里面存储属性，但是这对它的执行没有任何影响。变量不是函数属性，反之亦然。它们之间是平行的。  

> 命名函数表达式（NFE，Named Function Expression），指带有名字的函数表达式的术语。  
``` js
let sayHi = function func(who) {
if (who) {
  alert(`Hello, ${who}`);
} else {
  func("Guest"); // 使用 func 再次调用函数自身
}
};
sayHi(); // Hello, Guest
// 但这不工作：
func(); // Error, func is not defined（在函数外不可见）
// 应用场景：防止 sayHi 函数在外部被改变。
```
> 关于名字 func 有两个特殊的地方，这就是添加它的原因：   
  - 它允许函数在内部引用自己。
  - 它在函数外是不可见的。

## new Function 语法
[zh.javascript.info](https://zh.javascript.info/new-function)
> let func = new Function ([arg1, arg2, ...argN], functionBody);

> new Function 允许我们将任意字符串变为函数。例如，我们可以从服务器接收一个新的函数并执行它：

> 使用 new Function 创建函数的应用场景非常特殊，比如在复杂的 Web 应用程序中，我们需要从服务器获取代码或者动态地从模板编译函数时才会使用。

> 如果我们使用 new Function 创建一个函数，那么该函数的 [[Environment]] 并不指向当前的词法环境，而是指向全局环境。

> 因此，此类函数无法访问外部（outer）变量，只能访问全局变量。

## setTimeout & setInterval
[zh.javascript.info](https://zh.javascript.info/settimeout-setinterval)
> setTimeout 允许我们将函数推迟到一段时间间隔之后再执行。 
>   setInterval 允许我们重复运行一个函数，从一段时间间隔之后开始运行，之后以该时间间隔连续重复运行该函数。

> setTimeout 期望得到一个对函数的引用

> setTimeout 在调用时会返回一个“定时器标识符（timer identifier）”，在我们的例子中是 timerId，我们可以使用它来取消执行。

```js
let timerId = setTimeout(...);
clearTimeout(timerId);
```

> 嵌套的 setTimeout 相较于 setInterval 能够更精确地设置两次执行之间的延时。
```js
let timerId = setTimeout(function tick() {
  console.log("tick");
  timerId = setTimeout(tick, 2000); // (*)
}, 2000);
```

### 练习题
编写一个函数 printNumbers(from, to)，使其每秒输出一个数字，数字从 from 开始，到 to 结束。
使用以下两种方法来实现。

1. 使用 setInterval。
2. 使用嵌套的 setTimeout。
```js
function printNumbers(from, to) {
  // use setInterval
  // let i = from;
  // let timerId = setInterval(function () {
  //   console.log(i);
  //   i++;
  //   if (i > to) {
  //     clearInterval(timerId);
  //   }
  // }, 1000);

  // use setTimeout
  let i = from;
  let timerId = setTimeout(function print() {
    console.log(i);
    i++;
    timerId = setTimeout(print, 1000);

    if (i > to) {
      clearTimeout(timerId);
    }
  }, 1000);
}

printNumbers(1, 3);
```

## 装饰器模式和转发，call/apply
[zh.javascript.info](https://zh.javascript.info/call-apply-decorators)
### 透明缓存
```js
function slow(x) {
  console.log("from slow function");
  return x;
}

function cachingDecorator(func) {
  let cache = new Map();

  return function (x) {
    if (cache.has(x)) {
      console.log("from cache");
      return cache.get(x);
    }

    let result = func(x);

    cache.set(x, result);
    return result;
  };
}

slow = cachingDecorator(slow);

console.log(slow(1));
console.log("- - - - -");
console.log("again: " + slow(1));
console.log("- - - - -");
console.log(slow(2));
console.log("- - - - -");
console.log("again: " + slow(2));
```

> cachingDecorator 是可重用的。我们可以将它应用于另一个函数。 
>   缓存逻辑是独立的，它没有增加 slow 本身的复杂性（如果有的话）。 
>   如果需要，我们可以组合多个装饰器（其他装饰器将遵循同样的逻辑）。

> 对于即可迭代又是类数组的对象，例如一个真正的数组，我们使用 call 或 apply 均可，但是 apply 可能会更快，因为大多数 JavaScript 引擎在内部对其进行了优化。

> 将所有参数连同上下文一起传递给另一个函数被称为“呼叫转移（call forwarding）”。

>  方法借用（method borrowing）。 
>  我们从常规数组 [].join 中获取（借用）join 方法，并使用 [].join.call 在 arguments 的上下文中运行它。

> 装饰器 是一个围绕改变函数行为的包装器。主要工作仍由该函数来完成。

> 装饰器可以被看作是可以添加到函数的 “features” 或 “
>         
>           aspects

> func.call(context, arg1, arg2…) —— 用给定的上下文和参数调用 func。 
>   func.apply(context, args) —— 调用 func 将 context 作为 this 和类数组的 args 传递给参数列表。

```js
let worker = {
  someMethod() {
    return 1;
  },

  slow(min, max) {
    return min + max;
  },
};

function cachingDecorator(func, hash) {
  let cache = new Map();
  console.log(this);
  return function () {
    let key = hash();
    if (cache.has(key)) {
      return cache.get(key);
    }
    console.log(this);
    let result = func.call(this, ...arguments);
    cache.set(key, result);
    return result;
  };
}

function hash() {
  return [].join.call(arguments);
}

console.log(worker.slow(3, 5));

worker.slow = cachingDecorator(worker.slow, hash);
console.log(worker.slow(3, 5));
```

### 练习题
1. 间谍装饰器
创建一个装饰器 spy(func)，它应该返回一个包装器，该包装器将所有对函数的调用保存在其 calls 属性中。
每个调用都保存为一个参数数组。
```js
function work(a, b) {
  alert( a + b ); // work 是一个任意的函数或方法
}

function spy(func) {
  function wrapper(...args) {
    wrapper.calls.push(...args);
    return func.apply(this, args);
  }

  wrapper.calls = [];
  return wrapper;
}

work = spy(work);

work(1, 2); // 3
work(4, 5); // 9

for (let args of work.calls) {
  console.log( 'call:' + args.join() ); // "call:1,2", "call:4,5"
}
```

2. 延时装饰器
创建一个装饰器 delay(f, ms)，该装饰器将 f 的每次调用延时 ms 毫秒。

```js
function f(x) {
  console.log(x);
}

function delay(func, mill) {
  // 注，setTimeout 中要使用正确的变量
  function wrapper(...args) {
    let that = this;
    setTimeout(function () {
      console.log("this", this);
      console.log("that", that);
      func.apply(that, args);
    }, mill);
  }

  return wrapper;
}

// 使用箭头函数
function delay(f, ms) {
  return function() {
    setTimeout(() => f.apply(this, arguments), ms);
  }
}

// create wrappers
let f1000 = delay(f, 1000);
let f5000 = delay(f, 5000);

f1000("test"); // 在 1000ms 后显示 "test"
f5000("test"); // 在 5000ms 后显示 "test"
```

3. 防抖装饰器
debounce(f, ms) 装饰器的结果是一个包装器，该包装器将暂停对 f 的调用，直到经过 ms 毫秒的非活动状态
（没有函数调用，“冷却期”），然后使用最新的参数调用 f 一次。
```js
function f(x) {
  console.log(x);
}

function debounce(f, ms) {
  let timeout;
  return function () {
    clearTimeout(timeout);
    timeout = setTimeout(() => f.apply(this, arguments), ms);
  };
}

f = debounce(f, 5000);
f(1);
f(1);
f(1);

for (let i = 0; i < 100; i++) {
  f(1);
}
f(2);
// 上述代码只会输出 2
```

4. 节流装饰器
创建一个“节流”装饰器 throttle(f, ms) —— 返回一个包装器。
当被多次调用时，它会在每 ms 毫秒最多将调用传递给 f 一次。
```js
function f(a) {
  console.log(a);
}

function throttle(func, ms) {
  let isThrottled = false,
    savedArgs,
    savedThis;

  function wrapper() {
    if (isThrottled) {
      // (2)
      savedArgs = arguments;
      savedThis = this;
      return;
    }
    isThrottled = true;

    func.apply(this, arguments); // (1)

    setTimeout(function () {
      isThrottled = false; // (3)
      if (savedArgs) {
        wrapper.apply(savedThis, savedArgs);
        savedArgs = savedThis = null;
      }
    }, ms);
  }

  return wrapper;
}

// f1000 最多每 1000ms 将调用传递给 f 一次
let f1000 = throttle(f, 1000);

f1000(1); // 显示 1
f1000(2); // (节流，尚未到 1000ms)
f1000(3); // (节流，尚未到 1000ms)

// 当 1000ms 时间到...
// ...输出 3，中间值 2 被忽略
```

在第一次调用期间，wrapper 只运行 func 并设置冷却状态（isThrottled = true）。
在这种状态下，所有调用都记忆在 savedArgs/savedThis 中。请注意，上下文和参数（arguments）同等重要，
应该被记下来。我们同时需要他们以重现调用。
……然后经过 ms 毫秒后，触发 setTimeout。冷却状态被移除（isThrottled = false），如果我们忽略了调用，
则将使用最后记忆的参数和上下文执行 wrapper。
第 3 步运行的不是 func，而是 wrapper，因为我们不仅需要执行 func，还需要再次进入冷却状态并设置 timeout 
以重置它。

## 函数绑定
[zh.javascript.info](https://zh.javascript.info/bind)
> 一旦方法被传递到与对象分开的某个地方 —— this 就丢失。

> 浏览器中的 setTimeout 方法有些特殊：它为函数调用设定了 this=window（对于 Node.js，this 则会变为计时器（timer）对象

> func.bind(context) 的结果是一个特殊的类似于函数的“外来对象（exotic object）”，它可以像函数一样被调用，并且透明地将调用传递给 func 并设定 this=context。

> 我们不仅可以绑定 this，还可以绑定参数（arguments）。
```js
function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
```

> bind 的完整语法如下： 
>   
>   let bound = func.bind(context, [arg1], [arg2], ...); 
>   
>  它允许将上下文绑定为 this，以及绑定函数的部分参数。

> 函数的部分应用（partial function application） —— 我们通过绑定先有函数的一些参数来创建一个新函数。

```js
function partial(func, ...argsBound) {
  return function(...args) { // (*)
    return func.call(this, ...argsBound, ...args);
  }
}

// 用法：
let user = {
  firstName: "John",
  say(time, phrase) {
    alert(`[${time}] ${this.firstName}: ${phrase}!`);
  }
};

// 添加一个带有绑定时间的 partial 方法
user.sayNow = partial(user.say, new Date().getHours() + ':' + new Date().getMinutes());

user.sayNow("Hello");
// 类似于这样的一些内容：
// [10:00] John: Hello!
```

### 练习题
1. 作为方法的绑定函数
```js
function f() {
  alert( this ); // ?
}

let user = {
  g: f.bind(null)
};

user.g();
```
注：
1. f.bind(null)，这时函数 f() 的 this 为 null，而在非严格模式下，ES5 标准会将值为 null 的 this 绑定到
全局对象，也就是 this=window（在浏览器环境下是 window，在其他环境下不同），所以就得到了
 [object Window]。

2. 那么在严格模式下，f.bind(null) 函数 f() 的 this=null。在本题中，绑定函数的绑定是 hard-bound，所以结
果是 null。

2. 二次 bind
```js
function f() {
  alert(this.name);
}

f = f.bind( {name: "John"} ).bind( {name: "Ann" } );

f();
// 将会输出 John，一个函数不能被重绑定
```

3. bind 后的函数属性
```js
function sayHi() {
  alert( this.name );
}
sayHi.test = 5;

let bound = sayHi.bind({
  name: "John"
});

alert( bound.test ); // 输出将会是什么？为什么？
// undefined, bind 的结果是另一个对象，它没有 test 属性
```

4. 修复丢失了 this 的函数
```js
function askPassword(ok, fail) {
  let password = prompt("Password?", '');
  if (password == "rockstar") ok();
  else fail();
}

let user = {
  name: 'John',

  loginOk() {
    alert(`${this.name} logged in`);
  },

  loginFail() {
    alert(`${this.name} failed to log in`);
  },

};

askPassword(user.loginOk, user.loginFail);
// 改为如下
askPassword(user.loginOk.bind(user), user.loginFail.bind(user));
```

5. 偏函数在登录中的应用
user 对象被修改了。现在不是两个函数 loginOk/loginFail，现在只有一个函数 user.login(true/false)。

在下面的代码中，我们应该向 askPassword 传入什么参数，以使得 user.login(true) 结果是 ok，user.login(false) 结果是 fail？
```js
function askPassword(ok, fail) {
  let password = prompt("Password?", '');
  if (password == "rockstar") ok();
  else fail();
}

let user = {
  name: 'John',

  login(result) {
    alert( this.name + (result ? ' logged in' : ' failed to log in') );
  }
};

// askPassword(?, ?); // ?
askPassword(() => user.login(true), () => user.login(false))
askPassword(user.login.bind(user, true), user.login.bind(user, false));
```

## 深入理解箭头函数
# 深入理解箭头函数
[zh.javascript.info](https://zh.javascript.info/arrow-functions)
> 箭头函数没有 this。如果访问 this，则会从外部获取。

> 不能对箭头函数进行 new 操作 
>   不具有 this 自然也就意味着另一个限制：箭头函数不能用作构造器（constructor）。不能用 new 调用它们。

> 箭头函数 => 和使用 .bind(this) 调用的常规函数之间有细微的差别： 
>     
>     .bind(this) 创建了一个该函数的“绑定版本”。 
>     箭头函数 => 没有创建任何绑定。箭头函数只是没有 this。this 的查找与常规变量的搜索方式完全相同：在外部词法环境中查找。

> 箭头函数也没有 arguments 变量。

> 箭头函数是针对那些没有自己的“上下文”，但在当前上下文中起作用的短代码的。

# 对象属性配置
## 属性标志和属性描述符
[zh.javascript.info](https://zh.javascript.info/property-descriptors)
> writable — 如果为 true，则值可以被修改，否则它是只可读的。 
>   enumerable — 如果为 true，则会被在循环中列出，否则不会被列出。 
>   configurable — 如果为 true，则此属性可以被删除，这些特性也可以被修改，否则不可以。

> Object.getOwnPropertyDescriptor 方法允许查询有关属性的 完整 信息。

> let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);

> 为了修改标志，我们可以使用 Object.defineProperty。

> Object.defineProperty(obj, propertyName, descriptor)

> 如果该属性存在，defineProperty 会更新其标志。否则，它会使用给定的值和标志创建属性；在这种情况下，如果没有提供标志，则会假定它是 false。

## 属性的 getter 和 setter
[zh.javascript.info](https://zh.javascript.info/property-accessors)
> 当读取 obj.propName 时，getter 起作用，当 obj.propName 被赋值时，setter 起作用。

> 从外表看，访问器属性看起来就像一个普通属性。

> 一个属性要么是访问器（具有 get/set 方法），要么是数据属性（具有 value），但不能两者都是。

> 访问器的一大用途是，它们允许随时通过使用 getter 和 setter 替换“正常的”数据属性，来控制和调整这些属性的行为。
```js
function User(name, birthday) {
  this.name = name;
  this.birthday = birthday;

  // 年龄是根据当前日期和生日计算得出的
  Object.defineProperty(this, "age", {
    get() {
      let todayYear = new Date().getFullYear();
      return todayYear - this.birthday.getFullYear();
    }
  });
}

let john = new User("John", new Date(1992, 6, 1));

alert( john.birthday ); // birthday 是可访问的
alert( john.age );      // ……age 也是可访问的
```

# 原型,继承
## 原型继承
[zh.javascript.info](https://zh.javascript.info/prototype-inheritance)
> 对象有一个特殊的隐藏属性 [[Prototype]]（如规范中所命名的），它要么为 null，要么就是对另一个对象的引用。该对象被称为“原型”：

> 使用特殊的名字 __proto__

> 引用不能形成闭环。如果我们试图给 __proto__ 赋值但会导致引用形成闭环时，JavaScript 会抛出错误。 
>   __proto__ 的值可以是对象，也可以是 null。而其他的类型都会被忽略。

> __proto__ 与内部的 [[Prototype]] 不一样。__proto__ 是 [[Prototype]] 的 getter/setter。

> 现代编程语言建议我们应该使用函数 Object.getPrototypeOf/Object.setPrototypeOf 来取代 __proto__ 去 get/set 原型。

> 在一个方法调用中，this 始终是点符号 . 前面的对象。

> for..in 循环也会迭代继承的属性。

> Object.keys 只返回自己的 key

> for..in 会遍历自己以及继承的键

> obj.hasOwnProperty(key)：如果 obj 具有自己的（非继承的）名为 key 的属性，则返回 true。

> for..in 只会列出可枚举的属性

### 练习题
1. 
```js
let animal = {
  jumps: null,
};
let rabbit = {
  __proto__: animal,
  jumps: true,
};

console.log(rabbit.jumps); // true from rabbit

delete rabbit.jumps;

console.log(rabbit.jumps); // null from animal

delete animal.jumps;

console.log(rabbit.jumps); // undefined, no exist
```

2. 搜索算法：给定以下对象
```js
let head = {
  glasses: 1
};

let table = {
  pen: 3
};

let bed = {
  sheet: 1,
  pillow: 2
};

let pockets = {
  money: 2000
};
```
- 使用 __proto__ 来分配原型，以使得任何属性的查找都遵循以下路径：pockets → bed → table → head。例如，pockets.pen 应该是 3（在 table 中找到），bed.glasses 应该是 1（在 head 中找到）。
```js
let head = {
  glasses: 1,
};

let table = {
  pen: 3,
  __proto__: head,
};

let bed = {
  sheet: 1,
  pillow: 2,
  __proto__: table,
};

let pockets = {
  money: 2000,
  __proto__: bed,
};

console.log(pockets.pen); // 3
console.log(bed.glasses); // 1
console.log(table.money); // undefined
```
- 回答问题：通过 pockets.glasses 或 head.glasses 获取 glasses，哪个更快？必要时需要进行基准测试。
在现代引擎中，从性能的角度来看，我们是从对象还是从原型链获取属性都是没区别的。它们（引擎）会记住在哪里找到的该属性，并在下一次请求中重用它。

3. 写在哪里？我们有从 animal 中继承的 rabbit。如果我们调用 rabbit.eat()，哪一个对象会接收到 full 属性：
animal 还是 rabbit？
```js
let animal = {
  eat() {
    this.full = true;
  }
};

let rabbit = {
  __proto__: animal
};

rabbit.eat();
```
rabbit。
这是因为 this 是点符号前面的这个对象，因此 rabbit.eat() 修改了 rabbit。s

4. 我们有两只仓鼠：speedy 和 lazy 都继承自普通的 hamster 对象。
当我们喂其中一只的时候，另一只也吃饱了。为什么？如何修复它？
```js
let hamster = {
  stomach: [],

  eat(food) {
    this.stomach.push(food);
  }
};

let speedy = {
  __proto__: hamster
};

let lazy = {
  __proto__: hamster
};

// 这只仓鼠找到了食物
speedy.eat("apple");
alert( speedy.stomach ); // apple

// 这只仓鼠也找到了食物，为什么？请修复它。
alert( lazy.stomach ); // apple
```
给每个仓鼠都设置一个自己的胃
```js
let speedy = {
  __proto__: hamster,
  stomach: [],
};

let lazy = {
  __proto__: hamster,
  stomach: [],
};
```

## F.prototype
[zh.javascript.info](https://zh.javascript.info/function-prototype)
> 如果 F.prototype 是一个对象，那么 new 操作符会使用它为新对象设置 [[Prototype]]。

> 设置 Rabbit.prototype = animal 的字面意思是：“当创建了一个 new Rabbit 时，把它的 [[Prototype]] 赋值为 animal”。

> 如果在创建之后，F.prototype 属性有了变化（F.prototype = <another object>），那么通过 new F 创建的新对象也将随之拥有新的对象作为 [[Prototype]]，但已经存在的对象将保持旧有的值。

> 默认的 "prototype" 是一个只有属性 constructor 的对象，属性 constructor 指向函数自身。

> F.prototype 的值要么是一个对象，要么就是 null：其他值都不起作用。

> "prototype" 属性仅当设置在一个构造函数上，并通过 new 调用时，才具有这种特殊的影响。

### 练习题
1. 修改 prototype
```js
function Rabbit() {}
Rabbit.prototype = {
  eats: true
};

let rabbit = new Rabbit();

alert( rabbit.eats ); // true
```

```js
function Rabbit() {}
Rabbit.prototype = {
  eats: true
};

let rabbit = new Rabbit();

Rabbit.prototype = {};

alert( rabbit.eats ); // true
// Rabbit.prototype 的赋值操作为新对象设置了 [[Prototype]]，但它不影响已有的对象。
```

```js
function Rabbit() {}
Rabbit.prototype = {
  eats: true
};

let rabbit = new Rabbit();

Rabbit.prototype.eats = false;

alert( rabbit.eats ); // false
// 对象通过引用被赋值。来自 Rabbit.prototype 的对象并没有被赋值，它仍然是被 Rabbit.prototype 
// 和 rabbit 的 [[Prototype]] 引用的单个对象。

// 所以当我们通过一个引用更改其内容时，它对其他引用也是可见的。
```

```js
function Rabbit() {}
Rabbit.prototype = {
  eats: true
};

let rabbit = new Rabbit();

delete rabbit.eats;

alert( rabbit.eats ); // true
// 所有 delete 操作都直接应用于对象。这里的 delete rabbit.eats 试图从 rabbit 中删除 eats 属性，
// 但 rabbit 对象并没有 eats 属性。所以这个操作不会有任何影响。
```

```js
function Rabbit() {}
Rabbit.prototype = {
  eats: true
};

let rabbit = new Rabbit();

delete Rabbit.prototype.eats;

alert( rabbit.eats ); // undefined
// 属性 eats 被从 prototype 中删除，prototype 中就没有这个属性了
```

## 原生的原型
[zh.javascript.info](https://zh.javascript.info/native-prototypes)
> 当 new Object() 被调用（或一个字面量对象 {...} 被创建），按照前面章节中我们学习过的规则，这个对象的 [[Prototype]] 属性被设置为 Object.prototype： 

> 在 Object.prototype 上方的链中没有更多的 [[Prototype]]：

> null 和 undefined 比较特殊。它们没有对象包装器，所以它们没有方法和属性。并且它们也没有相应的原型。

> 原生的原型是可以被修改的。

> 在现代编程中，只有一种情况下允许修改原生原型。那就是 polyfilling。

### 练习题
1. 在所有函数的原型中添加 defer(ms) 方法，该方法将在 ms 毫秒后运行该函数。
```js
Function.prototype.defer = function(ms) {
  setTimeout(this, ms);
};

function f() {
  alert("Hello!");
}

f.defer(1000); // 1 秒后显示 "Hello!"
```

2. 在所有函数的原型中添加 defer(ms) 方法，该方法返回一个包装器，将函数调用延迟 ms 毫秒。
```js
Function.prototype.defer = function (ms) {
  let f = this;
  return function (...args) {
    console.log(args);
    setTimeout(() => f.apply(this, args), ms);
  };
};

function f(a, b) {
  console.log(a + b);
}

f.defer(1000)(1, 2); // 1 秒后显示 3
```

## 原型方法，没有 __proto__ 的对象
[zh.javascript.info](https://zh.javascript.info/prototype-methods)
> 现代的获取/设置原型的方法有： 

>   Object.getPrototypeOf(obj) —— 返回对象 obj 的 [[Prototype]]。 
>   Object.setPrototypeOf(obj, proto) —— 将对象 obj 的 [[Prototype]] 设置为 proto。

> __proto__ 不被反对的唯一的用法是在创建新对象时，将其用作属性：{ __proto__: ... }。

> Object.create(proto, [descriptors]) —— 利用给定的 proto 作为 [[Prototype]] 和可选的属性描述来创建一个空对象。

> 我们可以使用 Object.create 来实现比复制 for..in 循环中的属性更强大的对象克隆方式： 

>   let clone = Object.create(
>   Object.getPrototypeOf(obj),
>   Object.getOwnPropertyDescriptors(obj)
> ); 

>  此调用可以对 obj 进行真正准确地拷贝，包括所有的属性：可枚举和不可枚举的，数据属性和 setters/getters —— 包括所有内容，并带有正确的 [[Prototype]]。

> __proto__ 属性很特殊：它必须是一个对象或者 null。字符串不能成为原型。这就是为什么将字符串赋值给 __proto__ 会被忽略。

> __proto__ 不是对象的属性，而是 Object.prototype 的访问器属性： 

>  因此，如果 obj.__proto__ 被读取或者赋值，那么对应的 getter/setter 会被从它的原型中调用，它会 set/get [[Prototype]]。

> Object.create(null) 创建了一个空对象，这个对象没有原型（[[Prototype]] 是 null）

### 练习题
1.这儿有一个通过 Object.create(null) 创建的，用来存储任意 key/value 对的对象 dictionary。为该对象添加 dictionary.toString() 方法，该方法应该返回以逗号分隔的所有键的列表。你的 toString 方法不应该在使用 for...in 循环遍历数组的时候显现出来。
```js
let dictionary = Object.create(null, {
  toString: {
    value() {
      return Object.keys(this).join();
    }
  }
});

// 你的添加 dictionary.toString 方法的代码

// 添加一些数据
dictionary.apple = "Apple";
dictionary.__proto__ = "test"; // 这里 __proto__ 是一个常规的属性键

// 在循环中只有 apple 和 __proto__
for(let key in dictionary) {
  alert(key); // "apple", then "__proto__"
}

// 你的 toString 方法在发挥作用
console.log(dictionary.toString()); // "apple,__proto__"
```

2. 调用方式的差异
```js
function Rabbit(name) {
  this.name = name;
}
Rabbit.prototype.sayHi = function() {
  alert(this.name);
};

let rabbit = new Rabbit("Rabbit");

rabbit.sayHi(); // Rabbit

// 后三个都是 undefined，都等同于 Rabbit.prototype
Rabbit.prototype.sayHi();
Object.getPrototypeOf(rabbit).sayHi();
rabbit.__proto__.sayHi();
```

# 类
## Class 基本语法
[zh.javascript.info](https://zh.javascript.info/class)

> new 会自动调用 constructor() 方法，因此我们可以在 constructor() 中初始化对象。

> 类的方法之间没有逗号

> class User {...} 构造实际上做了如下的事儿： 
>   
>   创建一个名为 User 的函数，该函数成为类声明的结果。该函数的代码来自于 constructor 方法（如果我们不编写这种方法，那么它就被假定为空）。

> 存储类中的方法，例如 User.prototype 中的 sayHi。

> 通过 class 创建的函数具有特殊的内部属性标记 [[IsClassConstructor]]: true。因此，它与手动创建并不完全相同。

> 与普通函数不同，必须使用 new 来调用它：

> 类方法不可枚举。 类定义将 "prototype" 中的所有方法的 enumerable 标志设置为 false。

> 类总是使用 use strict。 在类构造中的所有代码都将自动进入严格模式。

> 如果类表达式有名字，那么该名字仅在类内部可见：

> “类字段”是一种允许添加任何属性的语法。

> 类字段重要的不同之处在于，它们会在每个独立对象中被设好，而不是设在 User.prototype

> 如果一个对象方法被传递到某处，或者在另一个上下文中被调用，则 this 将不再是对其对象的引用。

```js
class Button {
  constructor(value) {
    this.value = value;
  }

  click() {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // undefined

// 两种修复方法：
// 1. 传递一个包装函数，例如 setTimeout(() => button.click(), 1000)。
// 2. 将方法绑定到对象，例如在 constructor 中。

// 在 class 中使用箭头函数
class Button {
  constructor(value) {
    this.value = value;
  }
  click = () => {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // hello
```

> 类字段 click = () => {...} 是基于每一个对象被创建的，在这里对于每一个 Button 对象都有一个独立的方法，在内部都有一个指向此对象的 this。我们可以把 button.click 传递到任何地方，而且 this 的值总是正确的。

```js
class MyClass {
  prop = value; // 属性

  constructor(...) { // 构造器
    // ...
  }

  method(...) {} // method

  get something(...) {} // getter 方法
  set something(...) {} // setter 方法

  [Symbol.iterator]() {} // 有计算名称（computed name）的方法（此处为 symbol）
  // ...
}
```

### 练习题
1. 重写以下代码
```js
function Clock({ template }) {
  let timer;

  function render() {
    let date = new Date();

    let hours = date.getHours();
    if (hours < 10) hours = '0' + hours;

    let mins = date.getMinutes();
    if (mins < 10) mins = '0' + mins;

    let secs = date.getSeconds();
    if (secs < 10) secs = '0' + secs;

    let output = template
      .replace('h', hours)
      .replace('m', mins)
      .replace('s', secs);

    console.log(output);
  }

  this.stop = function() {
    clearInterval(timer);
  };

  this.start = function() {
    render();
    timer = setInterval(render, 1000);
  };

}

let clock = new Clock({template: 'h:m:s'});
clock.start();
```

```js
class Clock {
  constructor({ template }) {
    this.template = template;
  }

  render() {
    let date = new Date();

    let hours = date.getHours();
    if (hours < 10) hours = "0" + hours;

    let mins = date.getMinutes();
    if (mins < 10) mins = "0" + mins;

    let secs = date.getSeconds();
    if (secs < 10) secs = "0" + secs;

    let output = this.template
      .replace("h", hours)
      .replace("m", mins)
      .replace("s", secs);

    console.log(output);
  }

  stop() {
    clearInterval(this.timer);
  }

  start() {
    this.render();
    this.timer = setInterval(() => this.render(), 1000);
  }
}
```

## 类继承
[zh.javascript.info](https://zh.javascript.info/class-inheritance)
> 类继承是一个类扩展另一个类的一种方式。

> 在内部，关键字 extends 使用了很好的旧的原型机制进行工作。它将 Rabbit.prototype.[[Prototype]] 设置为 Animal.prototype。所以，如果在 Rabbit.prototype 中找不到一个方法，JavaScript 就会从 Animal.prototype 中获取该方法。

> 类语法不仅允许指定一个类，在 extends 后可以指定任意表达式。

> 箭头函数没有 super。 
>    如果被访问，它会从外部函数获取。

> 如果一个类扩展了另一个类并且没有 constructor，那么将生成下面这样的“空” constructor：

> 继承类的 constructor 必须调用 super(...)，并且 (!) 一定要在使用 this 之前调用。

> 父类构造器总是会使用它自己字段的值，而不是被重写的那一个。

> 当父类构造器在派生的类中被调用时，它会使用被重写的方法。 
>  ……但对于类字段并非如此。

> 原因在于字段初始化的顺序。类字段是这样初始化的： 
>   
>   对于基类（还未继承任何东西的那种），在构造函数调用前初始化。 
>   对于派生类，在 super() 后立刻初始化。

### 练习题
1. 创建实例时出错
```js
class Animal {

  constructor(name) {
    this.name = name;
  }

}

class Rabbit extends Animal {
  constructor(name) {
    // this.name = name; 继承 class 需要使用 super
    super(name);
    this.created = Date.now();
  }
}

let rabbit = new Rabbit("White Rabbit"); // Error: this is not defined
alert(rabbit.name);
```

2. 创建一个继承自 Clock 的新的类 ExtendedClock，并添加参数 precision — 每次 “ticks” 之间间隔的
毫秒数，默认是 1000（1 秒）。
```js
class Clock {
  constructor({ template }) {
    this.template = template;
  }

  render() {
    let date = new Date();

    let hours = date.getHours();
    if (hours < 10) hours = '0' + hours;

    let mins = date.getMinutes();
    if (mins < 10) mins = '0' + mins;

    let secs = date.getSeconds();
    if (secs < 10) secs = '0' + secs;

    let output = this.template
      .replace('h', hours)
      .replace('m', mins)
      .replace('s', secs);

    console.log(output);
  }

  stop() {
    clearInterval(this.timer);
  }

  start() {
    this.render();
    this.timer = setInterval(() => this.render(), 1000);
  }
}

class ExtendedClock extends Clock {
  constructor(options) {
    super(options);
    let { precision = 1000 } = options;
    this.precision = precision;
  }

  start() {
    super.render();
    super.timer = setInterval(() => super.render(), this.precision);
  }
}

let lowResolutionClock = new ExtendedClock({
  template: "h:m:s",
  precision: 2000,
});

lowResolutionClock.start();
```

## 静态属性和静态方法
[zh.javascript.info](https://zh.javascript.info/static-properties-methods)
> 把一个方法作为一个整体赋值给类。这样的方法被称为 静态的（static）。

> 静态方法用于实现属于整个类，但不属于该类任何特定对象的函数。

> 静态方法不适用于单个对象 
>    
>    静态方法可以在类上调用，而不是在单个对象上。

> 静态属性和方法是可被继承的。

> 静态方法被用于实现属于整个类的功能。它与具体的类实例无关。

### 练习题
1. 类扩展自对象吗？如果我们像这样 `"class Rabbit extends Object"` 把它明确地写出来，那么结果会与简单的
 `"class Rabbit"` 有所不同么？

```js
class Rabbit extends Object {
  constructor(name) {
    this.name = name;
  }
}

let rabbit = new Rabbit("Rab");

alert( rabbit.hasOwnProperty('name') ); // Error
```

报错的原因：使用 `extends` 时需要调用 `super`，除此之外，两者还存在差异：
extends 会设置两个原型：
1. 在构造函数的 `"prototype"` 之间设置原型（为了获取实例方法）。
2. 在构造函数之间会设置原型（为了获取静态方法）

```js
// 在 class Rabbit extends Object 的例子中
// Rabbit 可以通过 Rabbit 访问 Object 的静态方法
class Rabbit extends Object {}

alert( Rabbit.prototype.__proto__ === Object.prototype ); // (1) true
alert( Rabbit.__proto__ === Object ); // (2) true
```

## 私有的和受保护的属性和方法
[zh.javascript.info](https://zh.javascript.info/private-protected-properties-methods)
> 面向对象编程最重要的原则之一 —— 将内部接口与外部接口分隔开来。

> 内部接口 —— 可以通过该类的其他方法访问，但不能从外部访问的方法和属性。 
>   外部接口 —— 也可以从类的外部访问的方法和属性。

> 受保护的属性通常以下划线 _ 作为前缀。

> 大多数时候首选 get.../set... 函数

> 可以接受多个参数

> 所以受保护的字段是自然可被继承的

> 私有属性和方法应该以 `#` 开头。它们只在类的内部可被访问。

> `#` 是该字段为私有的特殊标志。我们无法从外部或从继承的类中访问它。

> 私有字段不能通过 this[name] 访问

## 扩展内建类
[zh.javascript.info](https://zh.javascript.info/extend-natives)
> 如果我们希望像 map 或 filter 这样的内建方法返回常规数组，我们可以在 Symbol.species 中返
回 Array

```js
// 内建方法将使用这个作为 constructor
static get [Symbol.species]() {
  return Array;
}
```

```js
class PowerArray extends Array {
  isEmpty() {
    return this.length === 0;
  }

  // 内建方法将使用这个作为 constructor
  static get [Symbol.species]() {
    return Array;
  }
}

let arr = new PowerArray(1, 2, 5, 10, 50);
alert(arr.isEmpty()); // false

// filter 使用 arr.constructor[Symbol.species] 作为 constructor 创建新数组
let filteredArr = arr.filter(item => item >= 10);

// filteredArr 不是 PowerArray，而是 Array
alert(filteredArr.isEmpty()); // Error: filteredArr.isEmpty is not a function
```
> 内建类没有静态方法继承

## 类检查："instanceof"
[zh.javascript.info](https://zh.javascript.info/instanceof)
> instanceof 操作符用于检查一个对象是否属于某个特定的 class。同时，它还考虑了继承。

let s = Object.prototype.toString;

alert( s.call(123) ); // [object Number]
alert( s.call(null) ); // [object Null]
alert( s.call(alert) ); // [object Function]
> instanceof 在检查中会将原型链考虑在内,`instanceof` 并不关心函数，而是关心函数的与原型链匹配的 `prototype`。

> objA.isPrototypeOf(objB)，如果 objA 处在 objB 的原型链中，则返回 true。

> 使用 Object.prototype.toString 方法来揭示类型

> 对于 number 类型，结果是 [object Number] 
>   对于 boolean 类型，结果是 [object Boolean] 
>   对于 null：[object Null] 
>   对于 undefined：[object Undefined] 
>   对于数组：[object Array]

```js
let s = Object.prototype.toString;

alert( s.call(123) ); // [object Number]
alert( s.call(null) ); // [object Null]
alert( s.call(alert) ); // [object Function]
```

```js
function A() {}
function B() {}

A.prototype = B.prototype = {};

let a = new A();

alert( a instanceof B ); // true
// instanceof 并不关心函数，而是关心函数的与原型链匹配的 prototype。
```

## Mixin
[zh.javascript.info](https://zh.javascript.info/mixins)
> 在 JavaScript 中，我们只能继承单个对象。每个对象只能有一个 [[Prototype]]。并且每个类只可以扩展另外一个类。

> mixin 是一个包含可被其他类使用而无需继承的方法的类。

> mixin 提供了实现特定行为的方法，但是我们不单独使用它，而是使用它来将这些行为添加到其他类中。

> 在 JavaScript 中构造一个 mixin 最简单的方式就是构造一个拥有实用方法的对象，以便我们可以轻松地将这些实用的方法合并到任何类的原型中。

```js
let sayMixin = {
  say(phrase) {
    alert(phrase);
  }
};

let sayHiMixin = {
  __proto__: sayMixin, // (或者，我们可以在这儿使用 Object.setPrototypeOf 来设置原型)

  sayHi() {
    // 调用父类方法
    super.say(`Hello ${this.name}`); // (*)
  },
  sayBye() {
    super.say(`Bye ${this.name}`); // (*)
  }
};

class User {
  constructor(name) {
    this.name = name;
  }
}

// 拷贝方法
Object.assign(User.prototype, sayHiMixin);

// 现在 User 可以打招呼了
new User("Dude").sayHi(); // Hello Dude!
```

# 错误处理
## 错误处理，"try...catch"
[zh.javascript.info](https://zh.javascript.info/try-catch)
> 要使得 try...catch 能工作，代码必须是可执行的。换句话说，它必须是有效的 JavaScript 代码。 
>    如果代码包含语法错误，那么 try..catch 将无法正常工作

> 因为 try...catch 包裹了计划要执行的函数，该函数本身要稍后才执行，这时引擎已经离开了 try...catch 结构。 
>    为了捕获到计划的（scheduled）函数中的异常，那么 try...catch 必须在这个函数内：

```js
try {
  setTimeout(function() {
    noSuchVariable; // 脚本将在这里停止运行
  }, 1000);
} catch (err) {
  alert( "不工作" );
}

setTimeout(function() {
  try {
    noSuchVariable; // try...catch 处理 error 了！
  } catch {
    alert( "error 被在这里捕获了！" );
  }
}, 1000);
```

## 自定义 error
```js
class ReadError extends Error {
  constructor(message, cause) {
    super(message);
    this.cause = cause;
    this.name = 'ReadError';
  }
}

class ValidationError extends Error { /*...*/ }
class PropertyRequiredError extends ValidationError { /* ... */ }

function validateUser(user) {
  if (!user.age) {
    throw new PropertyRequiredError("age");
  }

  if (!user.name) {
    throw new PropertyRequiredError("name");
  }
}

function readUser(json) {
  let user;

  try {
    user = JSON.parse(json);
  } catch (err) {
    if (err instanceof SyntaxError) {
      throw new ReadError("Syntax Error", err);
    } else {
      throw err;
    }
  }

  try {
    validateUser(user);
  } catch (err) {
    if (err instanceof ValidationError) {
      throw new ReadError("Validation Error", err);
    } else {
      throw err;
    }
  }

}

try {
  readUser('{bad json}');
} catch (e) {
  if (e instanceof ReadError) {
    alert(e);
    // Original error: SyntaxError: Unexpected token b in JSON at position 1
    alert("Original error: " + e.cause);
  } else {
    throw e;
  }
}
```

# Promise, async/await
## Promise
[zh.javascript.info](https://zh.javascript.info/promise-basics)
> Promise 是将“生产者代码”和“消费者代码”连接在一起的一个特殊的 JavaScript 对象。

> 传递给 new Promise 的函数被称为 executor。当 new Promise 被创建，executor 会自动运行。它包含最终应产出结果的生产者代码。

> executor 会自动运行并尝试执行一项工作。尝试结束后，如果成功则调用 resolve，如果出现 error 则调用 reject。

> 由 new Promise 构造器返回的 promise 对象具有以下内部属性： 
>   
>   state —— 最初是 "pending"，然后在 resolve 被调用时变为 "fulfilled"，或者在 reject 被调用时变为 "rejected"。 
>   result —— 最初是 undefined，然后在 resolve(value) 被调用时变为 value，或者在 reject(error) 被调用时变为 error。

> .then 的第一个参数是一个函数，该函数将在 promise resolved 且接收到结果后执行。 
>  .then 的第二个参数也是一个函数，该函数将在 promise rejected 且接收到 error 信息后执行。

```js
new Promise((resolve, reject) => {
  /* 做一些需要时间的事，之后调用可能会 resolve 也可能会 reject */
})
  // 在 promise 为 settled 时运行，无论成功与否
  .finally(() => stop loading indicator)
  // 所以，加载指示器（loading indicator）始终会在我们继续之前停止
  .then(result => show result, err => show error)
```
### 练习题
1. 内建函数 setTimeout 使用了回调函数。请创建一个基于 promise 的替代方案。函数 delay(ms) 应
该返回一个 promise。这个 promise 应该在 ms 毫秒后被 resolve，所以我们可以向其中添加 .then
```js
function delay(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

delay(3000).then(() => alert("runs after 3 seconds"));
```

## Promise 链
[zh.javascript.info](https://zh.javascript.info/promise-chaining)
> 通过 .then 处理程序（handler）链进行传递 result。

> 从技术上讲，我们也可以将多个 .then 添加到一个 promise 上。但这并不是 promise 链（chaining）。

> 异步行为应该始终返回一个 promise。这样就可以使得之后我们计划后续的行为成为可能。即使我们现在不打算对链进行扩展，但我们之后可能会需要。

## 使用 promise 进行错误处理
[zh.javascript.info](https://zh.javascript.info/promise-error-handling)
> 当一个 promise 被 reject 时，控制权将移交至最近的 rejection 处理程序。

> 捕获所有 error 的最简单的方法是，将 .catch 附加到链的末尾

### 练习题
1. setTimeout 中的错误，以下代码的 `catch` 是否会被触发？
```js
new Promise(function(resolve, reject) {
  setTimeout(() => {
    throw new Error("Whoops!");
  }, 1000);
}).catch(alert);
```
函数代码周围有个“隐式的 try..catch”。所以，所有同步错误都会得到处理。
但是这里的错误并不是在 executor 运行时生成的，而是在稍后生成的。因此，promise 无法处理它。

## Promise API
[zh.javascript.info](https://zh.javascript.info/promise-api)
> Promise.all 接受一个可迭代对象（通常是一个数组项为 promise 的数组），并返回一个新的 promise。 
>  当所有给定的 promise 都 resolve 时，新的 promise 才会 resolve，并且其结果数组将成为新 promise 的结果。

> Promise.allSettled 等待所有的 promise 都被 settle，无论结果如何。结果数组具有： 
>   
>   {status:"fulfilled", value:result} 对于成功的响应， 
>   {status:"rejected", reason:error} 对于 error。

> 与 Promise.all 类似，但只等待第一个 settled 的 promise 并获取其结果（或 error）。

> 与 Promise.race 类似，区别在于 Promise.any 只等待第一个 fulfilled 的 promise，并将这个 fulfilled 的 promise 返回。如果给出的 promise 都 rejected，那么返回的 promise 会带有 AggregateError —— 一个特殊的 error 对象，在其 errors 属性中存储着所有 promise error。

## 微任务（Microtask）
[zh.javascript.info](https://zh.javascript.info/microtask-queue)
> promise 的处理程序 .then、.catch 和 .finally 都是异步的。 
>  即便一个 promise 立即被 resolve，.then、.catch 和 .finally 下面 的代码也会在这些处理程序之前被执行。

> 异步任务需要适当的管理。为此，ECMA 标准规定了一个内部队列 PromiseJobs，通常被称为“微任务队列（microtask queue）

> 队列（queue）是先进先出的：首先进入队列的任务会首先运行。 
>   只有在 JavaScript 引擎中没有其它任务在运行时，才开始执行任务队列中的任务。

> 当一个 promise 准备就绪时，它的 .then/catch/finally 处理程序就会被放入队列中：但是它们不会立即被执行。当 JavaScript 引擎执行完当前的代码，它会从队列中获取任务并执行它。

> 如果一个 promise 的 error 未被在微任务队列的末尾进行处理，则会出现“未处理的 rejection”。

## async/await
[zh.javascript.info](https://zh.javascript.info/async-await)
> 在函数前面的 “async” 这个单词表达了一个简单的事情：即这个函数总是返回一个 promise。其他值将自动被包装在一个 resolved 的 promise 中。

> 关键字 await 让 JavaScript 引擎等待直到 promise 完成（settle）并返回结果。

> await 实际上会暂停函数的执行，直到 promise 状态变为 settled，然后以 promise 的结果继续执行。这个行为不会耗费任何 CPU 资源，因为 JavaScript 引擎可以同时处理其他任务：执行其他脚本，处理事件等。

> 不能在普通函数中使用 await

> await 只在 async 函数中有效。

> 要声明一个 class 中的 async 方法，只需在对应方法前面加上 async 即可

> async/await 可以和 Promise.all 一起使用

### 练习题
1. 使用 async/await 重写以下代码
```js
function loadJson(url) {
  return fetch(url)
    .then(response => {
      if (response.status == 200) {
        return response.json();
      } else {
        throw new Error(response.status);
      }
    });
}

loadJson('https://javascript.info/no-such-user.json')
  .catch(alert); // Error: 404

async function loadJson(url) {
  let response = await fetch(url);

  if (response.status == 200) {
    let json = await response.json();
    return json;
  }

  throw new Error(response.status);
}

loadJson('https://javascript.info/no-such-user.json').catch(console.error)
```

2. 使用 async/await 重写以下代码
```js
class HttpError extends Error {
  constructor(response) {
    super(`${response.status} for ${response.url}`);
    this.name = "HttpError";
    this.response = response;
  }
}

async function loadJson(url) {
  let response = await fetch(url);
  if (response.status == 200) {
    return response.json();
  } else {
    throw new HttpError(response);
  }
}

// 询问用户名，直到 github 返回一个合法的用户
async function demoGithubUser() {
  let user;
  while (true) {
    let name = prompt("Enter a name?", "iliakan");

    try {
      user = await loadJson(`https://api.github.com/users/${name}`);
      break; // 没有 error，退出循环
    } catch (err) {
      if (err instanceof HttpError && err.response.status == 404) {
        // 循环将在 alert 后继续
        alert("No such user, please reenter.");
      } else {
        // 未知的 error，再次抛出（rethrow）
        throw err;
      }
    }
  }

  alert(`Full name: ${user.name}.`);
  return user;
}

demoGithubUser();
```

3. 在非 async 函数中调用 async 函数
```js
async function wait() {
  await new Promise(resolve => setTimeout(resolve, 1000));

  return 10;
}

function f() {
  // ……这里你应该怎么写？
  // 我们需要调用 async wait() 并等待以拿到结果 10
  // 记住，我们不能使用 "await"
  wait().then(result => console.log(result));
}

f();
```

# Generator，高级 iteration
## generator
[zh.javascript.info](https://zh.javascript.info/generators)
> generator 可以按需一个接一个地返回（“yield”）多个值。它们可与 iterable 完美配合使用，从而可以轻松地创建数据流。

> 要创建一个 generator，我们需要一个特殊的语法结构：function*，即所谓的 “generator function”。

> generator 函数与常规函数的行为不同。在此类函数被调用时，它不会运行其代码。而是返回一个被称为 “generator object” 的特殊对象，来管理执行流程。

> 一个 generator 的主要方法就是 next()

> next() 的结果始终是一个具有两个属性的对象： 
>   
>   value: 产出的（yielded）的值。 
>   done: 如果 generator 函数已执行完成则为 true，否则为 false。

> function* f(…) 或 function *f(…)？ 
>    
>    这两种语法都是对的。 
>    但是通常更倾向于第一种语法，因为星号 * 表示它是一个 generator 函数，它描述的是函数种类而不是名称，因此 * 应该和 function 关键字紧贴一起。

> generator 是 可迭代（iterable）的。 
>  我们可以使用 for..of 循环遍历它所有的值：

> 当 done: true 时，for..of 循环会忽略最后一个 value。因此，如果我们想要通过 for..of 循环显示所有的结果，我们必须使用 yield 返回它们：

> generator 是可迭代的，我们可以使用 iterator 的所有相关功能，例如：spread 语法 ...

> 对于 generator 而言，我们可以使用 yield* 这个特殊的语法来将一个 generator “嵌入”（组合）到另一个 generator 中：

> yield* 指令将执行 委托 给另一个 generator。这个术语意味着 yield* gen 在 generator gen 上进行迭代，并将其产出（yield）的值透明地（transparently）转发到外部。就好像这些值就是由外部的 generator yield 的一样。

> yield 是一条双向路（two-way street）：它不仅可以向外返回结果，而且还可以将外部的值传递到 generator 内。

```js
function* gen() {
  // 向外部代码传递一个问题并等待答案
  let result = yield "2 + 2 = ?"; // (*)

  alert(result);
}

let generator = gen();

let question = generator.next().value; // <-- yield 返回的 value

generator.next(4); // --> 将结果传递到 generator 中
```

> generator 和调用 generator 的代码可以通过在 next/yield 中传递值来交换结果。

> 每个 next(value)（除了第一个）传递一个值到 generator 中，该值变成了当前 yield 的结果，然后获取下一个 yield 的结果。

> generator.return(value) 完成 generator 的执行并返回给定的 value。

### 练习题
1. “种子伪随机（seeded pseudo-random）generator”。它们将“种子（seed）”作为第一个值，然后使用公式生成下一个值。以便相同的种子（seed）可以产出（yield）相同的序列，因此整个数据流很容易复现。我们只需要记住种子并重复它即可。

```js
function* pseudoRandom(seed) {
  let value = seed;

  while (true) {
    value = (value * 16807) % 2147483647;
    yield value;
  }
}

let generator = pseudoRandom(1);

log(generator.next().value);
log(generator.next().value);
log(generator.next().value);
```

## 异步迭代和 generator
[zh.javascript.info](https://zh.javascript.info/async-iterators-generators)
> 异步迭代允许我们对按需通过异步请求而得到的数据进行迭代。

> 为了使一个对象可以异步迭代，它必须具有方法 Symbol.asyncIterator 

> 这个方法必须返回一个带有 next() 方法的对象，next() 方法会返回一个 promise

> 这个 next() 方法可以不是 async 的，它可以是一个返回值是一个 promise 的常规的方法，但是使用 async 关键字可以允许我们在方法内部使用 await，所以会更加方便。

> 我们使用 for await(let value of range) (4) 来进行迭代，也就是在 for 后面添加 await。它会调用一次 range[Symbol.asyncIterator]() 方法一次，然后调用它的 next() 方法获取值。

> Spread 语法 ... 无法异步工作

> generator，它使我们能够写出更短的迭代代码。在大多数时候，当我们想要创建一个可迭代对象时，我们会使用 generator。

> 当我们想创建一个异步生成一系列值的对象时，我们都可以使用异步 generator。

> 在 function* 前面加上 async。这即可使 generator 变为异步的。 
>  然后使用 for await (...) 来遍历它

> 对于异步 generator，generator.next() 方法是异步的，它返回 promise。

> 在一个常规的 generator 中，我们使用 result = generator.next() 来获得值。但在一个异步 generator 中，我们应该添加 await 关键字

> 常规的 generator 可用作 Symbol.iterator 以使迭代代码更短。

> 异步 generator 可用作 Symbol.asyncIterator 来实现异步迭代。

![image.png](../assets/image_1676730478134_0.png)

```js
let range = {
  from: 1,
  to: 5,

  // 这一行等价于 [Symbol.asyncIterator]: async function*() {
  async *[Symbol.asyncIterator]() {
    for(let value = this.from; value <= this.to; value++) {

      // 在 value 之间暂停一会儿，等待一些东西
      await new Promise(resolve => setTimeout(resolve, 1000));

      yield value;
    }
  }
};

(async () => {

  for await (let value of range) {
    alert(value); // 1，然后 2，然后 3，然后 4，然后 5
  }

})();
```

# 模块
## 模块简介
[zh.javascript.info](https://zh.javascript.info/modules-intro)
> 一个模块（module）就是一个文件。一个脚本就是一个模块。

> export 关键字标记了可以从当前模块外部访问的变量和函数。

> import 关键字允许从其他模块导入功能。

> 模块始终在严格模式下运行

> 每个模块都有自己的顶级作用域（top-level scope）。换句话说，一个模块中的顶级作用域变量和函数在其他脚本中是不可见的。

> 如果同一个模块被导入到多个其他位置，那么它的代码只会执行一次，即在第一次被导入时。然后将其导出（export）的内容提供给进一步的导入（importer）。

> 首先，如果执行一个模块中的代码会带来副作用（side-effect），例如显示一条消息，那么多次导入它只会触发一次显示 —— 即第一次：

> 模块导出一些配置方法，例如一个配置对象。 
>   在第一次导入时，我们对其进行初始化，写入其属性。可以在应用顶级脚本中进行此操作。 
>   进一步地导入使用模块。

> import.meta 对象包含关于当前模块的信息。 
>  它的内容取决于其所在的环境。在浏览器环境中，它包含当前脚本的 URL，或者如果它是在 HTML 中的话，则包含当前页面的 URL。

> 在一个模块中，顶级 this 是 undefined。

> 模块脚本 总是 被延迟的

> 模块脚本是被延迟的，所以要等到 HTML 文档被处理完成才会执行它。而常规脚本则会立即运行，所以我们会先看到常规脚本的输出。

## 导出与导入
[zh.javascript.info](https://zh.javascript.info/import-export)
> 可以通过在声明之前放置 export 来标记任意声明为导出，无论声明的是变量，函数还是类都可以。

> 导出 class/function 后没有分号

> 通常，我们把要导入的东西列在花括号 import {...} 中

> 如果有很多要导入的内容，我们可以使用 import * as <obj> 将所有内容导入为一个对象

> 可以使用 as 让导入具有不同的名字。

> 模块提供了一个特殊的默认导出 export default 语法

> 每个文件应该只有一个 export default：

> import 命名的导出时需要花括号，而 import 默认的导出时不需要花括号。

## 动态导入
[zh.javascript.info](https://zh.javascript.info/modules-dynamic-imports)
> import(module) 表达式加载模块并返回一个 promise，该 promise resolve 为一个包含其所有导出的模块对象。

> 尽管 import() 看起来像一个函数调用，但它只是一种特殊语法，只是恰好使用了括号（类似于 super()）。 
>    因此，我们不能将 import 复制到一个变量中，或者对其使用 call/apply。因为它不是一个函数。
