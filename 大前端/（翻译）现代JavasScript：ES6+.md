# 现代JavasScript：ES6+

ECMAScript 2015，也就是我们所知道的ES6，介绍了许多JavaScript的新特性。从那以后，每年都会增加一些新的特性。ES6及以后的扩展通常被称为现代JavaScript，因为有着这些重要的变化。这篇文章主要探索的是ES6, ES7, ES8, ES9以及ES10的新特性。

## 什么是ECMAScript

ECMAScript是一门脚本语言的标准。JavaScript是一门实现了ECMAScript标准的编程语言。ECMA国际是制定ES标准的协会。TC39是ECMA国际下的一个委员会，它决定JavaScript是如何工作的，以及应该有哪些新的特性。在2015年，JavaScript有了重大的变化，因为ES6发布了，这意味着许多新特性增加了进来。（在发布ES6之前的版本是2011年发布的ES5.1）。从2015年开始，TC39每年都会增加一些新的特性。因此，每次新的版本不会再出现大量的特性，以及发布时间上的巨大差距。


在英语中，ES是ECMAScript的简称。ES是一个标准，有点像一本专门讲规则的书。脚本语言遵守ES的标准，而JavaScript就是一种遵循这些ES标准的脚本语言。

## ES6 (2015)

#### 变量提升


用`var`关键字声明的变量会成为全局变量，或者成为函数的局部变量，但它没有块级作用域。使用`var`声明的变量可以被提升，重新赋值和重新声明。


`let`关键字允许变量有块级作用域。使用`let`声明的变量不会被提升，不能重新声明，但可以被重新赋值。

```javascript
// ES5:
var name = 'Lisa'
```

```javascript
// ES6: 
let name = 'Lisa'
name = 'Bart' // 'Bart'
let name = 'Maggie' // 'Maggie'
```

#### 常量声明

`const`关键字变量有块级作用域。用`const`声明的变量不能够被提升、重新声明，也不能重新赋值，但却是易变的。

```javascript
// ES6:
const name = 'Lisa'
name = 'Bart' // 类型错误，不能对常量进行再次赋值
const name = 'Maggie' // 语法错误，不能对常量进行再次声明
```

用`const`声明的变量是易变的。

```javascript
// ES6:
const simpson = { name: 'Lisa' }
simpson.name = 'Bart' // 改变name属性的值
simpson.address = '742 Evergreen Terrace' // 添加address属性
console.log(simpson) // { name: 'Bart', address: '742 Evergreen Terrace' }
simpson = { name: 'Bart' } // 类型错误，不能对常量进行重新赋值
```

#### 箭头函数


箭头函数表达式写起来比常规的函数表达式要简短。箭头函数不会绑定`this`，不应该将它作为方法，也不能将它作为构造器。

```javascript
// ES5:
function sum(a, b) {
  console.log(a + b)
}

const sum = function(a, b) {
  console.log(a + b)
}
```

```javascript
// ES6:
const sum = (a, b) => {
  console.log(a + b)
}
```

#### 模板字符串


模板字符串允许我们以更简洁的方式在字符串中嵌入表达式。模板字符串用反引号包起来。它们使用括号和美元符号表示占位符，就像这样`${variableName}`。

```javascript
let firstName = 'Lisa'
let lastName = 'Simpson'
```

```javascript
// ES5:
'Hello, ' + firstName + ' ' + lastName + '.'
// 'Hello, Lisa Simpson.'
```

```javascript
// ES6:
`Hello, ${firstName} ${lastName}.`
// 'Hello, Lisa Simpson.'
```

#### 解构赋值

解构赋值允许我们从数组中取出元素，或者从对象中取出元素，赋值给不同的变量。解构赋值在 [React](https://kentcdodds.com/blog/react-hooks-array-destructuring-fundamentals).中被重度使用。

数组解构：

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7]
```

```javascript
// ES5:
const one = numbers[0]
const two = numbers[1]

console.log(one) // 1
console.log(two) // 2
```

```javascript
// ES6:
const [one, two, three, ...rest] = numbers

console.log(one) // 1
console.log(two) // 2
console.log(rest) // [3, 4, 5, 6, 7]
```

对象解构：

```javascript
const lisa = {
  age: 8,
  school: 'Springfield Elementary',
}
```

ES5:

```javascript
const age = lisa.age
const school = lisa.school

console.log(age) // 8
console.log(school) // 'Springfield Elementary'
```

ES6:

```javascript
const { age, school } = lisa

