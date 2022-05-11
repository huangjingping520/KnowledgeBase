# Data Types

Seven primitive data types in JavaScript

1. **Number**: Floating poing numbers
2. **String**: Sequence of characters
3. **Boolean**: Logical type that can only be *true* or *false*
4. **Underfined**: Value taken by a variable that is not yet defined ('empty value')
5. **Null**: Also means 'empty value'
6. **Symbol(ES2015)**: Value that is unique and cannot be changed *(Not useful for now)*
7. **BigInt(ES2020)**: Larger integers than the Number type can hold

**JavaScript has dynamic typing:** We do **not** have to manually define the adta type of the value stored in a variable. Instead, data types are determined **automatically**.

**typeof**: We can use to show the type of the value.

```javascript
let isFun = true
console.log(typeof isFun)

// the answer is boolean
```

**Whenever** we declare an empty variavble, the value of the variable is undefined.

# let, const and var

## let

We us the let keyword to declare variable that can change later so basically during the execution of our program.

## const

We use the const keyword to declare variable that are not supposed to change at any point in the future.

**When use *const*, we need basically an initial value.**

## var

var is basically the old way of defining variables prior to ES6.

# Strings and Template Literals

before ES6

```javascript
const firstName = 'Merlin'
const job = 'programmer'
const birthYear = 2000
const year = 2022

const merlin = "I'm " firstName + ', a ' + (year - birthYear) + ' years old ' + job + '!'
```

and now we can use **template literals**

```javascript
const merlin = `I'm ${firstName}, a ${year - birthYear} years old ${job}!`
```

# Type Conversion and Coercion

**Type Conversion**

```javascript
Number('1998') // 1998
Number('merlin') // NaN
String(23) // '23'
```

**Type Coercion**

```javascript
'I am ' + 23 + ' years old!' // 23 from number to string
```

# Truthy and Falsy Values

**5 falsy value:** 0, '', undefined, null, NaN

# == and ===

 **=== is called the strict equality operator.**

It does not perform type coercion. And so it only returns true when both values are exactly the same.

**== is called the loose equality operator.**

It does type coercion.

```javascript
18 == 18			// true
18 === 18			// true
'18' == 18		// true
'18' === 18		// false
```

# Boolean Logic

**AND**: true when ALL are true

| AND   | TRUE  | FALSE |
| ----- | ----- | :---: |
| TRUE  | TRUE  | FALSE |
| FALSE | FALSE | FALSE |

**OR**: true when ONE is true

| OR    | TRUE | FALSE |
| ----- | ---- | ----- |
| TRUE  | TRUE | TRUE  |
| FALSE | TRUE | FALSE |

**NOT**: Inverts true/false value

# Statements and Expressions

An expression is a piece of code that produces a value.

The statement is like a bigger piece of code that is executed and which does not produce a value on itself.

# Function Declaration and Function Expression

```js
// Function Declaration
function calAge (birthYear) {
  return 2022 - birthYear
}

// Function Expression
const calAge = function (birthYear) {
  return 2022 - birthYear
}
```

We can call function declarations before they are defined in the code, but function expression does not work.

# Arrow Function

```js
const calAge = birthYear => 2022 - birthYear

const yearUntilRetirement = birthYear => {
  const age = 2022 - birthYear
  const retirement = 65 - age
  return retirement
}
```

# Array

```js
const friends = ['Jack', 'Bob', 'Peter']

