### 一、JS 的类型

Javascript 有两种数据类型，分别是基本数据类型和引用数据类型

- 基本数据类型：Undefined、Null、Boolean、Number、String、Symbol 
- 引用数据类型：统称为Object对象，主要包括对象、数组和函数



### 二、基本数据类型

1. 值是不可变的
2. 存放在栈区
3. 值的比较（== / ===）



### 三、引用数据类型

1. 值是可变的
2. 同时保存在栈内存和堆内存（栈存指针，堆存对象）
3. 比较是引用的比较



### 四、检验数据类型

#### 1、typeof

> **typeof 返回一个表示数据类型的字符串**

```js
typeof Symbol();// symbol 有效
typeof ''; 		// string 有效
typeof 1; 		// number 有效
typeof true; 	// boolean 有效
typeof undefined; 		// undefined 有效
typeof new Function(); 	// function 有效
typeof null; 		// object 无效
typeof [] ; 		// object 无效
typeof new Date(); 	// object 无效
typeof new RegExp();// object 无效
```

#### 2、instanceof

> instanceof 是用来判断 A 是否为 B 的实例，表达式为：A instanceof B。**instanceof 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性**

```js
[] instanceof Array; 	// true
{} instanceof Object;	// true
new Date() instanceof Date;		// true
new RegExp() instanceof RegExp	// true
null instanceof Null	// Null is not defined
undefined instanceof Undefined	// Undefined is not defined
```

### 3、Object.prototype.toString.call()

> **Object.prototype.toString.call() 最准确最常用的方式**

说明：Object 上的 toString 它的作用是返回当前方法执行的主体（方法中的this）所属类的详细信息即"[object Object]"，其中第一个 object 代表当前实例是对象数据类型的(这个是固定死的)，**第二个 Object代表的是 *this* 所属的类是 Object**

```js
Object.prototype.toString.call('') ;   // [object String]
Object.prototype.toString.call(1) ;    // [object Number]
Object.prototype.toString.call(true) ; // [object Boolean]
Object.prototype.toString.call(undefined) ; // [object Undefined]
Object.prototype.toString.call(null) ; // [object Null]
Object.prototype.toString.call(new Function()) ;// [object Function]
Object.prototype.toString.call(new Date()) ; 	// [object Date]
Object.prototype.toString.call([]) ; // [object Array]
Object.prototype.toString.call(new RegExp()) ; 	// [object RegExp]
Object.prototype.toString.call(new Error()) ; 	// [object Error]
Object.prototype.toString.call(document) ; 	// [object HTMLDocument]
Object.prototype.toString.call(window) ; 	// [object global] window 是全局对象 global 的引用
```