console.log(age) // 8
console.log(school) // 'Springfield Elementary'
```

#### 展开语法


展开语法允许像被操作对象像数组表达式或者字符串一样展开迭代。

展开语法可以被用作展开一个数组：

ES6:

```javascript
const family = ['Lisa', 'Bart', 'Maggie', 'Marge', 'Homer']
const pets = ["Santa's Little Helper", 'Snowball']

const theSimpsons = [...family, ...pets]

console.log(theSimpsons)
// ['Lisa', 'Bart', 'Maggie', 'Marge', 'Homer', "Santa's Little Helper", 'Snowball']
```

展开语法可以用在函数参数上：

ES6:

```javascript
const array = [1, 2, 3]
const sumNumbers = (a, b, c) => a + b + c

console.log(sumNumbers(...array)) // 6
```

#### 数组迭代


`for...of`表达式创建了一个在可迭代对象（如数组、映射和集合）上的循环。

```javascript
const array = ['Lisa', 'Marge', 'Maggie']
```

```javascript
// ES5:
for (let i = 0; i < array.length; i++) {
  console.log(array[i]) // 'Lisa', 'Marge', 'Maggie'
}
```

```javascript
// ES6:
for (i of array) {
  console.log(i) // 'Lisa', 'Marge', 'Maggie'
}
```

#### Promises


Promise是表示异步操作最终完成（或失败）状态以及结果值的对象。

```javascript
// ES6:
function firstHello() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('First hello!')
      resolve()
    }, 5000)
  })
}

function secondHello() {
  console.log('Second hello!!')
}

console.log(firstHello().then(secondHello))
// Promise pending <-- promise pends for 5 seconds
// First hello!
// Second hello!!
```

## ES7 (2016)

#### Array.prototype.includes()

The `includes()` method returns `true` if an array includes a certain specified value, and returns `false` if it doesn't.

如果一个数组包含指定的值，则`includes()`方法返回`ture`，如果不包含则返回`false`。

```javascript
// ES7:
const simpsons = ['Lisa', 'Bart', 'Maggie', 'Marge', 'Homer']

simpsons.includes('Lisa') // returns true

simpsons.includes('Ned') // returns false
```

#### 指数操作符


`**`表达式返回将第一个操作数作为底数，第二个操作数作为幂的结果。


指数运算符是右联式的。比如，`2 ** 3 ** 3`等于`2 ** (3 ** 3)`

```javascript
// ES6:
Math.pow(2, 3) // 8
```

```javascript
// ES7:
2 ** 3 // 8

2 ** (3 ** 3) // 134217728
```

## ES 8 (2017)

#### Object.values()

`Object,values()`将一个对象作为一个参数，返回一个由对象的值的集合组成的数组。返回值的顺序跟`for...in`循环调用的顺序一样。

```javascript
// ES8:
const character = {
  name: 'Lisa',
  age: 8,
  school: 'Springfield Elementary',
}

console.log(Object.values(character))
// ['Lisa', 8, 'Springfield Elementary']
```

#### Object.entries()

`Object.entries()`将一个对象作为参数，返回值是一个由键-值对数组组成的二维数组。返回值的顺序就像`for...in`循环调用的顺序一样

```javascript
// ES8:
const character = {
  name: 'Lisa',
  age: 8,
  school: 'Springfield Elementary',
}

console.log(Object.entries(character))
// [[name: 'Lisa'], [age: 8], [school: 'Springfield Elementary']]
```

#### String.prototype.padEnd()

`padEnd()`的作用是用另一个字符串填充字符串的末尾，一直到符合字符串长度的要求。如果有必要的话，用于填充的字符串将会被重复多次。

```javascript
// ES8:
'The'.padEnd(10) // 'The       '
'The'.padEnd(10, ' Simpsons') // 'The Simpso'
'The'.padEnd(12, ' Simpsons') // 'The Simpsons'
'The'.padEnd(15, ' Simpsons') // 'The Simpsons Si'
```

#### String.prototype.padStart()

`padEnd()`的作用是用另一个字符串填充字符串的头部，一直到符合字符串长度的要求。如果有必要的话，用于填充的字符串将会被重复多次。

```javascript
// ES8:
'Simpsons'.padStart(10) // '  Simpsons'
'Simpsons'.padStart(10, 'The ') // 'ThSimpsons'
'Simpsons'.padStart(12, 'The ') // 'The Simpsons'
'Simpsons'.padStart(15, 'The ') // 'The TheSimpsons'
```

#### 末尾逗号

末尾逗号是指在最后一个元素末尾的逗号。当你需要增加新的一行而不需要改变之前最后一行的时候它是很有用的，因为它已经有一个逗号了。末尾的逗号也会让版本控制的差异更清晰。

```javascript
// ES8:
const character = {
  name: 'Lisa',
  age: 8,
  school: 'Springfield Elementary',
}
```

#### Async functions (async/await)

`Async/await`是promises的高级语法糖。它让异步代码更加阅读和编写。一个`async`函数知道它可能会期待一个`await`关键字来调用异步代码。

`async`函数也知道它应该返回一个`promise`而不是直接返回一个值。函数前面的`async`关键字会把一个普通函数变为一个异步函数。

`await`关键字只能在`async`函数内部使用。`await`关键字用来暂停一行`promise`代码的执行，直到这个`promise`变为`fufilled`（就绪）状态。

异步的代码看起来就像这样：

```javascript
async function hello() {
  return (greeting = await Promise.resolve('Hello'))
}
```

下面这个例子说明了`async/await`的能力：

```javascript
// ES8:
function delayedHello() {
  return new Promise(res => {
    setTimeout(() => res(console.log('A delayed hello!')), 5000)
  })
}

