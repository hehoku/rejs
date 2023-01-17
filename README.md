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
