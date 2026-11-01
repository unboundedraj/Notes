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
