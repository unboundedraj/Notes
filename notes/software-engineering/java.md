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

### `System.out.println("Hello World!");`

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
