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

>  **# is used to write [Python Comments](https://www.geeksforgeeks.org/python/python-comments/). Comments are ignored during execution.**

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

# Python Data Structures

---

## **Python String**

Strings are sequence of characters written inside quotes. It can include letters, numbers, symbols and spaces. Python does not have a separate character type.

- A single character is treated as a string of length one.
- Strings are commonly used for text handling and manipulation.

## **Accessing Characters in String**

Strings are indexed sequences. Positive indices start at 0 from the left, negative indices start at -1 from the right

## **String Slicing**

[**Slicing**](https://www.geeksforgeeks.org/python/string-slicing-in-python/) is a way to extract a portion of a string by specifying the start and end indexes. The syntax for slicing is string\[start:end\], where start starting index and end is stopping index (excluded).

```
s = "ABCDEF"
print(s[1:4])    
print(s[:3])     
print(s[3:])    
print(s[::-1])

#OUTPUT
BCD
ABC
DEF
FEDCBA
```

## **String Immutability**

Strings are immutable, meaning their values cannot be changed after creation. Any modification to a string creates a new string instead of altering the original one.

## **Deleting a String**

Individual characters of a string cannot be deleted because strings are immutable. However, an entire string variable can be removed using [**del**](https://www.geeksforgeeks.org/python/python-del-to-delete-objects/) keyword.

```
s = "ABC"
del s
```

## **Updating a String**

Strings cannot be changed directly after creation. So any modification results in a new string being created using slicing or methods like [**replace()**](https://www.geeksforgeeks.org/python/python-string-replace/).

```python
s = "ABCD EF"
s1 = "H" + s[1:]                  
s2 = s.replace("ABC", "abc")  

print(s1)
print(s2)

#OUTPUT
HBCD EF
abcD EF
```

## **Common String Methods**

Python provides various built-in methods to manipulate strings. Below are some of the most useful methods:

1.  **len():** returns the total number of characters in a string (including spaces and punctuation).

```
s = "GeeksforGeeks"
print(len(s))
#OUTPUT
13
```

2.  **upper() and lower():** [**upper()**](https://www.geeksforgeeks.org/python/python-string-upper/) method converts all characters to uppercase whereas, [**lower()**](https://www.geeksforgeeks.org/python/python-string-lower/) method converts all characters to lowercase.

```
s = "Hello World"
print(s.upper())
print(s.lower())

#OUTPUT
HELLO WORLD
hello world

```

3.  **strip() and replace():** [**strip()**](https://www.geeksforgeeks.org/python/python-string-strip/) removes leading and trailing whitespace from the string and [**replace()**](https://www.geeksforgeeks.org/python/python-string-replace/) replaces all occurrences of a specified substring with another.

```
s = "   ABC   "
print(s.strip())    

s = "Python is fun"
print(s.replace("fun", "awesome"))

#OUTPUT
ABC
Python is awesome
```

4.  **Concatenation:** Strings can be combined by using + operator.

```
s1 = "Hello"
s2 = "World"
print(s1 + " " + s2)
```

5.  **Repetition:** A string can be repeated multiple times using \*.

```
s = "Hello "
print(s * 3)
```

6. **Using f-strings:** [**f-strings**](https://www.geeksforgeeks.org/python/formatted-string-literals-f-strings-python/) allows to directly insert variables and expressions inside a string using {} brackets.

```
name = "Jake"
age = 22
print(f"Name: {name}, Age: {age}")
```

7. [**in**](https://www.geeksforgeeks.org/python/python-in-keyword/) keyword is used to check whether a substring exists inside a string. It returns True if the substring is found, otherwise it returns False.

```
s = "GeeksforGeeks"
print("Geeks" in s)
print("GfG" in s)
```

8.  **Count()** Returns the number of times a substring appears in the string.

```
text = "apple apple mango"
print(text.count("apple"))
#output
2
```
