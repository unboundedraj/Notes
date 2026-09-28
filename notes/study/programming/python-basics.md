---
title: Python Basics
date: 2026-09-05
tags: [python, programming, study]
pinned: false
---

## Variables and Data Types

Python is dynamically typed, meaning you don't declare variable types explicitly. The type is inferred at runtime.

```python
name = "Alice"
age = 30
gpa = 3.85
is_student = True

print(f"Name: {name}, Age: {age}")
```

Common data types include `str` (string), `int` (integer), `float` (floating-point), `bool` (boolean), `list`, `tuple`, and `dict` (dictionary).

## Control Flow

Conditionals and loops are the building blocks of control flow:

```python
# If-else
if age >= 18:
    print("Adult")
else:
    print("Minor")

# For loop
for i in range(5):
    print(i)

# While loop
count = 0
while count < 3:
    print(count)
    count += 1
```

## Functions

Functions encapsulate reusable logic. Use `def` to define a function:

```python
def greet(name):
    return f"Hello, {name}!"

result = greet("Bob")
print(result)
```

Functions can have default parameters, `*args`, and `**kwargs` for flexibility.

## Lists and Dictionaries

Lists are ordered, mutable sequences. Dictionaries are key-value stores.

```python
fruits = ["apple", "banana", "cherry"]
person = {"name": "Charlie", "age": 25, "city": "NYC"}

print(fruits[0])  # "apple"
print(person["name"])  # "Charlie"
```

Inline code example: use `len()` to get the length of a sequence.

## JavaScript Quick Reference

For comparison, here's how you'd do something similar in JavaScript:

```javascript
const name = "Alice";
const age = 30;
const isStudent = true;

console.log(`Name: ${name}, Age: ${age}`);
```

## Bash Example

And in Bash, for scripting context:

```bash
#!/bin/bash
name="Alice"
age=30

echo "Name: $name, Age: $age"
```

## Next Steps

- Practice writing small scripts to manipulate lists and dictionaries
- Learn about list comprehensions for more concise code
- Explore the `import` system and commonly used libraries like `requests`, `numpy`, and `pandas`
