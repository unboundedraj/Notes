---
title: NodeJS
date: 2026-11-04
tags: [node, nodejs]
---

## What is Node.js, and how is it different from traditional backend technologies?

Node.js is an open-source JavaScript runtime built on Chrome’s V8 engine that executes code on the server side, whereas traditional backend technologies such as Java, Python, or PHP typically employ a multi-threaded, thread-per-request model where each connection is assigned a dedicated thread that can block during I/O operations. In contrast, Node.js operates on a single-threaded event loop utilizing non-blocking asynchronous I/O, allowing it to offload tasks and efficiently manage tens of thousands of concurrent connections with a minimal memory footprint, making it exceptionally well-suited for I/O-bound and real-time applications rather than heavy CPU-intensive processing.

## Is Node.js single-threaded? If yes, how does it handle multiple concurrent requests?

Node.js executes JavaScript on a main thread using a single Call Stack, but it is not entirely single-threaded. It delegates asynchronous I/O operations to the operating system or libuv's thread pool. Once an operation completes, its callback is scheduled for execution through the Event Loop. This allows Node.js to handle multiple concurrent requests without creating a separate JavaScript thread for every request.

## What is the V8 engine, and what role does it play in Node.js?

V8 is Google's open-source JavaScript engine, written in C++, that executes JavaScript code. It compiles JavaScript into machine code using techniques such as Just-In-Time (JIT) compilation and performs memory management and garbage collection. Node.js uses V8 to execute JavaScript outside the browser.

## What is the difference between Node.js and JavaScript running in a browser?

The core differences lie in their execution contexts, available APIs, and access to the underlying system:


