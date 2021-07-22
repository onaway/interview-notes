### 1、块级作用域

好处：

- **不再需要立即执行的函数表达式(IIFE)**
- **循环体中的闭包不再有问题**
- **防止重复声明变量**

### 2、数组的扩展

#### 2.1、Array.from() 

> 将伪数组对象或可遍历对象转换为真数组

**如果一个对象的所有键名都是正整数或零，并且有length属性**，那么这个对象就很像数组，称为伪数组

#### 2.2、Array.of()

> 将一系列值转换成数组

```js
const arr1 = Array.of(1, 2);
console.log(arr1.length); 	// 2
console.log(arr1[0]); 		// 1
console.log(arr1[1]); 		// 2

const arr2 = Array.of(2);
console.log(arr2.length);   // 1
console.log(arr2[0]); 		// 2
```

#### 2.3、 find() 和 findIndex()

- find()：用于找出第一个符合条件的数组成员，如果没有符合条件的成员，则返回 undefined
- findIndex()：返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回 -1

#### 2.4、includes

- Array.prototype.includes()：返回一个布尔值，表示某个数组是否包含给定的值
- 第二个参数表示搜索的起始位置，默认为 0
- 如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度，则会重置为从 0 开始

#### 2.5、数组实例的 entries()，keys() 和 values()

可以用for...of循环进行遍历

- keys() 是对键名的遍历
- values() 是对键值的遍历
- entries() 是对键值对的遍历

```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let val of ['a', 'b'].values()) {
  console.log(val);
}
// 'a'
// 'b'

for (let [index, val] of ['a', 'b'].entries()) {
  console.log(index, val);
}
// 0 "a"
// 1 "b"
```

### 3、箭头函数

> 作用：缩减代码和改变 this 指向

使用注意点：

- 函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象
- 不可以当作构造函数，也就是说，不可以使用 new 命令，否则会抛出一个错误
- 不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替
- 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。