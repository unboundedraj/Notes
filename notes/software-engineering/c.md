---
title: "C++"
date: 2026-10-15
tags: ["C++"]
---

## Introduction

C++ is a general-purpose programming language developed by **Bjarne Stroustrup** as an extension of C.  
C++ is a programming language known for its fast speed, low level memory management and is often taught as first programming language.  
Syntax similarity with C, Java, and C# makes it easier to switch languages.  
C++ is machine-independent at the **source code level**, but machine-dependent at the **compiled executable level**.  
C++ provides low-level access to system resources  
**Direct Memory Manipulation:** C++ uses pointers, which are variables that store the exact physical memory addresses of data. This allows developers to read from, write to, or manipulate specific locations in the RAM directly.  
**Manual Memory Management:** Unlike languages with automatic garbage collection (like Java or Python), C++ requires developers to explicitly allocate and free memory (using `new` and `delete`). This gives precise control over when resources are consumed and released.

---

The below C++ code shows the basic structure of a program.

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

- **Header File:** #include &lt;iostream&gt; adds input/output objects (cin, cout, etc.) via the preprocessor. Common headers: fstream (files), string (strings), vector (STL), bits/stdc++.h (all-in-one).
- **Namespace Declaration:** using namespace std; allows direct use of standard names like "cout" without std::
- **Main Function:** int main() is the program’s entry point; execution starts here and returns an integer with return 0 mean successful execution

**Comments:** // for single line, /\*....\*/ for multi-line are ignored by the compiler and used only for code documentation.

## Data types

**1. Built-in (Primitive) Data Types**  
These are the fundamental data types native to the C++ compiler.

- **Integer (**`int`**):** Stores whole numbers without decimals. Typically requires 4 bytes of memory. Example: `int age = 25;`
- **Character (**`char`**):** Stores a single character and requires 1 byte of memory. Characters are enclosed in single quotes. Example: `char grade = 'A';`
- **Boolean (**`bool`**):** Stores logical values, taking 1 byte of memory. It can only hold `true` (1) or `false` (0). Example: `bool is_valid = true;`
- **Floating-Point (**`float`**):** Stores single-precision decimal numbers. Typically requires 4 bytes of memory. Example: `float pi = 3.14f;`
- **Double Floating-Point (**`double`**):** Stores double-precision decimal numbers for higher accuracy. Typically requires 8 bytes of memory. Example: `double precise_pi = 3.14159265;`
- **Void (**`void`**):** Represents an absence of a value. It is primarily used for functions that do not return any data.  
  
*Note on Modifiers:* C++ allows you to modify the size or range of these primitive types using **type modifiers**: `signed`, `unsigned`, `short`, and `long`. For instance, an `unsigned int` only holds positive numbers, effectively doubling its positive range, while a `long long` increases the storage capacity for massive integers.

**2. Derived Data Types:**   
These types are constructed by modifying or grouping built-in data types.

- **Arrays:** A collection of elements of the same data type stored in contiguous memory locations. Example: `int scores[5] = {90, 85, 92, 88, 95};`
- **Pointers:** Variables that store the physical memory address of another variable rather than a direct value. Example: `int* ptr = &age;`
- **References:** An alias or alternative name for an already existing variable. Example: `int& ref = age;`
- **Functions:** A block of code that performs a specific task and returns a specific data type (or `void`).

**3. User-Defined Data Types**  
These are custom data types defined by the programmer to group disparate data together or create complex architectural structures.

- **Structures (**`struct`**):** Groups variables of *different* data types under a single name. Elements are accessed via dot notation.
- **Classes (**`class`**):** The foundation of C++ object-oriented programming. Similar to a `struct`, but it encapsulates both data variables and member functions, with data typically hidden via access modifiers (`private`, `public`, `protected`).
- **Unions (**`union`**):** Similar to a `struct`, but all members share the exact same memory location. The size of the union is determined by its largest member, and it can only hold one member's value at a time.
- **Enumerations (**`enum`**):** Creates a customized data type consisting of a set of named integer constants, improving code readability. Example: `enum Color { RED, GREEN, BLUE };`
- **Typedef (**`typedef`**):** Allows you to create a new alias or nickname for an existing data type. Example: `typedef unsigned long ulong;`

## **Data Type Modifiers**

**short:** Specifies a smaller integer type when supported.  
**long:** Specifies an integer type with at least as much storage as int.  
**signed:** Allows an integer type to represent both positive and negative values.  
**unsigned:** Allows an integer type to represent only non-negative values and provides a larger positive range

---
