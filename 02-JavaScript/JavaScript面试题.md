### JS中的继承 ❌

#### 原型链继承

#### `extends` 继承

#### 



## 「var 和 let 、const 的区别」⭐️

- var是ES5语法，var有变量提升。let const是ES6语法。
- var 和 let是变量，可修改；const是常量,不可修改。
- let 、 const有块级作用域；var没有。

代码演示：

```js
console.log(a) //undefined
var a = 200

相当于
var a 
console.log(a) // undefined
a = 200
```

> 额外关注一下：函数表达式 和 函数声明。



## 「typeof 返回哪些类型」

- string
- number
- boolean
- symbol（ES6）
- object（ 注意：typeof **null**  === **object** ）
- function
- undefined



## 「列举强制类型转换和隐式类型转换」

- 强制: `parseInt` 、`parseFloat` 、 `toString` 等
- 隐式: `if`、`逻辑运算`、`==`、`+拼接字符串`



## 「`split( )` 和 `join( )`的区别」



```js
[1,2,3].join('-') //'1-2-3'
'1-2-3'.split('-') //[1,2,3]
```



## 「数组的`pop` , `push` , `unshift` , `shift`做什么」

> 回答的角度：
>
> 1. 功能是什么?
> 2. 返回值是什么?
> 3. 是否会对原数组造成影响？



代码演示：

```js
const arr = [10, 20, 30, 40]

// pop
const popRes = arr.pop()
console.log(popRes, arr) //40 [10, 20, 30] 返回的是删除的最后一个元素，会改变原数组

// push
const pushRes = arr.push(50)  //在数组最后追加 50
console.log(pushRes, arr) //4 [10, 20, 30 ,50] 返回 length 会改变原数组

// unshift
const unshiftRes = arr.unshift(5) //在数组最前追加 5 
console.log(unshiftRes, arr) //5 [5, 10, 20, 30 ,50]  返回 length 会改变原数组

// shift
const shiftRes = arr.shift() //删除第一个元素 
console.log(shiftRes, arr) //5 [10, 20, 30, 50] 返回的是删除的第一个元素，会改变原数组
```



> 拓展：数组的API，有哪些是纯函数？
>
> 纯函数的概念：
>
> 1. 不改变原数组
> 2. 返回一个数组
>
> 纯函数：`concat` ，`map`  ， `filter` ，`slice`
>
> 非纯函数：`push`，`pop`，`shift`，`unshift`，`forEach`，`someevery`，`reduce`

代码演示：

```js
const arr = [10, 20, 30, 40]

// concat
const arr1 = arr.concat([50, 60, 70])
console.log(arr, arr1) //[10, 20, 30, 40]  [10, 20, 30, 40, 50, 60, 70]

// map
const arr2 = arr.map(num => num * 10)
console.log(arr, arr2) //[10, 20, 30, 40]  [100, 200, 300, 400]

// filter
const arr3 = arr.filter(num => num > 25)
console.log(arr, arr3) //[10, 20, 30, 40]  [30, 40]

// slice 没有参数 在这里是复制了一份数组,类似于拷贝。
const arr4 = arr.slice()
console.log(arr, arr4) //[10, 20, 30, 40] [10, 20, 30, 40]
```



## 「数组slice和splice的区别」

> 回答角度：
>
> - 功能区别( `slice`-切片, `splice`-剪接)
> - 参数和返回值
> - 是否纯函数?



代码演示：

```js
const arr = [10, 20, 30, 40, 50]

// slice 纯函数 原数组不变
const arr1 = arr.slice() //复制 [10, 20, 30, 40, 50]
const arr2 = arr.slice(1, 4) //按照范围截取 取得到左边取不到右边 [20, 30, 40]
const arr3 = arr.slice(2) //截取索引之后的 [30, 40, 50]
const arr4 = arr.slice(-3) //反向截取倒数第三个【没有倒数第0个 】 [30, 40, 50]

// splice 非纯函数 会改变原数组
const spliceRes = arr.splice(1, 2, 'a', 'b', 'c')
//这里简单举个例子，重点是它改变了原数组
//从索引1开始截取，截取2个元素,并使用 'a', 'b', 'c'替换了之前的截取的空位
console.log(spliceRes, arr) //[20, 30]  [10, 'a', 'b', 'c', 40, 50]
```



## 「[10, 20, 30].map(parseInt)返回结果是什么?」

> 回答角度：
>
> - `map`的参数和返回值
> - `parseInt`参数和返回值



代码演示：

```js
const res = [10,20,30].map(parseInt)
console.log(res) //[10, NaN, NaN]

//拆解
[10,20,30].map((item,index)=>{
    return parseInt(item,index)
})
//parseInt 第二个参数可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。
```



