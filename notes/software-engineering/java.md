---
title: Java
date: 2026-10-15
tags: [Java]
---

## Introduction

Java is a high-level, object-oriented programming language used to build web apps, mobile applications, and enterprise software systems.  
Java is a platform-independent language, which means code written in Java can run on any device that supports the Java Virtual Machine (JVM).  
Syntax and structure are similar to C-based languages like C++ and C#.  
Supports object-oriented programming concepts like classes, objects, inheritance, and polymorphism

---

Traditional Hello World Program in java:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

`public`: This is an **access modifier**. It means this class is visible and accessible to other classes.  
`class`: The keyword used to declare a blueprint for objects. **Rule in Java:** *Everything* must live inside a class. Unlike C++, Java does not support global functions or global variables outside of a class.  
`HelloWorld`: The name of the class. By Java convention, class names use PascalCase. **Important Rule:** In Java, the name of the main public class *must* match the file name exactly (so this code must be saved in a file named `HelloWorld.java`).

**The Main Method:** `public static void main(String[] args)`  
This is the exact entry point of your program analogous to `int main()` in C++. When you run a Java application, the Java Virtual Machine (JVM) looks specifically for this method signature to start execution.

> `public`: Must be public so the JVM (which lives outside your class) can call it to start the program.  
> `static`: Means this method belongs to the class itself rather than an instance (object) of the class. The JVM calls `main` without needing to create an object of `HelloWorld` first.  
> `void`: The return type. It returns nothing to the OS/JVM (unlike C++ where `main` typically returns an `int` exit code like `0`).  
> `main`: The mandatory name of the entry-point method. The JVM is hardcoded to look for a method named `main`.  
> `String[] args`: Command-line arguments. It accepts an array of strings (similar to `argv` in C++) if you pass arguments via the terminal when launching the program.

**System.out.println("Hello World!");**

This line prints text to the console and moves the cursor to a new line (equivalent to `std::cout << "Hello World!" << std::endl;` in C++).

