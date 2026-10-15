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

- Write code in a file like [HelloWorld.java](http://HelloWorld.java).
- Java Compiler "javac" compiles it into bytecode "HelloWorld.class".
- [**JVM**](https://www.geeksforgeeks.org/java/differences-jdk-jre-jvm/) (Java Virtual Machine) reads the .class file and interprets the bytecode.
- The JVM initially interprets bytecode and uses JIT (Just-In-Time) compilation to convert frequently executed code into native machine code for better performance