> 注意 `parseInt`的用法
>
> 



## 「ajax请求get和post的区别?」

- `get`一般用于查询操作, `post`一般用户提交操作
- `get`参数拼接在url上, `post`放在请求体内(数据体积可更大)
- 安全性: `post`易于防止`CSRF`



## 「函数bind,call和apply的区别」











## 「事件代理(委托)是什么?」







## 「闭包是什么,有什么特性?有什么负面影响？」⭐️

- 影响:变量会常驻内存，得不到释放。闭包不要乱用

> 结合：第六章 和 18-5



## 「如何阻止事件冒泡和默认行为?」

- `event.stopPropagation()`
- `event.preventDefault()`



## 「查找、添加、删除、移动DOM节点的方法?」

> 第九章



## 「如何减少DOM操作?」

- 缓存`DOM`查询结果
- 多次`DOM`操作,合并到一-次插入



## 「解释jsonp的原理,为何它不是真正的ajax ?」❌

- 浏览器的同源策略（服务端没有同源策略）和跨域。
- 哪些html标签能绕过跨域？
- jsonp原理？



## 「document load和ready的区别」

- `ready`，表示文档结构已经加载完成（不包含图片等非文字媒体文件）
- `onload`，指示页面包含图片等文件在内的所有元素都加载完成



代码演示：

```js
window.addEventListener('load',function(){
  //页面的全部资源加载完成才会执行，包括图片、视频等
})

document.addEventListener('DOMContentLoaded',function(){
  //DOM渲染完即可执行，此时图片、视频还可能没有加载完
})
```



## 「`==`和`===`的不同」❌

- `==` ：判断值相等，会自动转换数据类型
- `===` ：不会自动转换数据类型；全等十判断数据类型和值。
- 哪些场能用 `==` ?



## 「函数声明和函数表达式的区别」

- 函数声明`function fn() {...}`
- 函数表达式`const fn = function() {..}`
- 函数声明会在代码执行前预加载（类似于变量提升），而函数表达式不会



代码演示1：

```js
函数声明
const res = sum(10, 20)
console.log(res) //30
function sum(x, y) {
    return x + y
}

相当于：
function sum(x, y) {
    return x + y
}
const res = sum(10, 20)
console.log(res)
```



代码演示2:

```js
函数表达式
var res = sum(10, 20)
console.log(res)  //sum is not a function
var sum = function (x, y) {
    return x + y
}

const res = sum(10, 20)
console.log(res)  //Cannot access 'sum' before initialization
const sum = function (x, y) {
    return x + y
}
```



## 「`new Object()` 和 `Object.create()` 的区别」⭐️

- `{}` 等同于`new Object()`， 原型都是Object.prototype
- `Object.create(nul)`没有原型
- `Object.create({..})` 可指定原型



代码演示：

```js
const obj1 = {
    a: 10,
    b: 20,
    sum() {
        return this.a + this.b
    }
}

const obj2 = new Object({
    a: 10,
    b: 20,
    sum() {
        return this.a + this.b
    }
})

/**
 * 知识点一
 * 1: obj1 = {a: 10, b: 20, sum: ƒ}
 * 2: obj2 = {a: 10, b: 20, sum: ƒ}
 * 3: obj1 === obj2 为false。两者内存地址不同
*/
console.log(obj1 === obj2) //false

/**
 * 知识点二：
 * 1: obj3 = {a: 10, b: 20, sum: ƒ}
 * 2: obj3 === obj1 为true
 */
const obj3 = new Object(obj1)
console.log(obj3 === obj1); //true

/**
 * 知识点三：
 * 1: obj4 = {} 并且 No properties
 * 2: obj5 = {} 并且 [[Prototype]]: Object
*/
const obj4 = Object.create(null)
const obj5 = new Object()

/**
 * 知识点四：
 * 1: obj6 = {} 且 原型为  {a: 10, b: 20, sum: ƒ}
 * 2: obj7 = {} 且 原型为  obj1 = {a: 10, b: 20, sum: ƒ}
 * 3: obj6.a = 10
 */
const obj6 = Object.create({
    a: 10,
    b: 20,
    sum() {
        return this.a + this.b
    }
})
const obj7 = Object.create(obj1)
```



## 「关于 this 的场景题」

> this 是在执行的时候确定的

代码演示：

```js
const User = {
    count : 1,
    getCount: function() {
        return this.count
    }
}
console.log(User.getCount()) //what?
const func = User.getCount
console.log( func() ) //what?
```

答案：

- 第一个打印的是 `1`
- 第二个打印的是 `undefined` 因为这个时候 `this` 指向是`window`



