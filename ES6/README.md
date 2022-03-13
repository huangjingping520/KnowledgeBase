## ES6模块化

> ES6模块化规范是浏览器端和服务器端通用的模块化开发规范。

### 默认导出与默认导入

**默认导出：**

`export default 默认导出的成员`

在每个模块中只允许使用一次`export default`

**默认导入：**

`import 接收名称 from '模块标识符'`

### 按需导出与按需导入

**按需导出：**

`export 按需导出的成员`

可以多次按需导出

**按需导入：**

`export {s1} from '模块标识符'`

1. 按需导入的名称必须与按需导出的名称保持一致
2. 按需导入的时候可以使用`as关键字`进行重命名
3. 按需导入可以和默认导入一起使用

### 直接导入并执行模块中的代码

> 如果只想单纯的执行某个模块中的代码，并不需要得到向外共享的成员。此时，可以直接导入并执行模块代码。

```js
for (let i = 0; i < 3; i++>) {
  console.log(i)
}

// ---------------------

import '.js'
```

## Promise

### 回调地狱

> 多层回调函数的相互嵌套

- 代码耦合性太强，难以维护
- 大量冗余的代码相互嵌套，代码的可读性变差

### Promise的基本概念

Promise是一个构造函数。

Promise.prototype上包含一个.then()方法。

.then()方法用来预先制定成功和失败的回调函数。

```js
const p = new Promise()

p.then(result => {}, error => {})
```

成功的回调函数是必须的、失败的回调函数是可选的。

如果上一个.then()方法中饭回了一个新的Promise实例对象，则可以通过下一个.then()继续进行处理。通过.then()方法的链式调用，就解决了回调地狱的问题。

### 通过`.catch`捕获错误

在Promise的链式操作中如果发生了错误，可以使用Promise.prototype.catch方法捕获和处理。

### `Promise.all()`

`Promise.all()`会发起并行的Promise异步操作，等所有的异步操作全部结束后才会执行下一步的`.then`操作。

```js
import thenFs from 'then-fs'

const promiseArr = [
  thenFs.readFile('./files/1.txt', 'utf8'),
  thenFs.readFile('./files/2.txt', 'utf8'),
  thenFs.readFile('./files/3.txt', 'utf8')
]

Promise.all(promiseArr).then(result => {
  console.log(result)
})
```

### `Promise.race()`

`Promise.race()`方法会发起并行的Promise异步操作，只要任何一个异步操作完成，就立即执行下一步的`.then`操作。

```js
import thenFs from 'then-fs'

const promiseArr = [
  thenFs.readFile('./files/1.txt', 'utf8'),
  thenFs.readFile('./files/2.txt', 'utf8'),
  thenFs.readFile('./files/3.txt', 'utf8')
]

Promise.race(promiseArr).then(result => {
  console.log(result)
})
```

## async/await

> async/await 是 ES8 新引入的语法，用来简化Promise异步操作。

```js
import thenFs from 'then-fs'

async function getAllFile() {
  const r1 = await thenFs.readFile('./files/1.txt', 'utf8')
  console.log(r1)
  const r2 = await thenFs.readFile('./files/2.txt', 'utf8')
  console.log(r2)
  const r3 = await thenFs.readFile('./files/3.txt', 'utf8')
  console.log(r3)
}

getAllFile()
```

1. 如果function中使用了await，则function必须被async修饰
2. 在async方法中，第一个await之前的代码会同步执行，await之后的代码会异步执行。

## Eventloop

> JavaScript是一门单线程的编程语言。
> > 如果前一个任务非常耗时，则后续任务就不得不一直等待，从而造成程序假死。

### 同步任务（synchronous）

非耗时任务，指的是主线程上排队执行的那些任务。

只有前一个任务执行完毕，才能执行后一个任务。

### 异步任务（asynchronous）

耗时任务，异步任务由JavaScript委托给宿主环境进行执行。

当异步任务执行完成后，会通知JavaScript主线程执行异步任务的回调函数。

**宏任务：**

- 异步Ajax请求
- setTimeout、SetInterval
- 文件操作
- 其它宏任务

**微任务：**

- Promise.then、.catch和.finally
- process.nextTick
- 其它微任务

每一个宏任务执行完之后都会检查是否存在待执行的微任务，如果有则执行完所有的微任务之后，再继续执行下一个宏任务。

