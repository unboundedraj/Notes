---
title: Javascript
date: 2026-11-01
tags: [js, javascript]
---

# Introduction

JavaScript is a versatile, dynamically typed programming language that brings life to web pages by making them interactive. It is used for building interactive web applications and supports both client-side and server-side development.

- **Dynamically typed:** Variable types are determined at runtime.
- **Single-threaded:** Executes one task at a time (but supports asynchronous operations).
- **Compiled and interpreted:** Modern JavaScript engines combine compilation and interpretation for better performance
- **Client Side:** On the client side, JavaScript works along with HTML and CSS. HTML adds structure to a web page, CSS styles it, and JavaScript brings it to life by allowing users to interact with elements on the page, such as actions on clicking buttons, filling out forms, and showing animations. JavaScript on the client side is directly executed in the user's browser.
- **Server Side**: On the Server side (on Web Servers), JavaScript is used to access databases, file handling, and security features to send responses, to browsers.
- Supports powerful frameworks and libraries like **React, Angular, Vue.js, Node.js**, and **Express.js**, widely used in modern web applications.

```javascript
console.log("Hello World!");
```

Run it in your terminal with:

```
node index.js
```

## **Features of JavaScript**

Here are some key features of JavaScript that make it a powerful language for web development:

**Client-Side Scripting:** JavaScript runs on the user's [**browser,**](https://www.geeksforgeeks.org/computer-networks/web-browser/) so it has a faster response time without needing to communicate with the [**server**](https://www.geeksforgeeks.org/system-design/client-server-model/) .  
**Versatile:** Can be used for a wide range of tasks, from simple calculations to complex server-side applications.  
**Event-Driven:** Responds to user actions (clicks, keystrokes) in real-time.  
**Asynchronous:** It can handle tasks like fetching data from [**servers**](https://www.geeksforgeeks.org/computer-networks/what-is-server/) without freezing the user interface.  
**Rich Ecosystem:** There are numerous libraries and frameworks built on JavaScript, such as [**React**](https://www.geeksforgeeks.org/reactjs/react/) , [**Angular**](https://www.geeksforgeeks.org/angular-js/angular-tutorial/) , and [**Vue.js**](https://www.geeksforgeeks.org/javascript/vue-js/), which make development faster and more efficient.

# JavaScript Question Bank

## What are the different data types in JavaScript? Explain primitive vs non-primitive types.

JavaScript has 7 primitive data types: String, Number, Boolean, Undefined, Null, Symbol, and BigInt. Primitive values are immutable and are assigned/copied by value.

Non-primitive types include Objects, Arrays, and Functions. They are mutable and variables hold references to these objects.

```javascript
// Primitive
let a = 10;
let b = a;
b = 20;

console.log(a); // 10

// Non-primitive
let obj1 = { name: "John" };
let obj2 = obj1;

obj2.name = "Mike";

console.log(obj1.name); // Mike
```

## What is the difference between var, let, and const?

All three are used to declare variables, but differ in scope, hoisting, and reassignment behaviour.


| Feature                 | var      | let         | const       |
| ----------------------- | -------- | ----------- | ----------- |
| Scope                   | Function | Block       | Block       |
| Redeclaration           | Allowed  | Not allowed | Not allowed |
| Reassignment            | Allowed  | Allowed     | Not allowed |
| Hoisting                | Yes      | Yes         | Yes         |
| TDZ(Temporal Dead Zone) | No       | Yes         | Yes         |


```javascript
var a = 10;
var a = 20; // Allowed

let b = 10;
b = 20; // Allowed

const c = 10;
// c = 20; // Error
```

## What is type coercion in JavaScript? Explain implicit and explicit coercion.

Type coercion is the process of converting one data type into another. It can happen automatically (implicit) or manually (explicit).

- Implicit coercion: JavaScript automatically converts types during operations.
- Explicit coercion: Developers manually convert types using methods such as `Number()`, `String()`, and `Boolean()`.

```
// Implicit coercion
console.log("5" + 2); // "52"
console.log("5" - 2); // 3

// Explicit coercion
console.log(Number("10")); // 10
console.log(String(100)); // "100"
console.log(Boolean(1)); // true
```

## What is the difference between == and ===?

`==` is the loose equality operator. It compares values after performing type coercion when necessary.

`===` is the strict equality operator. It compares both value and type without performing type coercion.

```
console.log(5 == "5");  // true
console.log(5 === "5"); // false

console.log(null == undefined);  // true
console.log(null === undefined); // false
```

## What is the difference between null and undefined?

`undefined` means a variable has been declared but has not been assigned a value, whereas `null` represents the intentional absence of a value.

```javascript
let a;
console.log(a); // undefined

let b = null;
console.log(b); // null

console.log(typeof a); // undefined
console.log(typeof b); // object
```

## What is the difference between NaN and undefined? How do you check for NaN?

`undefined` represents a missing or uninitialized value, whereas `NaN` (Not-a-Number) represents an invalid numeric result.

```javascript
let a;
let b = "hello" * 2;

console.log(a); // undefined
console.log(b); // NaN

console.log(Number.isNaN(b)); // true
console.log(Number.isNaN(a)); // false
```

## What is the difference between pass by value and pass by reference in JavaScript?

JavaScript always passes arguments **by value**. For objects, the value being passed is a reference to the object. This means both variables can access and modify the same object, but reassigning the parameter does not reassign the original variable.

```javascript
// Primitive
function changeValue(x) {
    x = 20;
}

let a = 10;
changeValue(a);
console.log(a); // 10

// Object
function changeObject(obj) {
    obj.name = "Mike";
}

let user = { name: "John" };
changeObject(user);

console.log(user.name); // Mike
```

## What is hoisting in JavaScript? How does it work with var, let, and const?

Hoisting is **JavaScript's behaviour of processing declarations before executing code**. However, different declarations behave differently.

- `var`: Hoisted and initialized with `undefined`.
- `let` and `const`: Hoisted but remain in the Temporal Dead Zone until declaration execution.
- **Function declarations: Fully hoisted, so they can be called before their declaration.**

```javascript
var globalVar = 10;

function test() {
    var functionVar = 20;

    if (true) {
        let blockVar = 30;
        console.log(blockVar); // 30
    }

    console.log(functionVar); // 20
    // console.log(blockVar); // ReferenceError
}
```

> Unlike `var` variables—which are "hoisted" to the top of their scope and initialized with `undefined`—variables declared with `let` and `const` are also hoisted, but **they are not initialized**. The code execution cannot touch the variable until the parser reaches the actual line of code where the variable is declared and assigned a value. The region between the start of the scope and that line is the Temporal Dead Zone.

## What is an execution context in JavaScript?

An execution context is the environment in which JavaScript code is evaluated and executed. It maintains information about variables, functions, scope, and the value of `this`.

There are three commonly discussed types:

1. Global Execution Context: Created when JavaScript starts executing a script.
2. Function Execution Context: Created whenever a function is invoked.
3. Eval Execution Context: Created when code is executed using `eval()`.

An execution context goes through two broad phases:

- Creation phase: Sets up bindings, scope information, and `this`.
- Execution phase: Executes the code line by line.

Interview takeaway: Function calls create new execution contexts, which are managed through the call stack.

## What is the difference between the call stack and the execution context?

An execution context represents the environment in which code executes, while the call stack is the mechanism used to track active execution contexts.

Whenever a function is called, its execution context is pushed onto the call stack. Once the function completes, its context is popped.

## What is lexical scope and how does scope chaining work?

Lexical scope means that a function's access to variables is determined by where the function is physically written in the code, not where it is called.

Scope chaining allows JavaScript to search for a variable in the current scope, then its outer scope, continuing until the global scope is reached.

```javascript
let a = 10;

function outer() {
    let b = 20;

    function inner() {
        let c = 30;

        console.log(a, b, c);
    }

    inner();
}

outer(); // 10 20 30
```

## What is the difference between this in regular functions and arrow functions?

In regular functions, `this` is generally determined by how the function is called. In arrow functions, `this` is lexically inherited from the surrounding scope and cannot be independently changed using `call()`, `apply()`, or `bind()`.

```javascript
const user = {
    name: "John",

    regular() {
        console.log(this.name);
    },

    arrow: () => {
        console.log(this.name);
    }
};

user.regular(); // John
user.arrow();   // Usually undefined in a normal browser script
```

Interview takeaway: Arrow functions do not have their own `this`, `arguments`, or `prototype`. They are particularly useful for callbacks where preserving the surrounding `this` is important.

## What is the difference between function declarations and function expressions?

A function declaration defines a named function and is fully hoisted, meaning it can be called before its definition.

A function expression assigns a function to a variable. Its availability depends on the variable declaration and initialization.

```javascript
// Function declaration
greet();

function greet() {
    console.log("Hello");
}

// Function expression
const sayHello = function () {
    console.log("Hello");
};

sayHello();
```

Interview takeaway: Function declarations are fully hoisted, whereas function expressions are not independently hoisted. A `const` function expression cannot be accessed before initialization.

## What are arrow functions? How are they different from regular functions?

Arrow functions provide shorter function syntax and inherit `this` from their surrounding lexical scope.

Key differences:

- Arrow functions have lexical `this`.
- They cannot be used as constructors with `new`.
- They do not have their own `arguments` object.
- They do not have their own `prototype`.
- They support implicit returns for single-expression bodies.

```javascript
// Regular function
function add(a, b) {
    return a + b;
}

// Arrow function
const addNumbers = (a, b) => a + b;

console.log(addNumbers(2, 3)); // 5
```

## What are higher-order functions?

A higher-order function is a function that either accepts another function as an argument or returns another function.

They are commonly used in functional programming and array operations.

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

function add(x, y) {
    return x + y;
}

console.log(calculate(5, 3, add)); // 8
```

Examples include `map()`, `filter()`, and `reduce()`.

Interview takeaway: Higher-order functions help create reusable, modular, and composable code.

## What are callback functions? What is callback hell and how can it be avoided?

A callback is a function passed as an argument to another function, which is executed later or at a specific point during execution.

Callback hell occurs when multiple nested callbacks make code difficult to read, maintain, and debug.

```javascript
// Callback example
function greet(name, callback) {
    console.log("Hello " + name);
    callback();
}

greet("John", function () {
    console.log("Welcome!");
});
```

Callback hell example:

```javascript
getUser(function(user) {
    getOrders(user.id, function(orders) {
        getPayment(orders, function(payment) {
            console.log(payment);
        });
    });
});
```

It can be avoided using:  
Promises  
Async/await  
Modular functions

Interview takeaway: Callbacks are not inherently bad; deeply nested callbacks are what create callback hell.

## What is the prototype chain?

JavaScript uses prototypal inheritance, where objects can inherit properties and methods from other objects through their prototypes.

When accessing a property, JavaScript first checks the object itself. If the property is not found, it searches its prototype, then continues up the prototype chain until it finds the property or reaches `null`.

```javascript
const parent = {
    greet() {
        console.log("Hello");
    }
};

const child = Object.create(parent);

child.greet(); // Hello

console.log(Object.getPrototypeOf(child) === parent);
// true
```

Interview takeaway: The prototype chain is the mechanism behind JavaScript inheritance. Every ordinary object eventually inherits from `Object.prototype`, except objects created without a prototype.

## What are the different ways to clone an object in JavaScript?

There are two main types of cloning:

1. Shallow cloning: Copies only the first level. Nested objects still share references.

```
const original = {
    name: "John",
    address: { city: "Pune" }
};

const copy = { ...original };

copy.address.city = "Mumbai";

console.log(original.address.city); // Mumbai
```

Common shallow-copy methods:

- `Object.assign()`
- Spread operator (`...`)

2. Deep cloning: Creates an independent copy of nested objects as well.

```javascript
const original = {
    name: "John",
    address: { city: "Pune" }
};

const copy = structuredClone(original);

copy.address.city = "Mumbai";

console.log(original.address.city); // Pune
```

Interview takeaway: `structuredClone()` supports many built-in data types and circular references, but does not clone functions or arbitrary prototype chains. JSON stringify/parse is a more limited alternative.

## What is the difference between map(), filter(), reduce(), and forEach()?

These are JavaScript array methods used for iterating and processing arrays.


| Method      | Purpose                              | Returns            |
| ----------- | ------------------------------------ | ------------------ |
| `map()`     | Transforms each element              | New array          |
| `filter()`  | Selects matching elements            | New array          |
| `reduce()`  | Combines elements into one result    | Accumulator result |
| `forEach()` | Executes a callback for each element | `undefined`        |


```javascript
const numbers = [1, 2, 3, 4];

// map
console.log(numbers.map(n => n * 2));
// [2, 4, 6, 8]

// filter
console.log(numbers.filter(n => n > 2));
// [3, 4]

// reduce
console.log(numbers.reduce((sum, n) => sum + n, 0));
// 10

// forEach
numbers.forEach(n => console.log(n));
```

Interview takeaway: `map()`, `filter()`, and `reduce()` are useful when you need a returned result. `forEach()` is generally used for side effects.

## What is the difference between find(), findIndex(), and includes()?

All three methods are used to search for elements in an array, but they return different results.

- `find()`: Returns the first matching element or `undefined`.
- `findIndex()`: Returns the index of the first matching element or `-1`.
- `includes()`: Checks whether an array contains a particular value and returns a Boolean.

```
const numbers = [10, 20, 30, 40];

console.log(numbers.find(n => n > 20));
// 30

console.log(numbers.findIndex(n => n > 20));
// 2

console.log(numbers.includes(20));
// true
```

Interview takeaway: `find()` and `findIndex()` accept callback conditions, whereas `includes()` checks for a specific value using SameValueZero equality.

## What is synchronous vs asynchronous JavaScript?

Synchronous execution means code executes sequentially, and each operation must finish before the next one starts.

Asynchronous execution allows certain operations, such as timers and network requests, to complete later without blocking the main JavaScript thread while waiting.

```javascript
// Synchronous
console.log("First");
console.log("Second");

// Asynchronous
console.log("First");

setTimeout(() => {
    console.log("Second");
}, 1000);

console.log("Third");

//output:
// Synchronous part
First
Second

// Asynchronous part
First
Third
Second
```

Interview takeaway: JavaScript execution is generally single-threaded at the level of a given main execution thread, but the runtime provides asynchronous APIs and event-loop mechanisms to handle non-blocking operations.  


## What is the event loop in JavaScript?

The event loop is a mechanism that coordinates the call stack and task queues to enable asynchronous execution.

When the call stack becomes empty, the event loop processes queued work. Microtasks are processed before the next task (often called a macrotask) is taken from its queue.

Common examples:

- Microtasks: Promise callbacks, `queueMicrotask()`.
- Tasks: `setTimeout()`, `setInterval()`, DOM events.

```
console.log("Start");

setTimeout(() => {
    console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
    console.log("Promise");
});

console.log("End");
```

Output:

```
Start
End
Promise
Timeout
```

Interview takeaway: Even when `setTimeout()` has a delay of `0`, its callback does not execute immediately. Promise callbacks execute as microtasks before the next timer task.

## What is a Promise? Explain its different states.

A Promise is an object representing the eventual completion or failure of an asynchronous operation.

It has three states:

1. Pending: Initial state; operation is still in progress.
2. Fulfilled: Operation completed successfully.
3. Rejected: Operation failed.

Once fulfilled or rejected, a Promise is settled and cannot change its state again.

```javascript
const promise = new Promise((resolve, reject) => {
    const success = true;

    if (success) {
        resolve("Operation successful");
    } else {
        reject("Operation failed");
    }
});

promise
    .then(result => console.log(result))
    .catch(error => console.log(error))
    .finally(() => console.log("Completed"));
```

Interview takeaway: Promises help manage asynchronous operations and avoid deeply nested callbacks.

## What are async/await, and how do they work internally?

`async/await` is syntactic sugar built on top of Promises that makes asynchronous code easier to read and maintain.

An `async` function always returns a Promise. The `await` keyword pauses execution of that async function until the Promise settles, without blocking the JavaScript main thread.

```javascript
async function getData() {
    const response = await fetch(
        "https://jsonplaceholder.typicode.com/users"
    );

    const data = await response.json();

    console.log(data);
}

getData();
```

Interview takeaway: `await` can only be used inside an async function or at the top level of an ES module. Internally, async functions use Promise-based mechanisms to resume execution.

## How do you handle errors in Promises and async/await?

Errors in Promises can be handled using `.catch()`, while errors in async/await can be handled using `try...catch`.

```javascript
// Promise error handling
fetchData()
    .then(data => console.log(data))
    .catch(error => console.log(error));

// Async/await error handling
async function getData() {
    try {
        const data = await fetchData();
        console.log(data);
    } catch (error) {
        console.log(error);
    } finally {
        console.log("Execution completed");
    }
}
```

Interview takeaway: Use `try...catch` for sequential async operations. When using multiple independent Promises, `Promise.all()` can be combined with error handling to manage concurrent operations.

## What is the difference between setTimeout(), setInterval(), and requestAnimationFrame()?

These are browser timing APIs used to schedule code execution.


| Method                    | Purpose                                                |
| ------------------------- | ------------------------------------------------------ |
| `setTimeout()`            | Executes a callback once after a minimum delay         |
| `setInterval()`           | Repeatedly executes a callback at a specified interval |
| `requestAnimationFrame()` | Schedules a callback before the browser's next repaint |


```javascript
// Executes once
setTimeout(() => console.log("Hello"), 1000);

// Executes repeatedly
const interval = setInterval(() => {
    console.log("Repeated");
}, 1000);

// Stop interval
clearInterval(interval);

// Animation callback
requestAnimationFrame(() => {
    console.log("Before repaint");
});
```

Interview takeaway: `requestAnimationFrame()` is preferred for browser animations because it synchronizes with the browser's rendering cycle and can improve animation smoothness.

## What are JavaScript modules? Explain named exports vs default exports.

JavaScript modules allow code to be divided into separate files, making applications more maintainable, reusable, and organized.

There are two commonly used export types:

Named exports: A module can export multiple variables or functions by name.

```
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// app.js
import { add, subtract } from "./math.js";
```

Default export: A module can have one default export.

```
// user.js
export default function getUser() {
    return "John";
}

// app.js
import getUser from "./user.js";
```

Interview takeaway: Named exports generally require matching imported names (though aliases are allowed), while default exports can be imported using any local name.

## What is the difference between CommonJS and ES Modules?

CommonJS and ES Modules are two JavaScript module systems.


| Feature     | CommonJS                  | ES Modules            |
| ----------- | ------------------------- | --------------------- |
| Syntax      | `require()`               | `import`              |
| Export      | `module.exports`          | `export`              |
| Loading     | Traditionally synchronous | Statically structured |
| Evaluation  | Runtime-oriented          | Module-based          |
| Environment | Traditionally Node.js     | Browsers and Node.js  |


```
// CommonJS
const fs = require("fs");

module.exports = { name: "John" };
```

```
// ES Modules
import fs from "node:fs";

export const user = { name: "John" };
```

Interview takeaway: ES Modules support static analysis, tree shaking, and top-level `await`. Modern Node.js supports both systems.

## What is debouncing and throttling? Where are they used?

Debouncing and throttling are techniques used to control how frequently a function executes, especially during frequent events such as scrolling, typing, and resizing.

Debouncing: Executes a function only after a specified period has passed without another event.

Throttling: Ensures a function executes at most once during a specified time interval.

```
// Debouncing
function debounce(fn, delay) {
    let timer;

    return function (...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            fn.apply(this, args);
        }, delay);
    };
}

