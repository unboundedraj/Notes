---
title: "C++"
date: 2026-10-15
tags: ["C++"]
pinned: false
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

> Any decimal literal without a suffix (e.g., `3.14`) is treated as a `double` by the compiler.
>
> **Suffixes:** To explicitly make a literal a `float`, you must append an `f` or `F` (e.g., `3.14f`).
>
> *Note on Modifiers:* C++ allows you to modify the size or range of these primitive types using **type modifiers**: `signed`, `unsigned`, `short`, and `long`. For instance, an `unsigned int` only holds positive numbers, effectively doubling its positive range, while a `long long` increases the storage capacity for massive integers.

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

## **Rules For Naming Variable**

The names given to a variable are called [**identifiers**](https://www.geeksforgeeks.org/cpp/cpp-identifiers/). There are some rules for creating these identifiers (names):

- A name can only contain **letters** (A-Z or a-z), **digits** (0-9), and **underscores (\_)**.
- It should start with a **letter or an underscore only.**
- It is case sensitive.
- The name of the variable should not contain any whitespace and special characters (i.e. #, $, %, \*, etc).
- We cannot use [**C++ keyword**](https://www.geeksforgeeks.org/cpp/cpp-keywords/) (e.g. float, double, class) as a variable name.

## **C++ Operator Types**

C++ operators are classified into **6 types** on the basis of type of operation they perform:

## **Arithmetic Operators**

[**Arithmetic operators**](https://www.geeksforgeeks.org/cpp/cpp-arithmetic-operators/) are used to perform arithmetic or mathematical operations on the operands. For example, '**+**' is used for addition.

- **Addition**, +, Adds two operands
- **Subtraction**, -, Subtracts second operand from the first
- **Multiplication**, \*, Multiplies two operands
- **Division**, /, Divides first operand by the second operand
- **Modulo Operation**, %, Returns the remainder of an integer division
- **Increment**, ++, Increases the value of operand by 1
- **Decrement**, --, Decreases the value of operand by 1

> **++a** and **a++**, both are increment operators, however, both are slightly different. In **++a**, the value of the variable is incremented first and then it is used in the program. In **a++**, the value of the variable is assigned first and then it is incremented. Similarly happens for the decrement operator.

## **Relational Operators**

[**Relational operators**](https://www.geeksforgeeks.org/c/relational-operators-in-c/) are used for the comparison of the values of two operands. For example, '&gt;' check right operand is greater.

- **Is Equal To**, ==, Checks if both operands are equal
- **Greater Than**, &gt;, Checks if the first operand is greater than the second operand
- **Greater Than or Equal To**, &gt;=, Checks if the first operand is greater than or equal to the second operand
- **Less Than**, &lt;, Checks if the first operand is lesser than the second operand
- **Less Than or Equal To**, &lt;=, Checks if the first operand is lesser than or equal to the second operand
- **Not Equal To**, !=, Checks if both operands are not equal

## **Logical Operators**

[**Logical operators**](https://www.geeksforgeeks.org/c/relational-operators-in-c/) are used to combine two or more conditions or constraints or to complement the evaluation of the original condition in consideration. The result returns a Boolean value, i.e., true or false.

- **Logical AND**, &amp;&amp;, Returns true only if all the operands are true or non-zero
- **Logical OR**, ||, Returns true if either of the operands is true or non-zero
- **Logical NOT**, !, Returns true if the operand is false or zero

## **Bitwise Operators**

[**Bitwise operators**](https://www.geeksforgeeks.org/cpp/cpp-bitwise-operators/) are works on bit-level. So, compiler first converted to bit-level and then the calculation is performed on the operands.

- **Binary AND**, &amp;, Copies a bit to the result if it exists in both operands
- **Binary OR**, |, Copies a bit to the result if it exists in any of the operands
- **Binary XOR**, ^, Copies the bit to the result if it is present in either of the operands but not both
- **Left Shift**, &lt;&lt;, Shifts the value to the left by the number of bits specified by the right operand
- **Right Shift**, &gt;&gt;, Shifts the value to the right by the number of bits specified by the right operand
- **One's Complement**, `~`, Changes binary digits 1 to 0 and 0 to 1

> **Note:** Only char and int data types can be used with Bitwise Operators.

## **Assignment Operators**

[**Assignment operators**](https://www.geeksforgeeks.org/cpp/cpp-assignment-operators/) are used to assign value to a variable. We assign the value of right operand into left operand according to which assignment operator we use.  

- **Assignment**, =, Assigns the value on the right to the variable on the left
- **Add and Assignment**, +=, Adds the right operand to the left operand and assigns the result to the left operand
- **Subtract and Assignment**, -=, Subtracts the right operand from the left operand and assigns the result to the left operand
- **Multiply and Assignment**, \*=, Multiplies the left operand by the right operand and assigns the result to the left operand
- **Divide and Assignment**, /=, Divides the left operand by the right operand and assigns the result to the left operand

## **Ternary or Conditional Operators**

[**Conditional operator**](https://www.geeksforgeeks.org/cpp/cpp-ternary-or-conditional-operator/) returns the value, based on the condition. This operator takes **three operands**, therefore it is known as a **Ternary Operator**.

```cpp
Expression1 ? Expression2 : Expression3
```

In the above statement:

- The ternary operator **?** determines the answer on the basis of the evaluation of **Expression1**.
- If **Expression1** is true, then **Expression2** gets evaluated.
- If **Expression1** is false, then **Expression3** gets evaluated.

## **Miscellaneous Operators**

**Scope Resolution Operator (::)** in C++ is used to identify and specify the context (or scope) to which a variable, function, or class belongs. It directs the compiler to look for an identifier within a specific namespace, class, or the global scope.

1. Accessing Global Variables

```cpp
int x = 100; // Global variable

void printX() {
    int x = 10; // Local variable
    cout << x;   // Prints 10 (local)
    cout << ::x; // Prints 100 (global)
}
```

2. Defining Class Methods Externally

```cpp
class Rectangle {
public:
    int area(int w, int h); // Declaration only
};

// Definition outside the class
int Rectangle::area(int w, int h) {
    return w * h;
}
```

3. Accessing Static Class Members  
 Static variables and functions belong to the class itself rather than a specific object instance. They are accessed using the class name and the scope resolution operator.

```cpp
class Counter {
public:
    static int count;
};

// Initializing the static variable outside the class
int Counter::count = 0;
```

---

[**sizeof operator**](https://www.geeksforgeeks.org/cpp/cpp-sizeof-operator/) is a unary operator used to compute the size of its operand or variable in bytes. For example,

```cpp
sizeof (char);
sizeof (var_name);
```

[**Comma operator**](https://www.geeksforgeeks.org/cpp/comma-in-cpp/) is a binary operator that is used for multiple purposes. It is used as a separator or used to evaluate its first operand and discards the result; it then evaluates the second operand and returns this value (and type).

```cpp
int n = (m+1, m-2, m+5);
int a, b, c;
```

[**Addressof operator**](https://www.geeksforgeeks.org/cpp/cpp-pointer-operators/) is used to find the memory address in which a particular variable is stored. In C++, it is also used to create a [**reference**](https://www.geeksforgeeks.org/cpp/references-in-cpp/).

```
&var_name;
```

> \* is used for dereferencing a pointer

[**Dot operator**](https://www.geeksforgeeks.org/c/dot-operator-in-c/) is used to access members of structure variables or class objects using their object names.

```
obj . member;

```

[**Casting operators**](https://www.geeksforgeeks.org/cpp/casting-operators-in-cpp/) are used to convert the value of one data type to another data type. For example, for an integer value x:

```
(float)x
static_cast<float>(x)
```

## Operator Precedence in C++

**1. Scope Resolution**

- **Operator:** `::`
- **Description:** Global scope, namespace, and class scope resolution (Left-to-right).

**2. Postfix (Unary) Operators**

- **Operators:** `++`, `--` (post-increment/decrement), `()`, `[]` (function call and array subscript), `.`, `->` (member access), `typeid`, and casts (`static_cast`, etc.).
- **Associativity:** Left-to-right.

**3. Prefix (Unary) Operators**

- **Operators:** `++`, `--` (pre-increment/decrement), `+`, `-` (unary plus/minus), `!`, `~` (logical/bitwise NOT), `*`, `&` (dereference/address-of), `sizeof`, `alignof`, `new`, `delete`.
- **Associativity:** Right-to-left.

**4. Pointer-to-Member Operators**

- **Operators:** `.*`, `->*`
- **Associativity:** Left-to-right.

**5. Multiplicative Operators**

- **Operators:** `*`, `/`, `%` (multiplication, division, modulo)
- **Associativity:** Left-to-right.

**6. Additive Operators**

- **Operators:** `+`, `-` (addition and subtraction)
- **Associativity:** Left-to-right.

**7. Bitwise Shift Operators**

- **Operators:** `<<`, `>>` (shift left and shift right)
- **Associativity:** Left-to-right.

**8. Three-Way Comparison Operator**

- **Operator:** `<=>` (Spaceship operator, introduced in C++20)
- **Associativity:** Left-to-right.

**9. Relational Operators**

- **Operators:** `<`, `<=`, `>`, `>=` (less than, less-or-equal, greater than, greater-or-equal)
- **Associativity:** Left-to-right.

**10. Equality Operators**

- **Operators:** `==`, `!=` (equal to and not equal to)
- **Associativity:** Left-to-right.

**11. Bitwise AND**

- **Operator:** `&`
- **Associativity:** Left-to-right.

**12. Bitwise XOR (Exclusive OR)**

- **Operator:** `^`
- **Associativity:** Left-to-right.

**13. Bitwise OR (Inclusive OR)**

- **Operator:** `|`
- **Associativity:** Left-to-right.

**14. Logical AND**

- **Operator:** `&&`
- **Associativity:** Left-to-right.

**15. Logical OR**

- **Operator:** `||`
- **Associativity:** Left-to-right.

**16. Conditional (Ternary) Operator**

- **Operator:** `?:`
- **Associativity:** Right-to-left.

**17. Assignment Operators**

- **Operators:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=`, `&=`, `^=`, `|=`
- **Associativity:** Right-to-left.

**18. Throw Operator**

- **Operator:** `throw` (for exception handling)
- **Associativity:** Right-to-left.

**19. Comma Operator**

- **Operator:** `,` (separates expressions evaluated sequentially)
- **Associativity:** Left-to-right.

## **Loop Control Statements**

Generally, the normal flow of any loop is that it will repeat till its test condition is true. In each repetition, it will execute the given set of statements. But C++ provides ways to modify this normal flow. This can be done by using loop control statements shown below:  
The [**break**](https://www.geeksforgeeks.org/cpp/cpp-break-statement/) statement when encountered, terminates the loop regardless of its test condition. This is useful when the execution of loop is dependent on multiple conditions.

```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 0; i < 5; i++) {
        
        // Terminating before reaching i = 4
        if (i == 2) break;
        cout << "Hi" << endl; 
    }
    return 0;
}
```

The [**continue**](https://www.geeksforgeeks.org/cpp/continue-statement-cpp/) statement, when encountered, skips the remaining code inside the current iteration of the loop and proceeds to the next iteration. This is useful when you want to skip specific iterations based on certain conditions but still want to continue the loop execution.

```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 0; i < 5; i++) {
        
        // Skipping when i equals 2
        if (i == 2) continue;
        cout << "Hi" << endl; 
    }
    return 0;
}
```

In C++, the `goto` statement is a jump statement that provides an unconditional transfer of execution control from the `goto` statement to a labeled statement **within the same function**.

```cpp
#include <iostream>
using namespace std;

int main() {
    int count = 1;

    // The jump destination
    loopStart: 
    if (count > 3) {
        goto endProgram; // Jumps out of the loop logic
    }

    cout << "Count is: " << count << endl;
    count++;
    
    goto loopStart; // Jumps back to the label

    endProgram:
    cout << "Program finished!" << endl;
    return 0;
}
```

> The only scenario where experienced C++ developers occasionally use `goto` is to **break out of deeply nested loops**. Standard `break` only exits the innermost loop, whereas a `goto` can instantly escape multiple layers of nested loops to an error-handling cleanup block at the bottom of a function.

# **Vectors in C++**

---

A vector in C++ is a dynamic sequence container provided by the Standard Template Library (STL).

### **Using Initializer List**

We can initialize a vector with the list of values enclosed in **curly braces {}** known as [**initializer list**](https://www.geeksforgeeks.org/cpp/std-initializer_list-in-cpp-11/).

```
vector<type> v = {val1, val2, val3, ...};
```

### **One by One Initialization**

Vector can be initialized by pushing value one by one. In this method, an empty vector is created, and elements are added to it one by one using the [**vector::push\_back()**](https://www.geeksforgeeks.org/cpp/vector-push-back-cpp-stl/) method

```
v.push_back(val);
```

### **With a Single Value**

We can initialize all the elements of the vector to a single value. We create a vector of a specified size and initialize all elements to the same value using vector constructor.

```
vector<type> v(n, val);
```

**Where:**  
n -&gt; Size of vector  
val -&gt; Value assigned to all elements

### **From Another Vector**

We can also initialize a newly created vector from an already created vector if they are of same type.

```
vector<type> v2(v1.begin(), v1.end());
```

### **From Any STL Container**

Vectors are flexible containers that can be initialized by any other already existing containers such as set, multiset, map, etc. if they are of same type.

```
vector<type> v(first, last);
```

---

**A list of popular vector functions can be found in the table below.**


| **Function**                                                           | **Description**                                                  | Example                     | Importance |     |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------- | --------------------------- | ---------- | --- |
| [back()](https://www.w3schools.com/cpp/ref_vector_back.asp)            | Returns the last element of a vector                             | int b = vec.back();         |            |     |
| [at()](https://www.w3schools.com/cpp/ref_string_at.asp)                | Returns the character at a specified index, with bounds checking |                             |            |     |
| [clear()](https://www.w3schools.com/cpp/ref_vector_clear.asp)          | Removes all of the contents of a vector                          | vec.clear();                |            |     |
| [front()](https://www.w3schools.com/cpp/ref_vector_front.asp)          | Returns the first element of a vector                            | int f = vec.front();        |            |     |
| [push\_back()](https://www.w3schools.com/cpp/ref_vector_push_back.asp) | Adds an element to the end of a vector                           | vec.push\_back(10);         | \*\*\*     |     |
| [pop\_back()](https://www.w3schools.com/cpp/ref_vector_pop_back.asp)   | Removes the last element of a vector                             | vec.pop\_back();            | \*         |     |
| [swap()](https://www.w3schools.com/cpp/ref_vector_swap.asp)            | Swaps the contents of one vector with another                    | vec1.swap(vec2);            | \*         |     |
| size()                                                                 | Returns the number of elements currently in the vector.          | int s = vec.size();         | \*\*\*     |     |
| empty()                                                                | Checks whether the vector is empty (returns `true` or `false`).  | bool isEmpty = vec.empty(); |            |     |


# Maps in C++

---

A map stores elements in "**key/value**" pairs.

Elements in a map are:  
Accessible by keys (not index), and each key is unique.  
Automatically sorted in ascending order by their keys.  
Maps store the pair of values in the sorted order on account of the first value however memory allocation is not sequential

```
//SYNTAX:
map<key's data type, value's data type>map name;
```

> When accessing elements using the **\[\] operator**, if the key does not already exist, it is inserted into the map with a default-constructed value. For primitive types like int, this default construction results in zero initialization. Therefore, if you access **map\[key\]** for a non-existent key, the map will create a new entry with that key and a value of 0. If the key exists, the current value will be returned.

**A list of popular vector functions can be found in the table below.**


| Function                                                            | Description                                                                                                                             | Example                                          | Importance |     |
| ------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ | ---------- | --- |
| [map::insert()](https://www.geeksforgeeks.org/map-insert-in-c-stl/) | Insert elements with a particular key in the map container –&gt; O(log n)<br>                                                           | Map.insert({key,value})                          |            |     |
| erase()                                                             | Removes elements by key, by iterator, or a range of iterators.                                                                          | myMap.erase("apple");                            |            |     |
| swap()                                                              | Swaps the contents of this map with another map.                                                                                        | myMap.swap(otherMap);                            |            |     |
| size()                                                              | Returns the number of key-value pairs currently in the map.                                                                             | int s = myMap.size();                            |            |     |
| lower\_bound()                                                      | Returns an iterator to the first element whose key is *not less than* (&gt;=) the given key.                                            | auto it = myMap.lower\_bound(10);                |            |     |
| upper\_bound()                                                      | Returns an iterator to the first element whose key is *strictly greater than* (&gt;) the given key.                                     | auto it = myMap.upper\_bound(10);                |            |     |
| find()                                                              | Returns an iterator pointing to the key-value pair, or `map::end` if the key is not found.                                              | auto it = myMap.find("apple");                   |            |     |
| count()                                                             | Returns the number of elements matching the specific key. For standard maps/sets, it only returns `1` (exists) or `0` (does not exist). | if (myMap.count("apple")) { /\* key exists \*/ } | \*\*\*     |     |
| [map::clear()](https://www.geeksforgeeks.org/mapclear-c-stl/)       | Removes all the elements from the map.                                                                                                  |                                                  |            |     |
|                                                                     |                                                                                                                                         |                                                  |            |     |


## Unordered Map

An `std::unordered_map` in C++ is an associative container from the Standard Template Library (STL) that stores data in key-value pairs. It is implemented internally using a hash table.

> **Time Complexity:** It offers an average-case time complexity of O(1) for insertions, deletions, and lookups. This makes it significantly faster than a standard `std::map` (which takes O(log N) time) for large datasets.

# Sets in C++

---

A `std::set` in C++ is an associative container that stores unique elements in a specifically sorted order (ascending by default). It is implemented internally as a balanced binary search tree (typically a Red-Black Tree), which means its core operations—insertion, deletion, and search execute in O(log N) time.

```
std::set<int> numbers;
```


| Function       | Description                                                        | Example                           | Importance |     |
| -------------- | ------------------------------------------------------------------ | --------------------------------- | ---------- | --- |
| insert()       | Adds a new element to the set and automatically sorts it.          | mySet.insert(15);                 |            |     |
| erase()        | Removes a specific element by value or via an iterator.            | mySet.erase(15);                  |            |     |
| find()         | Returns an iterator to the element if found, or `set::end` if not. | auto it = mySet.find(10);         |            |     |
| count()        | Returns 1 if the element exists in the set, and 0 if it does not.  | if (mySet.count(10)) { }          | \*\*       |     |
| size()         | Returns the total number of elements currently in the set          | int s = mySet.size();             |            |     |
| empty()        | Checks whether the set is empty (returns `true` or `false`).       | bool isEmpty = mySet.empty();     |            |     |
| clear()        | Removes all elements from the set.                                 | mySet.clear();                    |            |     |
| lower\_bound() | Returns an iterator to the first element $\\ge$ the given value.   | auto it = mySet.lower\_bound(10); |            |     |
| upper\_bound() | Returns an iterator to the first element $&gt;$ the given value.   | auto it = mySet.upper\_bound(10); |            |     |


# Strings in C++

---

**The** `<string>` **library has many functions that allow you to perform tasks on strings.**


| **Function**                                                    | **Description**                                                                                       | **Example**      | Importance |     |
| --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ---------------- | ---------- | --- |
| append()                                                        | Adds characters or another string to the end of the current string                                    | str.append("!"); |            |     |
| [at()](https://www.w3schools.com/cpp/ref_string_at.asp)         | Returns the character at a specified index, with bounds checking                                      |                  |            |     |
| [length()](https://www.w3schools.com/cpp/ref_string_length.asp) | Returns the number of characters in the string                                                        |                  |            |     |
| push\_back()                                                    | Adds a single character to the end of the string                                                      |                  |            |     |
| pop\_back()                                                     | Removes the last character from the string                                                            |                  |            |     |
| [size()](https://www.w3schools.com/cpp/ref_string_size.asp)     | Alias of [length()](https://www.w3schools.com/cpp/ref_string_length.asp); returns the string's length |                  |            |     |
| substr()                                                        | Returns a portion of the string, starting at a given index and length                                 |                  |            |     |
| swap()                                                          | Exchanges the contents of two strings                                                                 |                  |            |     |


# Stack in C++

---

A Stack is a linear data structure that strictly follows the **Last-In, First-Out (LIFO)** principle. The last element added to the stack is always the first one to be removed.

**Time &amp; Space Complexity:**

- **Push (Insert):** O(1)
- **Pop (Remove):** O(1)
- **Peek / Top (Access):** O(1)  

  
  | Function | Description                                                        | Example                              | Importance |     |
  | -------- | ------------------------------------------------------------------ | ------------------------------------ | ---------- | --- |
  | push()   | Pushes an element onto the stack represented by this deque.        | stack.push(10);                      |            |     |
  | pop()    | Removes the top element. **Note: It does not return the element.** | st.pop();                            |            |     |
  | top()    | Returns a reference to the top element without removing it.        | int val = [st.top](http://st.top)(); |            |     |
  | empty()  | Checks if the stack is empty (returns `true` or `false`).          | bool isEmpty = st.empty();           |            |     |
  | size()   | Returns the number of elements in the stack.                       | int s = st.size();                   |            |     |
