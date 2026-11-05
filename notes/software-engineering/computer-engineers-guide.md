---
title: Computer Engineer's Guide
date: 2026-10-29
tags: [GK]
pinned: true
---

## Difference between Data and Information

**Data** refers to raw, unprocessed facts and figures that have no meaning on their own. It can be numbers, words, measurements, or symbols that have not yet been organized or analyzed.

- Example: 25, 37, 19, 42 (just numbers with no context)

**Information** is data that has been processed, organized, and given context, making it meaningful and useful for decision-making.

- Example: "The average score of students in Class 10 is 30.75" (data arranged and interpreted)

## What is the internet?

The Internet is a worldwide network that connects computers, mobile phones, servers, and other devices so they can share information with each other.

## What is DNS?

DNS stands for **Domain Name System**. It is like the phonebook of the internet. It translates website names that humans can easily remember into IP addresses that computers use to find servers.

## What is IP address

An IP address (Internet Protocol address) is a numerical address assigned to a device or network interface so it can be identified and communicate over an IP network.

## Difference between Authentication and Authorization

#### [**1. Authentication (AuthN)**](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-1-authentication-authn)

Authentication is the process of verifying *who* is trying to access a system. It ensures that the entity (a user, device, or system) is who they claim to be.

- **How it works:** The user provides a form of identification and proof.
- **Common Factors:**
  - *Something you know:* Passwords, PINs, security questions.
  - *Something you have:* Smartphones (for OTPs/push notifications), hardware security keys (FIDO2/WebAuthn).
  - [*Something you are:* Fingerprints, facial recognition, iris scans\*\*.\*\*](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-something-you-are-fingerprints-facial-recognition-iris-scans)

#### [**2. Authorization (AuthZ)**](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-2-authorization-authz)

Authorization is the process of deciding *what* an authenticated user is permitted to do. Even if a system knows your exact identity, it must check whether you have the necessary clearance to view a file, edit a database, or execute a command.

- **How it works:** The system checks the user's roles, groups, or permissions against the requested resource.
- **Common Models:**
  - **RBAC (Role-Based Access Control):** Permissions are assigned to roles (e.g., "Manager", "Employee"), and users are assigned to those roles.
  - **ABAC (Attribute-Based Access Control):** Access is granted based on attributes like user location, time of day, and security clearance level.

## What are the stages a source code file goes through from compilation to execution?

### The Steps in That Pipeline:

1. **Preprocessing:** The preprocessor strips comments and processes directives (like `#include` in C++), inserting header contents and expanding macros.
2. **Compilation:** The compiler translates the high-level source code into intermediate assembly code tailored to the target CPU architecture.
3. **Assembly:** The assembler converts the assembly code into machine-readable binary code, producing an object file (`.o` or `.obj`).
4. **Linking:** The linker combines all compiled object files with external libraries (like the standard library) to resolve references and create a single, unified executable file.
5. **Loading:** The operating system's loader reads the executable file from disk, allocates virtual memory in RAM, sets up the call stack and heap, and hands control over to the CPU to start execution.

## **What is Call Stack?**

The **call stack** is a special region of computer memory that manages function execution in a program using a Last-In, First-Out (LIFO) structure. Whenever a function is called, a new block of memory called a **stack frame** (or activation record) is pushed onto the stack to store its parameters, local variables, and return address. Once the function finishes executing, its frame is automatically popped off, returning control and restoring the execution context of the calling function.