> `System`: A built-in core class provided by Java (located in the `java.lang` package) that gives access to standard input/output systems.  
> `out`: A `static` public member variable inside the `System` class representing the standard output stream (the console).  
> `println`: A method belonging to the output stream that prints whatever is inside the parentheses and appends a newline character at the end. (You can also use `print` if you don't want a new line).  
> `"Hello World!"`: A string literal (text enclosed in double quotes).  
> `;`: The statement terminator, required at the end of every statement in Java, just like in C++.

- Write code in a file like [HelloWorld.java](http://HelloWorld.java).
- Java Compiler "javac" compiles it into bytecode "HelloWorld.class".
- [**JVM**](https://www.geeksforgeeks.org/java/differences-jdk-jre-jvm/) (Java Virtual Machine) reads the .class file and interprets the bytecode.
- The JVM initially interprets bytecode and uses JIT (Just-In-Time) compilation to convert frequently executed code into native machine code for better performance

## **Naming Rules of Java Variables**

- **Valid Characters**: Variable names can contain Unicode letters and digits, as well as \_ and $, according to Java identifier rules.
- **Starting Character**: A variable name cannot start with a digit. It must begin with a valid identifier-start character, such as a letter, \_, or $.
- **No Reserved Keywords**: Reserved Java keywords such as int, class, and if cannot be used as variable names.
- **Case-Sensitive**: Java treats names such as age and Age as different variables.
- **No Spaces**: Variable names cannot contain spaces.
- **Meaningful Names**: Use descriptive names that clearly indicate the purpose of the variable, such as studentName instead of s.
- **Naming Convention**: Use camelCase for variable names, such as totalMarks or studentAge

> Java **constants** are declared using the `final` keyword (often combined with `static` at the class level to match conventions like `MAX_USERS`), ensuring they can only be assigned a value once and throwing a compiler error if modified. This differs from C++, which uses `const` or compile-time `constexpr` keywords and allows global or standalone constant definitions outside of classes.
>
> **Java does not allow re-declaring a local variable with the same name in nested blocks within the same method**  
> **Just like C++, any floating-point literal without a suffix (e.g.,** `3.14`**) is automatically treated as a** `double`

## **Data Types**

Data types in Java define the kind of data a variable can hold and the memory required to store it. They are broadly divided into two categories:

- **Primitive Data Types:** Store simple values directly in memory.
- **Non-Primitive (Reference) Data Types:** Store memory references to objects.

## **1. Primitive Data Types**

Primitive data types store simple values directly in memory. Java provides eight primitive data types, each with a fixed size and range, which are summarized below:

1. `byte`

- **Size &amp; Range:** 8-bit signed integer, with a range from **-128 to 127.**
- **Use Case:** Primarily used to save memory in large arrays where memory savings are critical, especially when data is being handled from a network or file stream.

### 2. `short`

- **Size &amp; Range:** 16-bit signed integer, with a range from **-32,768 to 32,767.**
- **Use Case:** Like the `byte`, it is used to save memory in large data structures, though it is used less frequently in modern applications since memory is cheap.

### 3. `int`

- **Size &amp; Range:** **32-bit signed integer**, ranging from roughly **-2 billion to 2 billion (-{2,147,483,648} to {2,147,483,647}).**
- **Use Case:** This is the **default and most commonly used** integer type in Java for general-purpose whole numbers unless a larger range is explicitly required.

> **The default value of int in Java is 0 when it is declared as a class variable.**

### 4. `long`

- **Size &amp; Range: 64-bit signed integer**, offering a massive range from roughly **-9 x 10^{18} to 9 x 10^{18}.**
- **Use Case:** Used when a wider range than `int` is needed (such as handling timestamps or large IDs). Literal values assigned to a `long` usually require an `L` or `l` suffix at the end (e.g., `15000000L`).

### 5. `float`

- **Size &amp; Precision:** 32-bit single-precision floating-point number, offering about 6 to 7 decimal digits of precision.
- **Use Case:** Used for saving memory in large arrays of floating-point numbers. Like in C++, decimal literals default to `double`, so you must append an `f` or `F` suffix to `float` literals (e.g., `5.75f`).

### 6. `double`

- **Size &amp; Precision:** 64-bit double-precision floating-point number, offering about 15 to 16 decimal digits of precision.
- **Use Case:** This is the **default choice for decimal numbers** in Java due to its high precision and modern hardware optimization.

### 7. `char`

- **Size &amp; Range:** 16-bit unsigned Unicode character, ranging from `\u0000` (0) to `\uffff` (65,535).
- **Use Case:** Used to store a single character, which must be enclosed in single quotes (e.g., `'A'`, `'$'`, or `'9'`). Because Java uses Unicode, it can store characters from almost any global language.

### 8. `boolean`

- **Size:** Not precisely defined by JVM specifications, but conceptually represents 1 bit of information.
- **Use Case:** Represents true/false conditions and can only hold two possible values: `true` or `false`. It is heavily used in control flow statements like `if`, `while`, and `for`.

## **2. Non-Primitive (Reference) Data Types**

Non-primitive data types store references (memory addresses) rather than actual values. They are created by users and include types like String, Class, Object, Interface, and Array.

### 1. Strings (`String`)

- **What it is:** A sequence of characters representing text (e.g., `"Hello, World!"`).
- **Key Detail:** In Java, `String` is a built-in class, not a primitive. Strings are **immutable**, meaning once a `String` object is created, its value cannot be changed. Any modification creates a brand-new string object in memory.

### 2. Arrays (`[]`)

- **What it is:** A fixed-size container structure that holds a collection of values of the *same* data type (e.g., `int[] numbers = {1, 2, 3, 4, 5};`).
- **Key Detail:** Arrays are treated as objects in Java. Once an array is created, its length is fixed and cannot be changed dynamically. They use zero-based indexing to access elements.

### 3. Classes and Objects (`class`)

- **What it is:** A user-defined blueprint (`class`) from which individual instances (`objects`) are created.
- **Key Detail:** A class bundles together variables (state) and methods (behavior). When you instantiate a class using the `new` keyword (e.g., `Car myCar = new Car();`), you are creating a non-primitive reference variable that points to that object in memory.

### 4. Interfaces (`interface`)

- **What it is:** A reference type similar to a class that can contain only constants, method signatures, default methods, and static methods.
- **Key Detail:** Interfaces cannot be instantiated directly. Instead, classes **implement** interfaces to establish a contract defining what methods the class must have, enabling a form of multiple inheritance of behavior.

### 5. Enums (`enum`)

- **What it is:** A special data type used to define collections of fixed, predefined constants (e.g., days of the week like `MONDAY`, `TUESDAY`, or compass directions).
- **Key Detail:** Enums make code more readable and type-safe compared to using plain integer or string constants, and they can contain fields, constructors, and methods just like regular classes.

# **Java Operators**

---

Java operators are symbols used to perform operations on variables and values. They play a key role in expressions, calculations, and decision-making in programs. Operators help simplify complex logic into concise statements.

### 1. Basic Arithmetic Operators

These operators perform standard mathematical calculations on operands, behaving just like they do in C++:

- **Addition (**`+`**):** Adds two operands together. For example, `10 + 3` evaluates to `13`.
- **Subtraction (**`-`**):** Subtracts the right operand from the left operand. For example, `10 - 3` evaluates to `7`.
- **Multiplication (**`*`**):** Multiplies two operands. For example, `10 * 3` evaluates to `30`.
- **Division (**`/`**):** Divides the left operand by the right operand. When dividing two integers, Java performs integer division, meaning any fractional remainder is dropped entirely. For example, `10 / 3` results in `3`, not `3.33`. To get a decimal result, at least one operand must be a floating-point type (e.g., `10.0 / 3`).
- **Modulus (**`%`**):** Returns the remainder of a division operation. For example, `10 % 3` evaluates to `1` because 3 goes into 10 three times with a remainder of 1.

### 2. Unary Operators

Unary operators operate on a single operand to modify its value or sign:

- **Unary Plus (**`+`**):** Explicitly indicates a positive value, though it is rarely used because numbers are positive by default.
- **Unary Minus (**`-`**):** Negates an expression or value, turning a positive number negative or vice versa.
- **Increment (**`++`**):** Increases the value of a variable by 1. It can be used as a prefix (`++a`, which increments the value *before* using it in an expression) or a postfix (`a++`, which uses the current value *first* and increments it afterward).
- **Decrement (**`--`**):** Decreases the value of a variable by 1. Like increment, it supports both prefix (`--a`) and postfix (`a--`) behavior.

### 3. Compound Assignment Operators

Java provides shorthand operators that combine an arithmetic operation with a variable assignment:

- **Add and Assign (**`+=`**):** Adds the right-hand value to the left-hand variable and assigns the result back to the variable (e.g., `a += 3` is shorthand for `a = a + 3`).
- **Subtract and Assign (**`-=`**):** Subtracts the right-hand value from the left-hand variable (e.g., `a -= 2` is shorthand for `a = a - 2`).
- **Multiply and Assign (**`*=`**):** Multiplies the variable by the right-hand value (e.g., `a *= 4` is shorthand for `a = a * 4`).
- **Divide and Assign (**`/=`**):** Divides the variable by the right-hand value (e.g., `a /= 2` is shorthand for `a = a / 2`).
- **Modulus and Assign (**`%sin` **or** `%=`**):** Assigns the remainder of division to the variable (e.g., `a %= 3` is shorthand for `a = a % 3`).

### **4. Relational Operators**

[**Relational Operators**](https://www.geeksforgeeks.org/java/java-relational-operators-with-examples/) are used to check for relations like equality, greater than, and less than. They return boolean results after the comparison and are extensively used in looping statements as well as conditional if-else statements.    
**1. Equal To (**`==`**)**

- **What it does:** Checks if two operands are equal to each other. If they are equal, it evaluates to `true`; otherwise, it evaluates to `false`.
- **Example:** `int a = 5; int b = 5; boolean result = (a == b);` evaluates to `true`.
- **C++ Comparison:** Works the same way for primitive types in both languages.

**2. Not Equal To (**`!=`**)**

- **What it does:** Checks if two operands are *not* equal to each other. If they are different, it evaluates to `true`; if they are identical, it evaluates to `false`.
- **Example:** `int a = 5; int b = 3; boolean result = (a != b);` evaluates to `true`.

**3. Greater Than (**`>`**)**

- **What it does:** Checks if the left operand is strictly greater than the right operand.
- **Example:** `10 > 5` evaluates to `true`, but `5 > 5` evaluates to `false`.

**4. Less Than (**`<`**)**

- **What it does:** Checks if the left operand is strictly less than the right operand.
- **Example:** `3 < 7` evaluates to `true`.

**5. Greater Than or Equal To (**`>=`**)**

- **What it does:** Checks if the left operand is greater than or equal to the right operand.
- **Example:** `5 >= 5` evaluates to `true` because the values are equal.

**6. Less Than or Equal To (**`<=`**)**

- **What it does:** Checks if the left operand is less than or equal to the right operand.
- **Example:** `4 <= 8` evaluates to `true`.

### **5. Logical Operators**

[**Logical Operators**](https://www.geeksforgeeks.org/java/java-logical-operators-with-examples/) are used to perform "logical AND" and "logical OR" operations, similar to AND gate and OR gate in digital electronics. They have a short-circuiting effect, meaning the second condition is not evaluated if the first is false.

- Boolean variables x and y are used to perform logical operations.
- &amp;&amp; (AND) returns true only if both conditions are true.
- || (OR) returns true if at least one condition is true.
- ! (NOT) reverses the boolean value.

### 6. The Ternary Operator (`? :`)

The ternary operator is a shorthand inline alternative to an `if-else` statement. It evaluates a boolean condition and returns one of two values depending on whether the condition is true or false.

- **Syntax:** `condition ? valueIfTrue : valueIfFalse;`

```java
int score = 85;
String result = (score >= 50) ? "Pass" : "Fail"; 
// result will be "Pass"
```

### 7. Bitwise Operators

Bitwise operators perform operations directly on the individual binary bits of integer types (`int`, `long`, `short`, `char`, `byte`).

- **Bitwise AND (**`&`**):** Compares corresponding bits of two numbers. If both bits are `1`, the resulting bit is `1`; otherwise, it is `0`. *(Note: When used with booleans instead of numbers,* `&` *acts as a logical AND that **does not** short-circuit).*
- **Bitwise OR (**`|`**):** Sets a bit to `1` if at least one of the corresponding bits is `1`. *(With booleans,* `|` *acts as a non-short-circuiting logical OR).*
- **Bitwise XOR (**`^`**):** Stands for "Exclusive OR". Sets a bit to `1` if only one of the corresponding bits is `1` (if both are `1` or both are `0`, it results in `0`).
- **Bitwise Complement (**`~`**):** A unary operator that flips all the bits of a number (turning `0`s to `1`s and `1`s to `0`s).
- **Left Shift (**`<<`**):** Shifts the bits of the left operand to the left by the number of positions specified by the right operand, effectively multiplying the number by powers of 2.
- **Signed Right Shift (**`>>`**):** Shifts bits to the right, preserving the sign bit (positive/negative), effectively dividing by powers of 2.
- **Unsigned Right Shift (**`>>>`**):** A Java-specific operator that shifts bits to the right, always filling the vacant higher-order bits with `0`s regardless of whether the original number was positive or negative.

### 8. The `instanceof` Operator

The `instanceof` operator is a type comparison operator used exclusively with non-primitive reference types (objects and classes). It checks whether an object is an instance of a specific class, subclass, or implements a particular interface.

- **What it returns:** It evaluates to a `boolean` (`true` if the object matches the type, otherwise `false`).
- **Why it's useful:** It helps prevent runtime casting errors (`ClassCastException`) when dealing with inheritance or polymorphism.

```java
String name = "Java";
boolean check = name instanceof String; // evaluates to true
```

## Operator Precedence in Java

Here is the operator precedence and associativity in Java, organized in a clear, non-tabular format from highest precedence (evaluated first) to lowest precedence (evaluated last):

### 1. Postfix Operators (Highest Precedence)

- **Operators:** `expr++`, `expr--`
- **Associativity:** Left-to-right
- **Description:** Evaluates the expression using its current value before incrementing or decrementing it.

### 2. Unary Operators

- **Operators:** `++expr`, `--expr`, `+expr`, `-expr`, `~`, `!`
- **Associativity:** Right-to-left
- **Description:** Includes prefix increment/decrement, unary plus and minus, bitwise complement (`~`), and logical NOT (`!`).

### 3. Creation and Type Casting

- **Operators:** `new`, `(type)value`
- **Associativity:** Right-to-left
- **Description:** Used for instantiating new objects with `new` or explicitly casting a value to another data type.

### 4. Multiplicative Operators

- **Operators:** `*`, `/`, `%`
- **Associativity:** Left-to-right
- **Description:** Standard multiplication, division, and modulus operations.

### 5. Additive Operators

- **Operators:** `+`, `-`
- **Associativity:** Left-to-right
- **Description:** Standard addition and subtraction (along with string concatenation for `+`).

### 6. Shift Operators

- **Operators:** `<<`, `>>`, `>>>`
- **Associativity:** Left-to-right
- **Description:** Bitwise left shift, signed right shift, and unsigned right shift.

### 7. Relational Operators

- **Operators:** `<`, `>`, `<=`, `>=`, `instanceof`
- **Associativity:** Left-to-right
- **Description:** Used for numeric comparisons and checking object types.

### 8. Equality Operators

- **Operators:** `==`, `!=`
- **Associativity:** Left-to-right
- **Description:** Checks if operands are equal or not equal.

### 9. Bitwise AND

- **Operator:** `&`
- **Associativity:** Left-to-right
- **Description:** Performs a bitwise AND operation on numeric bits (or non-short-circuiting logical AND on booleans).

### 10. Bitwise Exclusive OR (XOR)

- **Operator:** `^`
- **Associativity:** Left-to-right
- **Description:** Performs a bitwise XOR operation.

### 11. Bitwise Inclusive OR

- **Operator:** `|`
- **Associativity:** Left-to-right
- **Description:** Performs a bitwise OR operation (or non-short-circuiting logical OR on booleans).

### 12. Logical AND

- **Operator:** `&&`
- **Associativity:** Left-to-right
- **Description:** Logical AND with short-circuit evaluation.

### 13. Logical OR

- **Operator:** `||`
- **Associativity:** Left-to-right
- **Description:** Logical OR with short-circuit evaluation.

### 14. Ternary Operator

- **Operator:** `? :`
- **Associativity:** Right-to-left
- **Description:** Inline conditional shorthand for `if-else` statements.

### 15. Assignment Operators (Lowest Precedence)

- **Operators:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`, etc.
- **Associativity:** Right-to-left
- **Description:** Assigns values or performs compound arithmetic assignments. Because they evaluate right-to-left, chained assignments like `a = b = 5;` work correctly.

# **Java - Conditional Statements**

---

### **Java if-else-if ladder**

The if-else-if ladder allows multiple independent conditions to be checked in order. As soon as one condition is true, its block executes, and the rest are skipped.

```java
import java.util.*;

class Geeks {
    public static void main(String args[])
    {
        int i = 20;

        if (i == 10)
            System.out.println("i is 10");
        else if (i == 15)
            System.out.println("i is 15");
        else if (i == 20)
            System.out.println("i is 20");
        else
            System.out.println("i is not present");
    }
}
```

### **Java Switch Case**

The [**switch**](https://www.geeksforgeeks.org/java/switch-statement-in-java/) statement is a multiway branch statement. It provides an easy way to dispatch execution to different parts of code based on the value of the expression. 

```java

import java.io.*;

class Geeks {
    public static void main(String[] args)
    {
        int num = 20;
        switch (num) {
        case 5:
            System.out.println("It is 5");
            break;
        case 10:
            System.out.println("It is 10");
            break;
        case 15:
            System.out.println("It is 15");
            break;
        case 20:
            System.out.println("It is 20");
            break;
        default:
            System.out.println("Not present");
        }
    }
}
```

- The expression inside the switch statement is evaluated.
- The value of the expression is compared with each case label.
- If a matching case is found, the statements associated with that case are executed.
- The break statement terminates the switch block and transfers control outside the switch.
- If break is omitted, execution continues to the next case statements (fall-through).
- If no case matches the expression value, the default block is executed (if present).
- After the switch statement finishes execution, control moves to the next statement in the program.