async function logHello() {
  await delayedHello()
}

console.log('Before logHello')
logHello()
console.log('After logHello')

// Before logHello
// After logHello
// A delayed hello! <-- logs after 5 seconds has passed
```

## ES9 (2018)

#### Promise.prototype.finally()
`finally()`方法都会被执行，无论`Promise`是`resolved`还是`rejected`的状态。

```javascript
// ES9:
const hello = () => {
  console.log('hello')
}

try {
  hello()
} catch (error) {
  console.log(error)
} finally {
  console.log('all done!')
}
// hello
// all done! <-- logs when promise is resolved

try {
  functionDoesNotExist()
} catch (error) {
  console.log(error)
} finally {
  console.log('all done!')
}
// ReferenceError: functionDoesNotExist is not defined
// all done <-- logs when promise is rejected
```

## ES10 (2019)

#### Array.flat()

`flat()`方法会创建一个新的数组，将子数组元素都将被加入进来。它有一个可选参数，`depth`，默认值是1。`depth`指定了嵌套数组应该被扁平化的深度。

```javascript
// ES10:
const array = [1, 2, 3, [4, 5]]
console.log(array.flat())
// [1, 2, 3, 4, 5]

const array2 = [1, 2, [3, [4, 5]]]

console.log(array2.flat())
// [1, 2, 3, [4, 5]]

console.log(array2.flat(2))
// [1, 2, 3, 4, 5]
```

#### Array.flatMap()

`flat.map()`方法使用map函数映射每个元素，然后将结果进行扁平化并放入一个数组中。这相当于向使用`map()`函数，再调用深度为1的`flat()`方法。

```javascript
// ES10 map() then flat():
const array = [1, 2, 3, 4, 5]

console.log(array.map(x => [x * 2]))
// [[2], [4], [6], [8], [10]]

console.log(array.map(x => [x * 2]).flat())
// [2, 4, 6, 8, 10]
```

```javascript
// ES10 flatMap():
const array = [1, 2, 3, 4, 5]

console.log(array.flatMap(x => [x * 2]))
// [2, 4, 6, 8, 10]
```

#### Object.fromEntries()

`Object.fromEntries()`方法是将一个`key-value`对的列表转为一个对象。

```javascript
// ES10:
const lisaArray = [
  ['grade', 2],
  ['school', 'Springfield Elementary'],
]

console.log(Object.fromEntries(lisaArray))
// {grade: 2, school: "Springfield Elementary"}

const lisaMap = new Map([
  ['grade', 2],
  ['school', 'Springfield Elementary'],
])

console.log(Object.fromEntries(lisaMap))
// {grade: 2, school: "Springfield Elementary"}
```

#### TrimStart()
`trimStart()`方法用于移除一个字符串头部的空格。

```javascript
// ES10:
const simpsons = '    The Simpsons    '

console.log(simpsons.trimStart())
// 'The Simpsons     '
```

#### TrimEnd()

`trimEnd()`方法用于移除一个字符串尾部的空格。

```javascript
// ES10:
const simpsons = '    The Simpsons    '

console.log(simpsons.trimEnd())
// '    The Simpsons'
```

#### 可选的catch参数

在`try...catch`中，错误参数现在是可选的。

```javascript
// ES10:
try {
  // do something
} catch (err) {
  // handle error
}
```

```javascript
// ES10:
try {
  // do something
} catch {
  // handle error
}
```

## 总结

这就是我们的收获！现在你知道了如何使用许多常用的ES6+的javascript新特性了。测试一下你的JavaScript知识吧[JavaScript questions by Lydia Hallie](https://github.com/lydiahallie/javascript-questions).