## 「关于作用域和自由变量的场景题」❌







## 「手写字符串trim方法,保证浏览器兼容性」

> - replace支持正则
> - 原型, this, 正则表达式 把空白变为空字符串。

代码演示：

```js
String.prototype.trim = function(){
    return this.replace(/^\s+/,'').replace(/\s+$/,'')
}
```



## 「如何获取多个数字中的最大值」

```js
function max() {
    const nums = Array.prototype.slice.call(arguments)//把参数变为数组
    let max = 0
    nums.forEach(item => {
        if(item > max) {
            max = item
        }
    })
    return max
}
//使用
console.log(max(1,2,3,4,5)) //5
```



## 「如何捕获JS程序中的异常？」

1: 通过 `try...catch...` 捕获

代码演示：

```js
try {
  //to do
}catch (ex) {
  console.log("error", ex.message); // 手动捕获 catch
}finally{
  //to do
}
```



2: `window.onerror` 自动捕获【不推荐】

- 第一，对跨域的js,如CDN的，不会有详细的报错信息。
- 第二，对于压缩的js,还要配合 sourceMap 反查到未压缩代码的行、列。

代码演示:

```js
window.onerror = function(message, source, lineNum, colNom, error) { 
	....
}
```



3: `window.addEventListener('error')` 

代码演示：

```js
window.addEventListener('error', function(event) { 
	....
})
```



## 「什么是JSON ?」

- `json`是一种数据格式，本质是一-段字符串
- `json`格式和`JS`对象结构一致，对`JS`语言更友好
- window.JSON是一个全局对象：JSON.stringify、JSON.parse



## 「获取当前页面url参数」❌



## 「将`url`参数解析为`JS`对象」❌



# for..in 和 for..of的区别 ✅

## key 和 value

for...in 遍历 key ；  for...of 遍历 value

```js
// 数组
const arr = [10, 20, 30]
for (let n of arr) {
  console.log(n)；  // 10 , 20 , 30
}

for (let key in arr) {
  console.log(key); // 0 ，1 ，2
}

// 字符串
const str = 'abc'
for (let s of str) {
  console.log(s); // a, b, c
}
for (let key in str) {
  console.log(key); // 0 , 1 , 2
}

// 函数
function fn1() {
  for (let argument in arguments) {
    console.log(argument) // for...of 可以获取 value ，而 for...in 获取 key
  }
}
fn1(10, 20, 30); //0, 1, 2

function fn2() {
  for (let argument of arguments) {
    console.log(argument) // for...of 可以获取 value ，而 for...in 获取 key
  }
}
fn2(10, 20, 30); //10, 20, 30


// DOM对象
const pList111 = document.querySelectorAll('p')
for (let p of pList111) {
  console.log(p) // for...of 可以获取 value（这里是DOM元素） ，而 for...in 获取 key。
}

const pList222 = document.querySelectorAll('p')
for (let p in pList222) {
  console.log(p) // for...of 可以获取 value ，而 for...in 获取 key（这里是pList222里面的健名）
}
```



## 遍历对象

for...in 可以遍历对象；for...of 不可以

```js
const obj = {
  name: "双越",
  city: "北京",
};
for (let val of obj) {
  console.log(val); // 报错 Uncaught TypeError: obj is not iterable
}

for (let val in obj) {
  console.log(val); // name , city
}
```



## 遍历 Map/Set

for...in 不可以遍历；for...of 可以遍历 Map/Set 

```js
const set1 = new Set([10, 20, 30])
for (let n of set1) {
  console.log(n); // 10 , 20 , 30。  注意：for...in...是无反应且无报错。
}

let map1 = new Map([
  ['x', 10], ['y', 20], ['z', 3]
])
for (let n of map1) {
  console.log(n) // ['x', 10], ['y', 20], ['z', 3]
}
```



## 遍历 generator

for...in 不可以遍历；for...of 可遍历 generator 

```js
function* foo(){
  yield 10
  yield 20
  yield 30
}
for (let o of foo()) {
  console.log(o)
}
```



## for...in 和 for..of 遍历的本质

### 对象的可枚举属性

> 本质：**for...in 遍历一个对象的可枚举属性。**

使用 `Object.getOwnPropertyDescriptors(需要鉴定的对象)` 可以获取对象的所有属性描述，看里面的 ` enumerable: true` 来判断该属性是否可枚举。

对象，数组，字符串

```js
const obj1 = { x:100 }
Object.getOwnPropertyDescriptors(obj1) //里面含有 enumerable: true
```



### 可迭代对象

> 本质：**for...of 遍历一个可迭代对象。**

其实就是迭代器模式，通过一个 `next` 方法返回下一个元素。

