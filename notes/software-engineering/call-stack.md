---
title: Call Stack
date: 2026-10-17
tags: [call stack]
---

The **call stack** is a special region of computer memory that manages function execution in a program using a Last-In, First-Out (LIFO) structure. Whenever a function is called, a new block of memory called a **stack frame** (or activation record) is pushed onto the stack to store its parameters, local variables, and return address. Once the function finishes executing, its frame is automatically popped off, returning control and restoring the execution context of the calling function.