|                              |                                                                                                                     |                                                                                                                                         |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **Feature**                  | **JavaScript in a Browser**                                                                                         | **Node.js**                                                                                                                             |
| **Primary Environment**      | Client-side (runs inside the user's web browser).                                                                   | Server-side or local machine (runs as a standalone process).                                                                            |
| **Global Objects &amp; DOM** | Has full access to the **DOM** (`document`, `window`), and browser Web APIs (`fetch`, `localStorage`, `navigator`). | Has **no DOM** or browser APIs; instead, it provides server-side globals (`process`, `Buffer`) and core modules (`fs`, `path`, `http`). |
| **File System Access**       | Strictly sandboxed for security; **cannot** directly read, write, or delete files on the user's local file system.  | Has **full access** to the operating system's file system and hardware via native modules like `fs`.                                    |
| **Module System**            | Traditionally relies on ES Modules (`import`/`export`) native to the browser, often bundled via Webpack/Vite.       | Historically used **CommonJS** (`require`/`module.exports`), though modern Node.js versions fully support ES Modules.                   |
| **Primary Use Cases**        | Building interactive user interfaces, client-side routing, handling user events, and rendering web pages.           | Building backend APIs, microservices, real-time chat apps, CLI tools, and automation scripts.                                           |


## What is the role of `libuv` in Node.js?

Libuv is a C library that provides Node.js with an event loop, asynchronous I/O capabilities, and a thread pool. It handles operations such as file system access, DNS lookups, and certain cryptographic operations. It enables Node.js to perform non-blocking operations without blocking the main JavaScript thread.

## What are the advantages and disadvantages of using Node.js?

Advantages:

- Uses JavaScript for both frontend and backend development.
- Non-blocking I/O makes it suitable for handling concurrent connections.
- Large ecosystem of packages through npm.
- Well-suited for real-time applications and APIs.
- Supports scalable, event-driven architectures.

Disadvantages:

- CPU-intensive operations can block the Event Loop.
- Asynchronous code can become difficult to manage if poorly structured.
- Some packages may have compatibility or maintenance issues.
- Not always ideal for heavy computational workloads.

## What is the Event Loop in Node.js, and how does it work internally?

The Event Loop is the mechanism that allows Node.js to execute non-blocking asynchronous operations despite having a single main JavaScript thread. It continuously checks whether the Call Stack is free and processes callbacks from different queues and event loop phases. When asynchronous operations complete, their callbacks are scheduled for execution, allowing Node.js to handle multiple operations efficiently.

## Explain the different phases of the Node.js Event Loop.

The Node.js Event Loop consists of six main phases:

1. Timers: Executes callbacks scheduled by `setTimeout()` and `setInterval()` when their thresholds have elapsed.
2. Pending Callbacks: Executes certain system-level I/O callbacks deferred from previous iterations.
3. Idle, Prepare: Used internally by Node.js and libuv.
4. Poll: Retrieves new I/O events and executes related callbacks.
5. Check: Executes callbacks scheduled by `setImmediate()`.
6. Close Callbacks: Executes close event callbacks, such as `socket.on('close')`.

Microtasks, including Promise callbacks and `process.nextTick()` callbacks, are processed between relevant execution points rather than being separate Event Loop phases.

## What is the difference between `process.nextTick()`, `setImmediate()`, and `setTimeout()`?

- `process.nextTick()`: Executes its callback after the current JavaScript operation completes, before the Event Loop continues.
- `setImmediate()`: Executes its callback in the Check phase of the Event Loop.
- `setTimeout()`: Executes its callback after a specified minimum delay, provided the Event Loop can process it.

Example:

```
console.log("Start");

process.nextTick(() => console.log("Next Tick"));

setTimeout(() => console.log("Timeout"), 0);

setImmediate(() => console.log("Immediate"));

console.log("End");
```

The guaranteed initial output is:

```
Start
End
Next Tick
```

The relative order of `setTimeout()` and `setImmediate()` here is not guaranteed.

## What is the difference between synchronous and asynchronous operations in Node.js?

Synchronous operations execute one after another and block further JavaScript execution until the current operation completes. Asynchronous operations allow execution to continue while waiting for an operation to finish, with the result handled later through callbacks, Promises, or async/await.

```
const fs = require("fs");

// Synchronous
const data = fs.readFileSync("file.txt", "utf8");
console.log(data);

// Asynchronous
fs.readFile("file.txt", "utf8", (err, data) => {
    if (err) throw err;
    console.log(data);
});

console.log("This can execute before file reading completes");
```

## 11. What are callbacks, and what is Callback Hell? How can it be avoided?

A callback is a function passed as an argument to another function and executed when an operation completes. Callback Hell occurs when multiple nested callbacks make code difficult to read, debug, and maintain.

It can be avoided using:

- Promises.
- Async/await.
- Modular functions.
- Proper error handling.

```javascript
// Callback Hell
getUser(id, (user) => {
    getOrders(user.id, (orders) => {
        getPayment(orders[0], (payment) => {
            console.log(payment);
        });
    });
});

// Using async/await
async function getDetails(id) {
    const user = await getUser(id);
    const orders = await getOrders(user.id);
    const payment = await getPayment(orders[0]);

    console.log(payment);
}
```

## What are Promises, and how do they work internally?

A Promise is an object representing the eventual completion or failure of an asynchronous operation. It has three states: `pending`, `fulfilled`, and `rejected`. Once settled, its state cannot change. We handle successful results using `.then()` and errors using `.catch()`.

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
    .catch(error => console.error(error));
```

## What is the difference between `Promise.all()`, `Promise.allSettled()`, `Promise.race()`, and `Promise.any()`?


| Method                 | Behaviour                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------- |
| `Promise.all()`        | Resolves when all Promises resolve; rejects as soon as one rejects.                   |
| `Promise.allSettled()` | Waits for all Promises to settle, regardless of success or failure.                   |
| `Promise.race()`       | Settles with the first Promise that settles, whether fulfilled or rejected.           |
| `Promise.any()`        | Resolves with the first fulfilled Promise; rejects with AggregateError if all reject. |


Example:

```javascript
const p1 = Promise.resolve("A");
const p2 = Promise.resolve("B");
const p3 = Promise.reject("Error");

Promise.all([p1, p2]).then(console.log);

Promise.allSettled([p1, p3]).then(console.log);

Promise.race([p1, p2]).then(console.log);

Promise.any([p3, p2]).then(console.log);
```

## How does `async/await` work, and how is it different from Promises?

`async/await` is syntactic sugar built on top of Promises that makes asynchronous code look synchronous. An `async` function always returns a Promise, while `await` pauses execution of that async function until the Promise settles without blocking the main JavaScript thread.

```javascript
async function fetchUser() {
    try {
        const response = await fetch("https://api.example.com/users");
        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

## What is the difference between the Call Stack, Callback Queue, and Event Loop?

- Call Stack: Maintains the execution context of currently running JavaScript functions.
- Callback Queue: Holds callbacks waiting for execution, including callbacks associated with certain Event Loop phases.
- Event Loop: Coordinates execution by checking whether the Call Stack is available and processing eligible callbacks.

In Node.js, there are also separate mechanisms for microtasks and `process.nextTick()`, so the browser's simplified queue model does not fully describe Node.js scheduling.

## How does Node.js handle CPU-intensive tasks?

CPU-intensive tasks can block the main JavaScript thread and prevent the Event Loop from processing other requests. Node.js can handle such tasks using `worker_threads`, child processes, or external services. Worker threads are particularly useful for CPU-intensive JavaScript calculations because they execute JavaScript in separate threads.

```javascript
const { Worker } = require("worker_threads");

const worker = new Worker("./worker.js");

worker.on("message", result => {
    console.log("Result:", result);
});

worker.on("error", console.error);
```

## What is the Cluster module in Node.js, and why is it used?

The Cluster module allows Node.js applications to create multiple worker processes that can share the same server port. Each worker is a separate process with its own JavaScript thread and memory space. It helps utilize multiple CPU cores and improves the ability to handle concurrent requests.

```javascript
const cluster = require("cluster");
const os = require("os");
const http = require("http");

if (cluster.isPrimary) {
    const cpuCount = os.availableParallelism();

    for (let i = 0; i < cpuCount; i++) {
        cluster.fork();
    }
} else {
    http.createServer((req, res) => {
        res.end(`Worker ${process.pid}`);
    }).listen(3000);
}
```

## What is the difference between concurrency and parallelism in Node.js?

Concurrency means handling multiple tasks during overlapping periods by switching between them or progressing them asynchronously. Parallelism means executing multiple tasks simultaneously, typically using multiple CPU cores or threads.

Node.js achieves concurrency through its Event Loop and asynchronous I/O, while parallelism can be achieved using worker threads or child processes.

## What happens internally when Node.js executes an I/O operation?

When Node.js executes an asynchronous I/O operation, it delegates the work to the operating system or libuv thread pool, depending on the operation. The main JavaScript thread continues executing other code instead of waiting. Once the operation completes, its callback is scheduled through the appropriate Event Loop mechanism and executed when the JavaScript thread becomes available.

## What is the difference between CommonJS and ES Modules in Node.js?

CommonJS (CJS) is the traditional module system in Node.js that uses `require()` and `module.exports`. ES Modules (ESM) is the standard JavaScript module system that uses `import` and `export`. CommonJS loads modules synchronously, whereas ES Modules support static imports and asynchronous module loading. ESM also supports features such as top-level `await`.

```javascript
// CommonJS
const fs = require("fs");
module.exports = {};

// ES Modules
import fs from "fs";
export default {};
```

## What is the difference between `require()` and `import`?

`require()` belongs to CommonJS and loads modules dynamically at runtime. `import` belongs to ES Modules and supports static analysis, named imports, and tree-shaking by compatible bundlers. Static `import` declarations must appear at the top level of a module, while `require()` can be called conditionally or inside functions.

```javascript
// require()
const express = require("express");

// import
import express from "express";

// Dynamic import
const module = await import("./module.js");
```

## What is module caching in Node.js?

Node.js caches modules after their first successful load using CommonJS `require()`. When the same module is required again, Node.js returns its cached exports instead of executing the module again. This improves performance and ensures that modules generally share the same exported object within a process.

```javascript
// app.js
const first = require("./config");
const second = require("./config");
console.log(first === second); // true
```

## What is the difference between `package.json` and `package-lock.json`?

`package.json` contains project metadata, scripts, dependencies, version requirements, and configuration. `package-lock.json` records the exact dependency tree and resolved package versions, including dependency information, to ensure consistent installations across environments.

In short: `package.json` defines what the project needs, whereas `package-lock.json` records exactly what was installed.

## What is the difference between dependencies, devDependencies, and peerDependencies?

- dependencies: Packages required for the application to run in production.
- devDependencies: Packages required during development, testing, or building, such as ESLint and Jest.
- peerDependencies: Packages that a library expects the consuming project to provide, often to ensure compatibility with a shared dependency.

Example:

```javascript
{
  "dependencies": {
    "express": "^5.0.0"
  },
  "devDependencies": {
    "jest": "^30.0.0"
  },
  "peerDependencies": {
    "react": ">=18"
  }
}
```

## What is the purpose of `__dirname`, `__filename`, and the `path` module?

- `__dirname`: Returns the absolute directory path of the current CommonJS module.
- `__filename`: Returns the absolute file path of the current CommonJS module.
- `path`: Provides utilities for working with file and directory paths across operating systems.

```
const path = require("path");

console.log(__dirname);
console.log(__filename);

const filePath = path.join(__dirname, "uploads", "file.txt");

console.log(filePath);
```

Note: `__dirname` and `__filename` are not directly available in ES Modules. They can be recreated using `import.meta.url` and Node.js URL utilities.
