# 1. ES6

[ECMAScript 6 文档](https://es6.ruanyifeng.com/?search=%E5%BB%B6%E5%B1%95&x=0&y=0)

**ECMAScript 和 JavaScript 的关系**

前者是后者的规格，后者是前者的一种实现。

**ES6 与 ECMAScript 2015 的关系**	

ES6泛指5.1版以后的JavaScript语言的下一个版本。

**Node.js** 是 JavaScript 的服务器运行环境

**Babel 转码器：**

 Babel是ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在老版本的浏览器执行。

**（1）安装：** （在项目目录中）

`$ npm install --save-dev @babel/core`

**（2）配置：** （项目的根目录下）

Babel的配置文件是`.babelrc`，该文件用来设置转码规则和插件

```js
{
  "presets": [], //presets字段设定转码规则
  "plugins": []
}
```

# 2. ES6新增语法

ES5 只有两种声明变量的方法：`var`命令和`function`命令。

ES6声明包括：ES5的两种命令、`let`命令、`const`命令、`import`命令、`class`命令。

## **2.1 let命令**

ES5缺点：

- 只有全局作用域和函数作用域，没有块级作用域；
- 会导致内层变量可能会覆盖外层变量；
- 用来计数的循环变量泄露为全局变量；
- 函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。

--------

ES6 新增了`let`命令，用来声明**变量**。

**（1）用法：**

```js
{
  let a = 10;
  //var b = 1;
}
```

**（2）特点：**

- **具有块级作用域**

let的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效，具有块级作用域。

使用let关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性。

块级作用域：必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。

- **防止循环变量变成全局变量**

- **不存在变量提升**

let命令改变了语法行为，变量必须要在声明后才能使用，否则报错。

```js
console.log(a); // a is not defined 
 let a = 20;
```

- **暂时性死区**

只要块级作用域内存在let命令，它所声明的变量就绑定了这个区域，不再受外部的影响。

```js
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError，未声明
  let tmp;
}
```

- **不允许重复声明**

let不允许在相同作用域内，重复声明同一个变量。

```js
// 报错
function func() {
  let a = 10;
  let a = 1;
}
```

不能在函数内部重新声明参数。

```js
function func(arg) {
  let arg;
}
func() // 报错

function func(arg) {
  {
    let arg;
  }
}
func() // 不报错
```

## **2.2 const命令**

ES6 新增了`const`命令，用来声明**常量**。

**（1）用法：**

```js
const PI = 3.1415;
```

**（2）特点**

- cosnt声明一个只读的常量。一旦声明，常量的值就不能改变；
- const声明常量时必须赋初始值；
- const的作用域与 let 命令相同：只能在声明的位置后面使用；具有块级作用域；不可重复声明。

```js
const PI = 3.1415;
const arr = [100, 200];
arr[0] = 123;
console.log(arr); //[123, 200]
arr = [1,2]; //报错
```

--------

**let、const、var 的区别**

var声明的变量，其作用域为该语句所在的函数内；

let声明的变量、const声明的常量，其作用域为该语句所在的代码块内；

| var          | let            | const          |
| ------------ | -------------- | -------------- |
| 函数级作用域 | 块级作用域     | 块级作用域     |
| 变量提升     | 不存在变量提升 | 不存在变量提升 |
| 值可更改     | 值可更改       | 值不可更改     |

--------



**顶层对象**

顶层对象：在浏览器环境指的是`window`对象，在 Node 指的是`global`对象。

ES5 中，顶层对象的属性与全局变量是等价的。

ES6中，`var`命令和`function`命令声明的全局变量，依旧是顶层对象的属性；`let`命令、`const`命令、`class`命令声明的全局变量，**不属于**顶层对象的属性。

```js
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```

**globalThis对象**

由于为了让同一段代码在各种环境中都能取到顶层对象，有着局限性。因此[ES2020](https://github.com/tc39/proposal-global) 在语言标准的层面，引入`globalThis`作为顶层对象。

globalThis，在任何环境下都能够取到顶层对象，指向全局环境下的this。

**this变量：**

- 全局环境中，this会返回顶层对象；Node.js 模块中this返回的是当前模块；ES6 模块中this返回的是undefined。
- 函数里面的this，如果函数不是作为对象的方法运行，而是单纯作为函数运行，this会指向顶层对象。但是，严格模式下，这时this会返回undefined。
- 不管是严格模式，还是普通模式，`new Function('return this')()`，总是会返回全局对象。但是，如果浏览器用了 CSP（Content Security Policy，内容安全策略），那么eval、new Function这些方法都可能无法使用。

## 2.3 解构赋值

### 2.3.1 数组的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对**变量**进行赋值，这被称为**解构**。

**（1）用法**

```js
//以前为变量赋值
let a = 1;
let b = 2;

//es6
let [a, b, c] = [1, 2, 3];
let [x, y, z] = new Set(['a', 'b', 'c']); //Set 结构
```

本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。

如果解构不成功，变量的值为undefined。

```js
let [foo] = []; //变量没有对应的值
let [bar, foo] = [1];
```

只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

**（2）默认值**

解构赋值允许指定默认值。

```js
et [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

只有当一个数组成员严格等于`undefined`，默认值才会生效。

### 2.3.2 对象的解构赋值

**（1）用法**

```js
用法一：对象的属性
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
console,log(foor); // 'aaa'
//或者
let { foor: myfoor, bar: mybar} = { foo: 'aaa', bar: 'bbb' };
console.log(foor); // 'aaa'

用法二：将现有对象的方法，赋值到某个变量。
let { log, sin, cos } = Math;  //将Math对象的对数、正弦、余弦三个方法，赋值到对应的变量上，
```

**对象的解构与数组的区别：**

数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值，否则为undefined 。

**（2）默认值**

对象的解构也可以指定默认值。

默认值生效的条件是，对象的属性值严格等于undefined。

```js
var {x = 3} = {};
x // 3

var {x, y = 5} = {x: 1};
x // 1
y // 5

var {x: y = 3} = {};
y // 3

var {x: y = 3} = {x: 5};
y // 5
```

**注意：**

- 如果要将一个已经声明的变量用于解构赋值，必须非常小心。

```js
// 错误的写法 JavaScript 引擎会将{x}理解成一个代码块，从而发生语法错误。
let x;
{x} = {x: 1};
// 正确的写法
let x;
({x} = {x: 1});
```

- 解构赋值允许等号左边的模式之中，不放置任何变量名

```js
({} = [true, false]);
({} = 'abc');
```

- 由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

```js
let arr = [1, 2, 3];
let {0 : first, [arr.length - 1] : last} = arr;
first // 1
last // 3
```

### 2.3.3 字符串的解构赋值

此时，字符串被转换成了一个类似数组的对象。

```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
```

类似数组的对象都有一个`length`属性，因此还可以对这个属性解构赋值。

```js
let {length : len} = 'hello';
len // 5
```

### 2.3.4 数值和布尔值的解构赋值

解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

```javascript
let {toString: s} = 123;
s === Number.prototype.toString // true
```

**解构赋值的规则**是，只要等号右边的值不是对象或数组，就先将其转为对象。由于`undefined`和`null`无法转为对象，所以对它们进行解构赋值，都会报错。

```javascript
let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
```

### 2.3.5 函数参数的解构赋值

```javascript
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

上面代码中，函数`add`的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量`x`和`y`。对于函数内部的代码来说，它们能感受到的参数就是`x`和`y`。

### 3.6 圆括号问题

ES6 的规则是，只要有可能导致解构的歧义，就不得使用圆括号。

**（1）不能使用圆括号的情况：**

- 变量声明语句

```javascript
// 全部报错
let [(a)] = [1];
let {x: (c)} = {};
let { o: ({ p: p }) } = { o: { p: 2 } };
```

- 函数参数

函数参数也属于变量声明，因此不能带有圆括号。

```js
function f([(z)]) { return z; } // 报错
```

- 赋值语句的模式

```javascript
({ p: a }) = { p: 42 };// 全部报错
([a]) = [5];
```

**（2）可以使用圆括号的情况**

- 赋值语句的非模式部分

```javascript
[(b)] = [3]; // 正确
({ p: (d) } = {}); // 正确
```

## 2.4 箭头函数

ES6中新增的定义函数的方式。

```js
//() => {} 
const fn = () => {}
```

- 如果函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号：

```js
 function sum(num1, num2) { 
     return num1 + num2; 
 }
 const sum = (num1, num2) => num1 + num2;
```

- 如果形参只有一个，可以省略小括号

```js
 function fn (v) {
     return v;
 } 
 const fn = v => v;
```

- 箭头函数不绑定this关键字，如果箭头函数使用this，指向的是函数定义位置的上下文this。

````js
var age = 100;
//如果全局作用域没有定义 var age 此时输出undefined
		var obj = {  //obj是对象，没有作用域
			age: 20,
			say: () => {
				alert(this.age) //输出100
			}
		}

		obj.say();
````



## 2.5 剩余参数

- 当函数实参个数大于形参个数时，可以将剩余的实参放入一个数组中。

```js
function sum (first, ...args) {
     console.log(first); // 10
     console.log(args); // [20, 30] 
 }
 sum(10, 20, 30)
```

- 剩余参数和解构配合使用

```js
 let [s1, ...s2] = ['wangwu', 'zhangsan', 'lisi'];
 console.log(s1);  // 'wangwu' 
 console.log(s2);  // ['zhangsan', 'lisi']
```

# 3.  ES6新增扩展

## 3.1 字符串String的扩展

**（1）模板字符串**

- ES6新增的创建字符串的方式，使用反引号定义。

```js
let name = `zhangsan`;
```

- 模板字符串中可以解析变量

```js
let name = 'xx'; 
//let sayHello = `hell,my name is` + name; 在模板字符串中可以直接在引号里用 ${name} 获取
let sayHello = `hello,my name is ${name}`; // hello, my name is xx
```

- 模板字符串中可以换行

```html
let result = {
    name: 'xx',
    age: 18
}
let html = `
	<div>
		<span>${resule.name}</span>
		<span>${resulet.age}</span>
	</div>
`;
```

- 在模板字符串中可以调用函数。

```js
const fn = () => {
    return 'xxx'
}
let html = 'yyy ${fn()}';
console.log(html); //输出yyyxxx
```

**（2）实例方法**

- **startsWith()** **和** **endsWith()**

startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值

endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值

```js
let str = 'Hello world!';
 str.startsWith('Hello') // true 
 str.endsWith('!')       // true
```

- **repeat()**

repeat方法表示将原字符串重复n次，返回一个新字符串。

```js
'x'.repeat(3)      // "xxx" 
'hello'.repeat(2)  // "hellohello"
```

## 3.2 数组Array的扩展

**（1）扩展运算符（展开语法）**

扩展运算符`...`

- 扩展运算符可以将数组或者对象转为用逗号分隔的参数序列。

```js
let ary = [1, 2, 3];
 ...ary  // 1, 2, 3
 console.log(...ary);    // 1 2 3  相当于console.log(1, 2, 3);
 console.log(1, 2, 3)
```

- 扩展运算符可以应用于**合并数组**。

```js
// 方法一 
 let ary1 = [1, 2, 3];
 let ary2 = [3, 4, 5];
 let ary3 = [...ary1, ...ary2];
 // 方法二 
 ary1.push(...ary2);
```

- 将伪数组或可遍历对象转换为真正的数组

```js
let oDivs = document.getElementsByTagName('div'); 
oDivs = [...oDivs];
```

**（2）构造函数方法：**

- **Array.from()**

将伪数组或可遍历对象转换为真正的数组

```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
}; 
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

```js
let arrayLike = { 
     "0": 1,
     "1": 2,
     "length": 2
 }
 let newAry = Array.from(aryLike, item => item *2) // item代表当前要处理的值
 // item => item * 2 相当于， (item) => { return item * 2}
```

- **Array.of()**

该方法用于将一组值，转换为数组。

```js
Array.of(3, 11, 8) // [3,11,8]
Array.of() // []
Array.of(3).length // 1
```

**（3）实例方法：**

- **find()**

用于找出第一个符合条件的数组成员，如果没有找到返回undefined

```js
let ary = [{
     id: 1,
     name: '张三‘
 }, { 
     id: 2,
     name: '李四‘
 }]; 
 let target = ary.find(item => item.id == 2); 
```

- **findIndex()**

用于找出第一个符合条件的数组成员的位置，如果没有找到返回-1

```js
let ary = [1, 5, 10, 15];
let index = ary.findIndex((value, index) => value > 9);  //index是索引号
console.log(index); // 2
```

- **includes()**

表示某个数组是否包含给定的值，返回布尔值

```js
[1, 2, 3].includes(2) // true 
[1, 2, 3].includes(4) // false
```

## 3.3 数值的扩展

### 3.3.1 Number对象

**（1）二进制和八进制表示法**

ES6 提供了二进制和八进制数值的新的写法，分别用前缀`0b`（或`0B`）和`0o`（或`0O`）表示。

```javascript
0b111110111 === 503 // true
0o767 === 503 // true
```

如果要将`0b`和`0o`前缀的字符串数值转为十进制，要使用`Number`方法。

```js
Number('0b111')  // 7
Number('0o10')  // 8
```

**（2）Number.isFinite()和Number.isNaN()** 

ES6在Number对象上，新提供了`Number.isFinite()`、` Number.isNaN() `

- Number.isFinite()用来检查一个数值是否为有限的（finite）;

```js
Number.isFinite(15); // true
Number.isFinite(Infinity); // false
```

注意：如果参数不是数值，则一律返回false。

- Number.isNaN()用来检查一个值是否为NaN（非数字）。

```js
Number.isNaN(15); //false
Number.isNaN(9/NaN); //true
```

注意：如果参数类型不是NaN，一律返回false。

它们与传统的全局方法`isFinite()`和`isNaN()`的区别在于，传统方法先调用`Number()`将非数值的值转为数值，再进行判断，而这两个新方法只对数值有效，返回true

**（3）Number.parseInt()和Number,parseFloat()**

ES6将全局方法`parseInt()`和`parseFloat()`（转换为数字型），移植到`Number`对象上面，行为完全保持不变。

```javascript
// ES5的写法
parseInt('12.34') // 12
parseFloat('123.45#') // 123.45

// ES6的写法
Number.parseInt('12.34') // 12
Number.parseFloat('123.45#') // 123.45
```

这样做的目的，是逐步减少全局性方法，使得语言逐步模块化。

**（4）Number.isInteger()**

Number.isInteger() 用来判断一个数值是否为整数。

如果参数不是数值，Number.isInteger()返回false

如果对数据精度的要求较高，不建议使用Number.isInteger()判断一个数值是否为整数。（根据53个二进制位，可能会出现判断错误）

```js
Number.isInteger(25) // true
Number.isInteger(25.1) // false
```

JavaScript 内部，整数和浮点数采用的是同样的储存方法，所以 25 和 25.0 被视为同一个值。

```js
Number.isInteger(25) // true
Number.isInteger(25.0) // true
```

**（5）Number.EPSILON**

ES6新增一个极小的常量，它表示 1 与大于 1 的最小浮点数之间的差。

该方法可用于浮点数计算。

### 3.3.2 Math对象

ES6 在 Math 对象上新增了 17 个与数学相关的方法。所有这些方法都是静态方法，只能在 Math 对象上调用。

**（1）Math.trunc()**

该方法用于去除一个数的小数部分，返回整数部分。

```js
Math.trunc(4.1) // 4
Math.trunc(-4.9) // -4
Math.trunc(-0.1234) // -0
```

对于非数值，Math.trunc内部使用Number方法将其先转为数值。

对于空值和无法截取整数的值，返回`NaN`。

```javascript
Math.trunc('123.456') // 123
Math.trunc(true) //1
Math.trunc(false) // 0
Math.trunc(null) // 0
```

**（2）Math.sign()**

该方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。

它会返回五种值。

- 参数为正数，返回+1；
- 参数为负数，返回-1；
- 参数为 0，返回0；
- 参数为-0，返回-0;
- 其他值，返回NaN；
- 如果参数是非数值，会自动转为数值。对于那些无法转为数值的值，会返回NaN

**（3）Math.cbrt()**

该方法用于计算一个数的立方根。

对于非数值，Math.cbrt()方法内部也是先使用Number()方法将其转为数值，非数值返回NaN。

**（4）Math.hypot**

该方法返回所有参数的平方和的平方根。

如果参数不是数值，Math.hypo方法会将其转为数值。只要有一个参数无法转为数值，就会返回 NaN。

**（5）对数方法**

ES6 新增了 4 个对数相关方法。

| 方法         | 说明                                                    |
| ------------ | ------------------------------------------------------- |
| Math.expm1() | 返回 e^x - 1，即Math.exp(x) - 1。                       |
| Math.log1p() | 返回1+x的自然对数，即Math.log(1+X)，如果小于-1，返回NaN |
| Math.log10() | 返回以 10 为底的x的对数，如果x小于 0，则返回 NaN        |
| Math.log2()  | 返回以 2 为底的x的对数，如果x小于 0，则返回 NaN         |

**（6）双曲函数方法**

ES6新增了6个双曲函数方法。

**（7）指数运算符**

ES2016 新增了一个指数运算符（**）。

```javascript
2 ** 2 // 4
2 ** 3 // 8
```

# 4. BigInt

## 4.1 BigInt数据类型

[ES2020](https://github.com/tc39/proposal-bigint) 引入了一种新的数据类型 BigInt（大整数）

BigInt 只用来表示整数，没有位数的限制，任何位数的整数都可以精确表示。

- 为了与 Number 类型区别，BigInt 类型的数据必须添加后缀`n`。
- BigInt 同样可以使用各种进制表示，都要加上后缀`n`。
- BigInt 与普通整数是两种值，它们之间并不相等
- typeof运算符对于 BigInt 类型的数据返回`bigint`。
- BigInt 可以使用负号（`-`），但是不能使用正号（`+`），因为会与 asm.js 冲突。

```js
1234 // 普通整数
1234n // BigInt

// BigInt 的运算
1n + 2n // 3n

42n === 42 // false
```

## 4.2 BigInt对象

JavaScript 原生提供BigInt对象，可以用作构造函数生成 BigInt 类型的数值。转换规则基本与`Number()`一致，将其他类型的值转为 BigInt。

BigInt()构造函数必须有参数，而且参数必须可以正常转为数值，否则报错。参数如果是小数，也会报错。

**（1）转换规则**

可以使用`Boolean()`、`Number()`和`String()`这三个方法，将 BigInt 可以转为布尔值、数值和字符串类型。

另外，取反运算符 ! 也可以将 BigInt 转为布尔值。

```js
Boolean(0n) // false
Boolean(1n) // true
Number(1n)  // 1
String(1n)  // "1"

!0n // true
!1n // true
```

**（2）数学运算**

BigInt 类型的`+`、`-`、`*`和`**`这四个二元运算符，与 Number 类型的行为一致。除法运算`/`会舍去小数部分，返回一个整数。

以下两个情况不能使用BigInt：

- 不带符号的右移位运算符`>>>`
- 一元的求正运算符`+`

BigInt 不能与普通数值进行混合运算。

```js
1n + 1.3 // 报错
```

igInt 与字符串混合运算时，会先转为字符串，再进行运算。

```js
'' + 123n // "123"
```



# 5. Set 数据结构

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

Set本身是一个构造函数，用来生成 Set 数据结构。

```
const s = new Set();
```

Set函数可以接受一个数组作为参数，用来初始化。

```js
const set = new Set([1,2,4]);
```

例子：

```js
const s1 = new Set(['a', 'a', 'b', 'b']);
console.log(s1.size); //2
const ary = [...s1];
console.log(ary); //(2) ["a", "b"]
```

**（1）实例方法**

- add(value)：添加某个值，返回 Set 结构本身

- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功

- has(value)：返回一个布尔值，表示该值是否为 Set 的成员

- clear()：清除所有成员，没有返回值

```js
 const s = new Set();
 s.add(1).add(2).add(3); // 向 set 结构中添加值 
 s.delete(2)             // 删除 set 结构中的2值 
 let result = s.has(1);
 console.log(result);    // 表示 set 结构中是否有1这个值 返回布尔值 
 s.clear()               // 清除 set 结构中的所有值
```

**（2）遍历**

Set 结构的实例与数组一样，也拥有`forEac`h方法，用于对每个成员执行某种操作，没有返回值。

```js
const s = new Set(['a', 'b', 'c']);
s.forEach(value = > {
    console.log(value); //a b c
})
```

# 6. 类class

**对象：**

在 JavaScript 中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串、数值、数组、函数等。

## 6.1 类class的用法

类抽象了**对象**的公共部分，它泛指某一大类（class）

**（1）创建类：**

``` js
class name {
    // 类的共有属性放到 constructor 里面
    constructor() {}
    //用this调用属性 this.属性名 = 属性值；
} 

//创建实例
var xx = new name();
```

注意： 

- 通过class 关键字创建类，类名我们还是习惯性定义首字母大写
- 类**必须使用** new 实例化对象，new不能省略
- 类里面有个constructor 函数，可以接受传递过来的**参数**,同时返回实例对象
- constructor 函数 只要 new 生成实例时,就会自动调用这个函数, 如果我们不写这个函数，类也会自动生成这个函数
- 语法规范：创建类：类名后面不要加小括号，生成实例：类名后面加小括号，构造函数不需要加function

**（2）类添加方法：**

```js
class name {
    constructor() {}
    方法名() {}
} 

var xx = new name();
xx.方法名();
```

- 类里面所有的函数不需要写function 
- 类里面多个函数方法之间不需要添加逗号分隔
- 方法还可以接受传递过来的参数

## 6.2 类class的继承

**（1）语法**

```js
class Father{   // 父类
} 
class Son extends Father {  // 子类继承父类
}
```

**（2）super 关键字**

super 关键字用于访问和调用对象父类上的函数。（可以调用父类的**构造函数**，也可以调用父类的**普通函数**。）

例子：

```js
class Father {
            constructor(x, y) {
                this.x = x;
                this.y = y;
            }
            sum() {
                console.log(this.x + this.y);
            }
        }
        class Son extends Father {
            constructor(x, y) {
                super(x, y); //调用了父类中的构造函数
            }
        }
        var son = new Son(1, 2);
        var son1 = new Son(11, 22);
        son.sum();
        son1.sum();
```

- 继承中的属性或者方法查找原则: 就近原则
- 注意: 子类在构造函数中使用super, 必须放到 this 前面  (必须先调用父类的构造方法,在使用子类构造方法)

```js
// super 关键字调用父类普通函数
        class Father {
            say() {
                return 'xx';
            }
        }
        class Son extends Father {
            say() {
                console.log(super.say() + 'yy');  //输出xxyy
                // super.say() 就是调用父类中的普通函数 say()
            }
        }
        var son = new Son();
        son.say();
```

**（3）注意**

- 类里面的共有属性和方法**一定**要加this使用.

- 类里面的this指向问题：constructor 里面的this指向实例对象,；方法里面的this 指向这个方法的调用者

- 在 ES6 中类没有变量提升，所以必须先定义类，才能通过类实例化对象