// Throttling
function throttle(fn, delay) {
    let lastCall = 0;

    return function (...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;
            fn.apply(this, args);
        }
    };
}
```

Interview takeaway:

- Debouncing: Search input, autocomplete, API calls after typing.
- Throttling: Scroll events, resize events, mouse movement.

## What is the difference between localStorage, sessionStorage, and cookies?

These are browser storage mechanisms used to store information on the client side.


| Feature                   | localStorage           | sessionStorage         | Cookies                           |
| ------------------------- | ---------------------- | ---------------------- | --------------------------------- |
| Lifetime                  | Until manually cleared | Until tab session ends | Based on expiry                   |
| Capacity                  | Usually around 5–10 MB | Usually around 5–10 MB | Around 4 KB each                  |
| Sent with HTTP requests   | No                     | No                     | Yes, when applicable              |
| Accessible via JavaScript | Yes                    | Yes                    | Unless HttpOnly                   |
| Scope                     | Origin                 | Origin + tab session   | Depends on domain/path attributes |


```
// localStorage
localStorage.setItem("name", "John");
localStorage.getItem("name");

// sessionStorage
sessionStorage.setItem("token", "123");

// Cookies
document.cookie = "username=John; path=/";
```

Interview takeaway: Avoid storing sensitive authentication tokens in JavaScript-accessible storage when possible. `HttpOnly`, `Secure`, and `SameSite` cookie attributes help improve cookie security.

## What is the difference between JSON.stringify() and JSON.parse()?

`JSON.stringify()` converts a JavaScript value into a JSON string, whereas `JSON.parse()` converts a valid JSON string into a JavaScript value.

```javascript
const user = {
    name: "John",
    age: 25
};

// Object to JSON string
const jsonData = JSON.stringify(user);

console.log(jsonData);
// '{"name":"John","age":25}'

// JSON string to object
const parsedData = JSON.parse(jsonData);

console.log(parsedData.name); // John
```

Interview takeaway: `JSON.stringify()` is commonly used when sending data to APIs, while `JSON.parse()` is used when reading JSON data.

Be aware that JSON serialization does not preserve every JavaScript value. For example, functions and `undefined` object properties are omitted, while circular references cause an error.
