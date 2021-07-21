### 1、其他的数据类型转换为 String

#### 1.1、toString() 方法

- 调用被转换数据类型的 `toString()` 方法,该方法不会影响到原变量，它会将转换的结果返回，**但是注意：null 和 undefined 这两个值没有 toString，如果调用他们的方法，会报错**
- 采用 Number 类型的 `toString()` 方法的基模式，可以用不同的基输出数字，例如二进制的基是 2，八进制的基是 8，十六进制的基是 16

```js
var iNum = 10;
alert(iNum.toString(2));        // 输出 "1010"
alert(iNum.toString(8));        // 输出 "12"
alert(iNum.toString(16));       // 输出 "A"
```

#### 1.2、String() 函数

- 使用 `String()` 函数做强制类型转换时，对于 Number 和 Boolean 实际上就是调用的 `toString()` 方法,
  但是对于 null 和 undefined，就不会调用 toString() 方法，它会将 null 直接转换为 "null" ，将 undefined 直接转换为 "undefined"

```js
String(null)		// "null"
String(undefined)	// "undefined"
```

- String 方法的参数如果是对象，返回一个类型字符串；如果是数组，返回该数组的字符串形式。

```js
String({a: 1})    // "[object Object]"
String([1, 2, 3]) // "1,2,3"
```

### 2、其他的数据类型转换为 Number

#### 2.1、使用 Number() 函数

##### 2.1.1、字符串转数字

- 如果是纯数字的字符串，则直接将其转换为数字
- 如果字符串中有非数字的内容，则转换为 NaN
- 如果字符串是一个空串或者是一个全是空格的字符串，则转换为 0

```js
Number('324') 	// 324
Number('324ab') // NaN
Number('') 		// 0
```

##### 2.1.2、布尔值转数字：true 转成 1，false 转成 0

```js
Number(true)  // 1
Number(false) // 0
```

##### 2.1.3、undefined 转数字：转成 NaN

```js
Number(undefined) // NaN
```

##### 2.1.4、null 转数字：转成 0

```js
Number(null) // 0
```

##### 2.1.5、Number() 接受数值作为参数

- 能识别负的十六进制
- 能识别 0 开头的八进制
- 返回值永远是十进制值

```js
Number(3.15);    // 3.15
Number(023);     // 19
Number(0x12);    // 18
Number(-0x12);   // -18
```

##### 2.1.6、Number() 参数是对象

- 将返回 NaN，除非是包含单个数值的数组

```js
Number({a: 1}) 		// NaN
Number([1, 2, 3]) 	// NaN
Number([5]) 		// 5
```

#### 2.2、parseInt() & parseFloat()

这种方式专门用来对付字符串。

- `parseInt()` 将一个字符串转换为一个整数

```js
console.log(parseInt('.21'));	// NaN
console.log(parseInt("10.3"));	// 10
console.log(parseInt("1abc2"))	// 1
console.log(parseInt("ab5c"))	// NaN
```

- `parseFloat()` 将一个字符串转换为一个浮点数

```js
console.log(parseFloat('.21'));       // 0.21
console.log(parseFloat('.d1'));       // NaN
console.log(parseFloat("10.11.33"));  // 10.11
console.log(parseFloat("4.3years"));  // 4.3
console.log(parseFloat("He40.3"));    // NaN
```

### 3、其他的数据类型转换为 Boolean

- 只有空字符串("")、null、undefined、+0、-0 和 NaN 转为布尔型是 false
- 其他的都是 true
- 空数组、空对象转换为布尔类型也是 true
- 甚至连 false 对应的布尔对象 new Boolean(false) 也是 true

