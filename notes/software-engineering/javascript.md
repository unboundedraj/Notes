---
title: Javascript
date: 2026-11-01
tags: [js]
---

## Introduction

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