该对象要实现一个 `[Symbol.iterator]` 方法，其中返回一个 `next` 函数，用于返回下一个 value（不是 key）。可以执行 `arr[Symbol.iterator]()` 看一下。

JS 中内置迭代器的类型有 `String`， `Array` ，`arguments`， `NodeList` ，`Map` ，`Set`， `generator` 等。

```js
const map = new Map
map[Symbol.iterator]() //MapIterator对象里面返回一个 next函数。

const arr = [1,2,3,4,5]
arr[Symbol.iterator]() //Array Iterator对象里面返回一个 next函数。
```



## 总结

- for...in 遍历一个对象的**可枚举属性**，如对象、数组、字符串。针对属性，所以获得 key
- for...of 遍历一个**可迭代对象**，如数组、字符串、Map/Set 。针对一个迭代对象，所以获得 value



## 划重点

“枚举” “迭代” 都是计算机语言的一些基础术语，目前搞不懂也没关系。但请一定记住 for...of 和 for...in 的不同表现。



## 连环问：for await...of

用于遍历异步请求的可迭代对象。

```js
// 像定义一个创建 promise 的函数
function createTimeoutPromise(val) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(val)
        }, 1000)
    })
}
```

如果你明确知道有几个 promise 对象，那直接处理即可

```js
(async function () {
    const p1 = createTimeoutPromise(10)
    const p2 = createTimeoutPromise(20)

    const v1 = await p1
    console.log(v1)
    const v2 = await p2
    console.log(v2)
})()
```

如果你有一个对象，里面有 N 个 promise 对象，你可以这样处理

```js
(async function () {
    const list = [
        createTimeoutPromise(10),
        createTimeoutPromise(20)
    ]

    // 方法一，使用 Promise.all 执行
    Promise.all(list).then(res => console.log(res))

    // 方法二，使用 for await ... of 遍历执行
    for await (let p of list) {
        console.log(p)
    }

    // 注意，如果用 for...of... 只能遍历出各个 promise 对象，而不能触发 await 执行
})()
```

【注意】如果你想顺序执行，只能延迟创建 promise 对象，而不能及早创建。

即，你创建了 promise 对象，它就立刻开始执行逻辑。

```js
方法一：
(async function () {
    const v1 = await createTimeoutPromise(100)
    console.log(v1)
    const v2 = await createTimeoutPromise(200)
    console.log(v2)
})()

方法二：
(async function () {
    for (let n of [100, 200]) {
        const v = await createTimeoutPromise(n)
        console.log('v', v)
    }
})()
```



## 连环问：如何退出 for...in 和 for..of 的循环？

- 如何退出`for..in..`和`for..of..`循环？
  - 一般的for循环，可以用return、break
  - foreach、map，只能用抛出错误的形式，退出。

------



# JS 严格模式和非严格模式 ✅

## 设计初衷

Javascript 设计之初，有很多不合理、不严谨、不安全之处，例如变量未定义即可使用 `n = 100`。严格模式用于规避这些问题。而现在 ES 规范已经普及，从语法上已经规避了这些问题。



## 开启严格模式

代码（或一个函数）一开始插入一行 `'use strict'` 即可开启严格模式

```js
// 全局开启严格模式
'use strict' // 全局开启

// 函数开启严格模式
function fn() {
  'use strict' // 某个函数开启
}
```

一般情况下，开发环境用 ES 或者 Typescript ，打包出的 js 代码使用严格模式



## 严格模式的不同

严格模式的细则有很多，这里总结一些常用常见的



### 全局变量必须声明

```js
'use strict'
n = 10 // ReferenceError: n is not defined
```



### 禁止使用 `with`

```js
'use strict'
var obj = { x: 10 }
with (obj) {
  // Uncaught SyntaxError: Strict mode code may not include a with statement
  console.log(x)
}
```



### 创建 eval 作用域

⚠️非常不推荐使用！

正常模式下，JS 只有两种变量作用域：全局作用域 + 函数作用域。严格模式下，JS 增加了 eval 作用域。

**chrome 隐私模式下执行这段代码？？？**

```js
'use strict'
var x = 10
eval('var x = 20; console.log(x)')
console.log(x)
```



### 禁止 this 指向全局作用域

```js
'use strict'
function fn() {
  console.log('this', this) // undefined
}
fn()
```



### 函数参数不能重名

```js
'use strict'

// Uncaught SyntaxError: Duplicate parameter name not allowed in this context
function fn(x, x, y) {
  return
}
```



## 总结

- 全局变量必须声明
- 禁止使用 with
- 创建 eval 作用域
- 禁止 this 指向全局作用域
- 函数参数不能重名

------



















