---
title: Python
date: 2026-10-24
tags: [python, ".py"]
---

# Introduction

---

Python is one of the most popular programming languages. It’s simple to use, packed with features and supported by a wide range of libraries and frameworks. Its clean syntax makes it beginner-friendly.

- A high-level language used in data science, automation, AI, web development and more.
- Known for its readability, which means code is easier to write, understand and maintain.
- Backed by strong library support, we don’t have to build everything from scratch.

```python
# This is a comment. It will not be executed.
print("Hello, World!")
```

- print() is a built-in Python function that instructs the computer to display text on the screen.
- "Hello, World!" is a string enclosed within quotes (either single ' or double ").
- Python uses indentation (spaces or tabs) to define code blocks instead of braces {} in C, C++ and Java .
- # is used to write [**Python Comments**](https://www.geeksforgeeks.org/python/python-comments/). Comments are ignored during execution.

# **Input and Output in Python**

---

The print() function is used for output in various formats and the input() function enables interaction with users.

```
name = input("Enter your name: ")
print("Hello,", name, "! Welcome!")
```

> input().split() reads a single line of input and splits it into multiple values based on spaces.

# **Python Variables**

---

Variables are used to store data that can be referenced and manipulated during program execution. A variable is essentially a name that is assigned to a value.

- Unlike Java and many other languages, Python variables do not require explicit declaration of type.
- Type of the variable is inferred based on the value assigned.

```
x = 5
name = "Alex"  
print(x)
print(name)
```

## **Rules for Naming Variables**

To use variables correctly, the following naming rules should be followed:

1. Names can contain letters, digits and underscores (\_).
2. The first character cannot be a digit.
3. Names are case-sensitive, so myVar and myvar are treated differently.
4. [**Keywords**](https://www.geeksforgeeks.org/python/python-keywords/) such as if, else and for cannot be used as variable names.

## **Assigning Values to Variables**

**1. Basic Assignment:** Variables are assigned values using the = [**operator**](https://www.geeksforgeeks.org/python/python-operators/).

```
x = 5
y = 3.14
z = "Hi"
```

**2. Dynamic Typing:** Python is dynamically typed, so the same variable can store different data types during execution.

```
x = 10
x = "Now a string"
```

  
**3. Assigning Same Value:** Same value can be assigned to multiple variables in a single line.

```
a = b = c = 100
print(a, b, c)
```

**4. Assigning Different Values:** Multiple variables can also be assigned different values in a single line.

```
x, y, z = 1, 2.5, "Python"
print(x, y, z)
```

> In Python, the type() function returns the type of the specified variable. It is used to determine the data type of an object. When you pass a variable to the type() function, it returns the type of the object that the variable references.

## **Deleting a Variable**

[**del**](https://www.geeksforgeeks.org/python/python-del-to-delete-objects/) keyword is used to delete a variable from memory. After deletion, the variable can no longer be accessed.

```
x = 10
del x
print(x)
```