const friends = new Array('Jack', 'Bob', 'Peter')
```

## Simple Methods

### push

**push** method adds elements to the end of an array.

```js
friends.push('Merlin') // ['Jack', 'Bob', 'Peter', 'Merlin']
```

### unshift

**unshift** method adds elements to the beginning of an array.

```js
friends.unshift('Merlin') // [ 'Merlin', 'Jack', 'Bob', 'Peter']
```

### pop

**pop** remove the last element of an array.

```js
friends.pop() // ['Jack', 'Bob']
```

### shift

**shift** remove the first element of an array.

```js
friend.shift() // ['Bob', 'Perter']
```

### indexOf

**indexOf** tells us in which position a certain element is in an array.

```js
friends.indexOf('Bob') // 1
```

### Includes

**includes** return true if the element is in the array or return false if the element is not in the array.

``` js
friends.includes('Bob') // true
friends.includes('Jhon') // false
```

### Slice

```js
let arr = ['a', 'b', 'c', 'd', 'e']
console.log(arr.slice(2, 4))
// ['c', 'd']
console.log(arr)
// ['a', 'b', 'c', 'd', 'e']
```

### Splice

```js
let arr = ['a', 'b', 'c', 'd', 'e']
console.log(arr.splice(2))
// ['c', 'd', 'e']
console.log(arr)
// ['a', 'b']
```

### Reverse

```js
let arr = ['a', 'b', 'c', 'd', 'e']
const arr2 = ['j', 'i', 'h', 'g', 'f']
console.log(arr2.reverse())
// ['f', 'g', 'h', 'i', 'j']
console.log(arr2)
// ['f', 'g', 'h', 'i', 'j']
```

### Concat

```js
const letters = arr.concat(arr2)
console.log(letters)
// ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
```

### Join

```js
console.log(letters.join(', '))
// a, b, c, d, e, f, g, h, i, j 
```

## The Spread Operator (...)

```js
const arr = [7, 8, 9]
const badNerArr = [1, 2, arr[0], arr[1], arr[2]] // [1, 2, 7, 8, 9]
const newArr = [1, 2, ...arr] // [1, 2, 7, 8, 9]
```

## Rest Pattern and Parameters

```js
const [a, b, ...others] = [1, 2, 3, 4, 5]
console.log(a, b, others) // 1 2 [3, 4, 5]
```

## Map

Map returns a new array containing the results of applying an operation on all original array elements.

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]
const eurToUsd = 1.1

const movementsUSD = movements.map(function (mov) {
  return mov * eurToUsd
})

// const movementsUSD = movements.map(mov => mov * eurToUsd)

console.log(movements)
// [200, 450, -400, 3000, -650, -130, 70, 1300]
console.log(movementsUSD)
// [220.00000000000003, 495.00000000000006, -440.00000000000006, 3300.0000000000005, -715.0000000000001, -143, 77, 1430.0000000000002]
```

## Filter

Filter returns a new array containing the array elements that passed a specified test condition.

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

const deposits = movements.filter(function (mov) {
  return mov > 0
})

console.log(movements)
// [200, 450, -400, 3000, -650, -130, 70, 1300]
console.log(deposits)
// [200, 450, 3000, 70, 1300]
```

## Reduce

Reduce boils all array elements down to one single value.

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

const balance = movements.reduce((acc, cur) => acc + cur, 0)
console.log(movements)
// [200, 450, -400, 3000, -650, -130, 70, 1300]
console.log(balance) // 3840
```

## Find

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

const firstWithdrawal = movements.find(mov => mov < 0)

console.log(movements)
// [200, 450, -400, 3000, -650, -130, 70, 1300]
console.log(firstWithdrawal) // -400
```

## FindIndex

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

const firstWithdrawal = movements.findIndex(mov => mov < 0)

console.log(movements)
// [200, 450, -400, 3000, -650, -130, 70, 1300]
console.log(firstWithdrawal) // 2
```

# Object

```js
const merlin = {
  firstName: 'Merlin',
  lastName: 'Alex',
  age: 22,
  job: 'programmer',
  friends: ['Jack', 'Bob', 'Peter']
}
```

## Dot and Bracket Notataion

```js
// dot notation
console.log(merlin.lastName) // Alex

// bracket notation
console.log(merlin['lastName']) // Alex
```

# Loop

## For 

for loop keeps running while condition is TRUE

```js
for (let i = 0; i < 10; i++) {
  console.log(i)
}
// 0 1 2 3 4 5 6 7 8 9
```

## Continue and Break

**continue** is to exit the current iteration of the loop and continue to the next one.

**break** is used to completely terminate the whole loop.

## While

```js
let i = 0
while (i < 10) {
  console.log(i)
  i++
}
// 0 1 2 3 4 5 6 7 8 9
```

## For-Of

```js
const menu = [
  'Focaccia',
  'Bruschetta',
  'Garlic Bread',
  'Caprese Salad',
  'Pizza',
  'Pasta',
  'Risotto'
]

for (const item of menu) {
  console.log(item)
}

// Focaccia Bruschetta     Garlic Bread Caprese Salad Pizza Pasta Risotto
```

## ForEach

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

