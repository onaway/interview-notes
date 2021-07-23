### 一、ES7

#### 1、Array.prototype.includes()

在 **ES6** 中有 `String.prototype.includes()` 可以查询给定字符串是否包含一个字符

`Array.prototype.includes()` 方法来判断一个数组是否包含一个指定的值，有返回 true，否则返回 false

#### 2、求幂运算符 **

具有与 `Math.pow()` 等效的计算结果

```js
console.log(2**10);		// 输出1024
console.log(Math.pow(2, 10)) // 输出1024
```



### 二、ES8

#### 1、Async/Await

> 提供了在不阻塞主线程的情况下使用同步代码实现异步访问资源的能力

- 支持 try catch 来捕获异常
- await 不可以脱离 async 单独使用
- await 后面一定是 Promise 对象，如果不是会自动包装成 Promise 对象
- async 是一个通过异步执行并隐式返回 Promise 作为结果的函数

#### 2、Object.values()，Object.entries()

- `Object.values()` 方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值

  - **如果属性名是数值类型的，是按照数值大小，从小到大遍历的**

  ```js
  const obj = { 100: 'a', 2: 'b', 7: 'c' };
  Object.values(obj) // ["b", "c", "a"]
  ```

- `Object.entries()` 方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组

#### 3、padding

- **str.padStart(targetLength, string)**：使用指定字符串填充到目标字符串前面，使其达到目标长度；

- **str.padEnd(targetLength, string)**：使用指定字符串填充到目标字符串后面，使其达到目标长度

#### 4、Object.getOwnPropertyDescriptors()

> 返回指定对象所有自身属性（非继承属性）的描述对象

该方法的引入目的，主要是为了解决 Object.assign() 无法正确拷贝 get 属性和 set 属性的问题


### 三、ES9

#### 1、for await of

> 可以用来遍历具有 Symbol.asyncIterator 方法的数据结构，也就是异步迭代器，且会等待前一个成员的状态改变后才会遍历到下一个成员

#### 2、扩展运算符 ...

- 数组合并：`[...arr1, ...arr2]`
- 复制数组：`[...arr]`
- 拆解数组：`...arr`
- 拷贝对象（浅拷贝）：`{ ...obj }`

#### 3、Promise.prototype.finally()

> 返回一个 Promise，在 promise 执行结束时，无论结果是 fulfilled 或者是 rejected，在执行 then() 和catch() 后，都会执行 finally 指定的回调函数

#### 4、新的正则表达式特性

##### 4.1、s(dotAll)flag

换行符(\n)或回车符(\r)，可以通过ES9的s(dotAll)flag，在原正则表达式基础上添加s表示：

```js
console.log(/foo.bar/.test('foo\nbar'))  // false
console.log(/foo.bar/s.test('foo\nbar')) // true
```

##### 4.2、命名捕获组

允许为每一个组匹配指定一个名字，既便于阅读代码，又便于引用

“命名捕获组”在圆括号内部，模式的头部添加“问号 + 尖括号 + 组名”（?），然后就可以在 exec 方法返回结果的 groups 属性上引用该组名

```js
const reg = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
const match = reg.exec('2019-01-01');
console.log(match.groups);          // → {year: "2019", month: "01", day: "01"}
console.log(match.groups.year);     // → 2019
console.log(match.groups.month);    // → 01
console.log(match.groups.day);      // → 01
```

##### 4.3、Lookbehind 后行断言

正则表达式的先行断言：

```js
let test = 'hello world'
console.log(test.match(/hello(?=\sworld)/))
// ["hello", index: 0, input: "hello world", groups: undefined]
```

正则表达式的后行断言：

```js
let test = 'world hello'
console.log(test.match(/(?<=world\s)hello/))
// ["hello", index: 6, input: "world hello", groups: undefined]
```

**(?<…)是后行断言的符号，(?..)是先行断言的符号**，然后结合 =(等于)、!(不等)、\1(捕获匹配)

##### 4.4、Unicode属性转义

\p{...} 和 \P{...} 允许正则表达式匹配符合 Unicode 某种属性的所有字符

- 如：\p{Number}来匹配所有的Unicode数字（小写 p）

```js
const str = '㉛';
console.log(/\d/u.test(str));    // → false
console.log(/\p{Number}/u.test(str));     // → true
```

- 如：\p{Alphabetic}来匹配所有的Unicode单词字符（小写 p）

```js
const str = 'ض';
console.log(/\p{Alphabetic}/u.test(str)); // → true
// the \w shorthand cannot match ض
console.log(/\w/u.test(str));    // → false
```

- 同样有一个负向的 Unicode 属性转义模板 \P{...}（大写 P）

```js
console.log(/\P{Number}/u.test('㉛'));    // → false
console.log(/\P{Number}/u.test('ض'));     // → true
console.log(/\P{Alphabetic}/u.test('㉛'));   // → true
console.log(/\P{Alphabetic}/u.test('ض'));    // → false
```



### 四、ES10

#### 1、Array.prototype.flat()

> flat() 方法会按照一个**可指定的深度**递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回

```js
newArray = arr.flat(depth) // depth 是指定要提取嵌套数组的结构深度，默认值为 1
```

#### 2、Array.prototype.flatMap()

> flatMap() 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。它包含两部分功能一个是 map，一个是 flat（深度为1）

```js
let arr = [1, 2, 3]
console.log(arr.map(item => [item * 2]).flat()) // [2, 4, 6]
console.log(arr.flatMap(item => [item * 2])) 	// [2, 4, 6]
```

实际上 flatMap 是综合了 map 和 flat 的操作，所以**它也只能打平一层**

#### 3、Object.fromEntries()

Object.fromEntries 这个新的 API 实现了与 Object.entries 相反的操作

```js
const object = { x: 23, y:24 };
const entries = Object.entries(object); 	// [['x', 23], ['y', 24]]
const result = Object.fromEntries(entries); // { x: 23, y: 24 }
```

#### 4、String.trimStart 和 String.trimEnd

> 移除开头和结尾的空格

- trimStart() 方法从字符串的开头删除空格，trimLeft()是此方法的别名
- trimEnd() 方法从一个字符串的右端移除空白字符，trimRight 是 trimEnd 的别名

#### 5、try…catch

> catch 后的 err 可以省略

```js
try {
  console.log('Foobar')
} catch {
  console.error('Bar')
}
```

#### 6、Symbol.prototype.description

Symbol 的描述只被存储在内部的 [[Description]]，没有直接对外暴露，只有调用 Symbol 的 toString() 时才可以读取这个属性：

```js
Symbol('desc').description;  // "desc"
Symbol('').description;      // ""
Symbol().description;        // undefined
```

#### 7、Function.prototype.toString()

之前执行这个方法时，得到的字符串是去空白符号的。而现在，得到的字符串呈现出原本源码的样子：

```js
function sum(a, b) {
  return a + b;
}
console.log(sum.toString());
// function sum(a, b) {
//  return a + b;
// }
```

