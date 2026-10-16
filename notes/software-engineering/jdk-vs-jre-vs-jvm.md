---
title: JDK vs JRE vs JVM
date: 2026-10-16
tags: [Java, Jvm, Jre, Jdk]
---

## **JDK (Java Development Kit)**

The [**Java Development Kit**](https://www.geeksforgeeks.org/java/jdk-in-java/) (JDK) is a software development kit used to develop Java applications. It provides the Java compiler and other tools required to write, compile, test, package, document, and debug Java programs.

- Includes compiler (javac), debugger, and utilities like jar and javadoc.
- Includes the runtime components needed to execute Java applications in addition to development tools.

### **Key Components of JDK**

- **javac:** Compiles Java source code (.java) into bytecode (.class).
- **java:** Launches Java applications using the JVM.
- **jdb:** Helps debug Java applications.
- **jar:** Packages Java classes and resources into JAR files.
- **javadoc:** Generates documentation from Java source code.

## **JRE (Java Runtime Environment)**

The [**Java Runtime Environment**](https://www.geeksforgeeks.org/java/jre-in-java/) (JRE) traditionally refers to the components required to run a Java application. It consists primarily of the JVM and the Java runtime libraries.

### **Key Components of JRE:**

- **JVM:** Executes Java bytecode.
- **Core Libraries:** Provide built-in classes for strings, collections, input/output, and other operations.
- **Supporting Runtime Files:** Provide resources and components required to run Java applications.

## **JVM (Java Virtual Machine)**

The [**Java Virtual Machine**](https://www.geeksforgeeks.org/java/how-jvm-works-jvm-architecture/) (JVM) is the runtime engine that executes Java bytecode. When Java source code is compiled, the compiler generates bytecode in .class files. The JVM loads this bytecode and executes it on the underlying operating system and hardware.

### **Main Responsibilities of JVM:**

- **Class Loading:** Loads required Java classes into memory.
- **Bytecode Verification:** Checks bytecode for structural and type-safety requirements.
- **Execution:** Interprets bytecode or compiles frequently executed code into native instructions using the Just-In-Time (JIT) compiler.
- **Memory Management:** Manages runtime memory and performs garbage collection.
- **Exception Handling:** Supports exception handling during program execution.

**Example:** The same compiled Java bytecode can execute on Windows, Linux, and macOS using a compatible JVM for each platform.