movements.forEach(function (movement[, index[, array ]]) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`)
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`)
  }
})
/*
You deposited 200
You deposited 450
You withdrew 400
You deposited 3000
You withdrew 650
You withdrew 130
You deposited 70
You deposited 1300
*/
```

# The JavaScript Engine and Runtime

## JavaScript Engine

It is a program that executes JavaScript code. Like V8 engine powers Google Chrome.  

# Scope

## Global Scope

```js
const me = 'merlin'
const job = 'programmer'
```

1. Outside of any function or block.
2. Variables declared in global scope are accessible everywhere.

## Function Scope

```js
function calAge(birthYear) {
  const now = 2022
  const age = now - birthYear
  return age
}

console.log(now) // ReferenceError
```

1. Variable are accessible only inside function, not outside.
2. Also called local scope.

## Block Scope (ES6)

```js
if (year >= 1981 && year <= 1996) {
  const millenial = true
  const food = 'Avocado toast'
}

console.log(millenial) // ReferenceError
```

1. Variables are accessible only inside block.
2. This only applied to let and const variables.
3. Functions are also block scoped(only in strict mode).

# The this Keyword

Special varable that is created for every execution context(every function). Takes the value of (points to) the "owner" of the function in which **this** keyword is used.

1. Method => this = <Object that is calling the method>
2. Simple function call => this = undefined
3. Arrow functions => this = <this of surrounding function (lexical this) >
4. Event linstener => this = <DOM element that the handler is attached to >

this doed not point to the function itself, and also not the its variable environment.

`Object.assign()` is a Shallow Copy.

# Destructuring Arrays

```js
const arr = [2, 3, 4]

const [x, y, z] = arr 
console.log(x, y, z) // 2 3 4
```

# Destructuring Objects 

```js
const obj = {
  name: 'Merlin',
  job: 'programmer',
  age: 22
}

const {name, job, age} = obj
console.log(name, job, age) // Merlin programmer 22


let a = 111
let b = 999
const obj = { a: 23, b: 3, c: 12 }
// { a, b } = obj // Unexpected token '='
({ a, b } = obj)
console.log(a, b) // 23 3
```

# Set

A set is basically just a collection of unique values.

```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza'
])

console.log(orderSet) // Set(3) { 'Pasta', 'Pizza', 'Risotto' }

console.log(new Set('Merlin')) // Set(6) { 'M', 'e', 'r', 'l', 'i', 'n' }
```

## set.size

```js
console.log(orderSet.size) // 3
```

## set.has()

```js
console.log(orderSet.has('Pizza')) // true
console.log(orderSet.has('Bread')) // false
```

## set.add()

```js
orderSet.add('Bread')
console.log(orderSet) // Set(4) { 'Pasta', 'Pizza', 'Risotto', 'Bread' }
```

## set.delete()

```js
orderSet.delete('Pizza')
console.log(orderSet) // Set(3) { 'Pasta', 'Risotto', 'Bread' }
```

## set.clear()

```js
order.clear()
console.log(orderSet) // Set(0) {}
```

# Map

A map is a data structure that we can use to map values to keys.

```js
const rest = new Map()
```

## map.set()

```js
rest.set('name', 'Classico Italiano')
rest.set(1, 'Firenze, Italy')
rest.set(2, 'Lisbon, Portugal')
console.log(rest) 
/* 
Map(3) {
  'name' => 'Classico Italiano',
  1 => 'Firenze, Italy',
  2 => 'Lisbon, Portugal'
}
*/
```

## map.get()

```js
console.log(rest.get('name')) // Classico Italiano
console.log(rest.get(1)) // Firenze, Italy
```

 ## map.has()

like set.

## map.delete()

like set.

## map.size

like set.

## map.clear()

like set.

Convert object to map:

```js
const hoursMap = new Map(Object.entries(openingHours))
```

# Function

## Default Parameters

```js
const createBooking = function (flightNum, numPassengers = 1, price = 199) { // default value ES6
  // ES5
  numPassengers = numPassengers || 1
  price = prece || 199
  const booking = {
    flightNum,
    numPassengers,
    price
  }
}
```

## First-Class Functions

1. JavaScript treats functions as first-class citizens.
2. This means that functions are simply values.
3. Functions are just another "type" of object.

## High-Order Functions

1. A function that receives another function as an argument, that returns a new function, or both.
2. This is only possible because of first-class functions.

## Call and Apply Methods

### Call

Call method which will call the book function with the this keyword set to eurowings.

```js
const lufthansa = {
  airline: 'Lufthansa',
  iataCode: 'LH',
  bookings: [],
  // book: function () {}
  book(flightNum, name) {
    console.log(`${name} booked a seat on ${this.airline} flight ${this.iataCode}${flightNum}`)
    this.bookings.push({
      flight: `${this.iataCode}${flightNum}`,
      name
    })
  }
}

lufthansa.book(123, 'Merlin') // Merlin booked a seat on Lufthansa flight LH123

const eurowings = {
  airline: 'Eurowings',
  iataCode: 'EW',
  bookings: [],
}

const book = lufthansa.book
// Does not work
// book(123, 'Merlin')

book.call(eurowings, 123, 'Merlin') // Merlin booked a seat on Eurowings flight EW123
```

### Apply

Apply method is a similar method to the call method. And the apply method does basically exactly the same thing. The only difference is that apply does not receive a list of arguments after the this keyword.

```js
const flightData = [123, 'Merlin']
book.apply(eurowings, flightData) // Merlin booked a seat on Eurowings flight EW123
```

## Bind Method

Just like call method, bind also allows us to manually set this keywords for any function call. The difference is that bind doex not immediately call the function instead it returns a new function where this keyword is bound.

```js
const bookEW = book.bind(eurowings)
bookEW(234, 'Merlin') // Merlin booked a seat on Eurowings flight EW234
```

Also, we can do that below.

```js
const bookEW789 = book.bind(eurowings, 789)
bookEW789('Merlin') // Merlin booked a seat on Eurowings flight EW789
```

# Immediately Invoked Function Expressions(IIFE)

```js
(function () {
  console.log('This will never run again')
})()
```

# Closures

A function always has access to the variable environment of the execution context in which it was created, even after a debt execution context is gone. The closure is then basically this variable environment attached to the function, exactly as it was at the time and place that the function was created.

`A closure is the closed-over variavle environment of the execution context in which a function was created, even after that execution context is gone.`

`A closure gives a function access to all the variables of its parent function, even after that parent function has returned. The function keeps a reference to its outer scope, which preserves the scope chain throughout time.`

`A closure is like a backpack that a function carries around wherever it goes. This backpack has all the variables that were present in the environment where the function was created. `

```js
const secureBooking = function () {
  let passengerCount = 0

  return function () {
    passengerCount++
    console.log(`${passengerCount} passengers`)
  }
}

const booker = secureBooking()

booker() // 1 passengers
booker() // 2 passengers
booker() // 3 passengers
```

```js
let f
const g = function () {
  const a = 12
  f = function () {
    console.log(a * 2)
  }
}

g()
f()
// 24
```

```js
const boardPassengers = function (n, wait) {
  const perGroup = n / 3

  setTimeout(function () {
    console.log(`We are now boarding all ${n} passengers`)
    console.log(`There are 3 groups, each with ${perGroup} passengers`)
  }, wait * 1000)

  console.log(`Will start boarding in ${wait} seconds`)
}

boardPassengers(180, 3)

/*
Will start boarding in 3 seconds
// After 3 seconds
We are now boarding all 180 passengers
There are 3 groups, each with 60 passengers
*/
```

# Timer

```js
const ingredients = ['olives', 'spinach']

const pizzaTimer = setTimeout((a, b) => console.log(`Here is your pizza with ${a} and ${b} 🍕`), 3000, ...ingredients)

console.log('waitting... ')

if (ingredients.includes('spinach')) clearTimeout(pizzaTimer)
// waitting... 
```

# DOM

## What is the DOM?

DOM is basically the interface between all JavaScript code and the browser, or more specifically HTML documents that are rendered in and by the browser.

1. Allows us to make JavaScript interact with the browser.
2. We can write JavaScript to create, modify and delete HTML elements, set styles, classes and attributes, and listen and respond to events.
3. DOM tree is generated from an HTML document, which we can then interact with.
4. DOM is a very complex API that contains lots of metheds and properties to interact with the DOM tree.

![](https://s3.bmp.ovh/imgs/2022/05/03/6227ac4872294274.png)

# Defer、Async

![](https://s3.bmp.ovh/imgs/2022/05/03/ee951778cff1dce2.png)

![](https://s3.bmp.ovh/imgs/2022/05/03/7e58ba61a283bc15.png)

# OOP

1. Object-oriented programming is a programming paradigm based on the concept of objects.
2. We use objects to model (describe) real-world or abstract features.
3. Objects may contain data (properties) and code (methods). By using objects, we pack data and the corresponding behavior into on block.
4. In OOP, objects are self-contained pieces/blocks of code.
5. Objects are building blocks of applications, and interact with one another.
6. Interactions happen through a public interface (API): methods that the code outside of the object can access and use to communicate with the object.
7. OOP was developed with the goal of organizing code, to make it more flexible and easier to maintain (avoid "spaghetti code")

## Abstraction

Ignoring or hiding details that don't matter, allows us to get an overview perspective of the thing we're implementing, instead of messing with details that don't really matter to our implementation.

## Encapsulation

Keeping properties and methods private inside the class, so they are not accessible from outside the class. Some methods can be exposed as a public interface (API).

## Inheritance

Making all properties and methods of a certain class available to a child class, forming a hierarchical relationship between classes. This allows us to reuse common logic and model real-world relationships. 

## Polymorphism

A child class can overwrite a method it inherited from a parent class.

## Constructor Function

1. New {} is created.
2. function is called, this = {}
3. {} linked to prototype
4. function automatically return {}

```js
const Person = function (firstName, birthYear) {
  this.firstName = firstName
  this.birthYear = birthYear
}

const merlin = new Person('Merlin', 2000)
console.log(merlin)
// Person { firstName: 'Merlin', birthYear: 2000 }
```

## Prototype Chain

![](https://s2.loli.net/2022/05/03/iERv5yO28CWcVSr.png)

# Asynchronous JavaScript

> Most code is **synchronous**.
>
> Synchronous code is executed line by line.
>
> Each line of code waits for previous line to finish.
>
> Long-running operations block code execution.

![image-20220508221509179](https://i0.hdslb.com/bfs/album/daa6aab5ad9d5109611b5f36cb9504809ca712a3.png)

**Callback function alone is NOT makecode asynchronous**

## AJAX

![image-20220508222206323](https://i0.hdslb.com/bfs/album/8ce8947d5abd961a69e7de40e193b8829521ad51.png)

## API

![image-20220508222350934](https://i0.hdslb.com/bfs/album/6b904c61e582801a4697b878a16ef4a2f8486f8f.png)

There are be many types of APIs in web development:

1. DOM API
2. Geolocation API
3. Own Class API
4. "Online" API

![image-20220508222516776](https://i0.hdslb.com/bfs/album/58920d5de4513729879a8466a7300b2cba6c733d.png)

## XMLHttpRequest

```js
const request = new XMLHttpRequest()
request.open('GET', '[url]')
request.send()

request.addEventListener('load', function () {})
```

公共API统计：[Public-APIs](https://github.com/public-apis/public-apis)

## Requests and Responses

![image-20220509223144529](https://i0.hdslb.com/bfs/album/ebd36a2ead1db0bef8dd894ddc83bd85ed5e4dcf.png)

![image-20220509223307669](https://i0.hdslb.com/bfs/album/8b033c24e859fe2dc312619b6f2e42e005400898.png)

![image-20220509223407906](https://i0.hdslb.com/bfs/album/3d8f59496c8b47f64fcb831b18feacf1587bee80.png)

![image-20220509225442345](https://i0.hdslb.com/bfs/album/efa22aa63d0770ae1321b2282d5bed058580d4e7.png)

![image-20220509225306368](https://i0.hdslb.com/bfs/album/211c5a76d4bc1283107bf2ffb7ceae5c4a580bbe.png)

**Request:**

![image-20220509225140031](https://i0.hdslb.com/bfs/album/4c2c7b136ca9c7cf4e5afaf3c5544e3063ef2533.png)

**Response:**

![image-20220509225340065](https://i0.hdslb.com/bfs/album/e0b015e59c308feed6be1f2282710e98403431c6.png)

## Callback Hell

```js
setTimeout(() => {
  console.log('1 second passed~~')
  setTimeout(() => {
    console.log('2 seconds passed~~')
    setTimeout(() => {
      console.log('3 seconds passed~~')
      setTimeout(() => {
        console.log('4 seconds passed~~')
      }, 1000)
    }, 1000)
  }, 1000)
}, 1000)
```

## Promise and the fetch API

```js
const request = fetch('https://restcountries.com/v2/name/China')
console.log(request)
```

![image-20220510154013415](https://i0.hdslb.com/bfs/album/bf3d26c651369b4d85edb5858298d0a2bef5a976.png)

**Promise:** Acontainer for a future value.

```js
const getCountryData = function (country) {
  fetch(`https://restcountries.com/v2/name/${country}`)
    .then(res => res.json())
    .then(data => renderCountry(data))
}
```

