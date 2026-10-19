---
title: OOPS
date: 2026-10-19
tags: [oops]
---

# Object Oriented Programming

---

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes programs around classes and objects. A class defines the data members and member functions, while an object is an instance of a class. OOP helps build modular, reusable, and maintainable software by modeling real-world entities.

- Promotes code reusability through inheritance.
- Improves code maintainability and scalability.
- Provides data security through encapsulation.
- Models real-world entities using classes and objects.

## **Class**

A **Class** is a user-defined data type that acts as a blueprint for creating objects. It defines the data members and member functions that describe the properties and behavior of the objects.

- A class is a user-defined data type.
- It contains data members and member functions.
- Multiple objects can be created from a single class.

## **Object**

An **Object** is an instance of a class that represents a real-world entity. It is used to access the data members and member functions defined in the class.

- **State:** Represents the current values of an object's data members.
- **Behavior:** Represents the actions an object can perform through its member functions.
- **Identity:** Every object has a unique memory location that distinguishes it from other objects, even if they contain the same data.

## **Constructor**

A [**constructor**](https://www.geeksforgeeks.org/cpp/constructors-c/) is a special member function of a class that is automatically called when an object is created. It is mainly used to initialize the object's data members and establish its initial state.

- A constructor has the same name as the class.
- It does not have a return type, not even void.
- It is automatically invoked whenever an object of the class is created.
- It helps initialize object properties during object creation.

### **Types of Constructor**

- **Default Constructor:** A constructor that does not accept any parameters and initializes an object with default values.
- **Parameterized Constructor:** A constructor that accepts parameters to initialize an object with specific values.
- **Copy Constructor:** A user-defined constructor that creates a new object by copying the data of another object of the same class.

## **Destructor**

A [**Destructor**](https://www.geeksforgeeks.org/cpp/destructors-c/) is a special member function that is automatically invoked when an object is destroyed. It is primarily used to release resources such as dynamically allocated memory, open files, or network connections.

- Destructor name is the same as the class name, preceded by a tilde (\~).
- A class can have only one destructor.
- It does not accept parameters and has no return type.
- It is automatically called when an object goes out of scope or is deleted.

> **Java does not have traditional destructors** like C++  
> Because Java manages memory automatically through its built-in **Garbage Collector (GC)**, you do not manually delete objects or free memory when you are done with them. The Garbage Collector automatically finds objects that are no longer reachable and reclaims their memory.

## **Access Specifiers**

[**Access specifiers**](https://www.geeksforgeeks.org/cpp/access-modifiers-in-c/) control the visibility and accessibility of class members. They help implement encapsulation by restricting access to data and member functions.

- **public:** Members can be accessed from anywhere in the program.
- **private:** Members can only be accessed within the same class.
- **protected:** Members can be accessed within the class and its derived classes.

## **Four Pillars of OOP**

The four pillars of Object-Oriented Programming (OOP) are **Encapsulation**, **Abstraction**, **Inheritance**, and **Polymorphism**

### 1. Encapsulation

Encapsulation is the practice of bundling data (variables) and methods (functions) into a single unit (a class) and restricting direct access to some of the object's components. This protects the internal state of an object from unintended modifications.

- **C++ Implementation:** Achieved using access specifiers (`private`, `protected`, `public`). Data members are typically declared `private`, and access is provided via public getter and setter member functions.
- **Java Implementation:** Similar to C++, Java uses `private`, `protected`, `public`, and default (package-private) access modifiers. Encapsulation is standard practice, paired with JavaBeans conventions (private fields with public `getXYZ()` and `setXYZ()` methods).

### 2. Abstraction

Abstraction focuses on hiding complex implementation details and exposing only the essential features of an object. It allows developers to interact with an object through a simplified interface without worrying about how it works under the hood.

### How Virtual Functions Enable Abstraction (C++ Example)

In C++, abstraction is implemented using **abstract classes** and **pure virtual functions**.

A **pure virtual function** is a virtual function initialized to zero (`= 0`). It has no body in the base class; it forces every derived class to provide its own specific implementation. Any class containing a pure virtual function becomes an **abstract class** (you cannot create an object of it directly).

```cpp
#include <iostream>
using namespace std;

// 1. Abstract Class (Defines the interface, hides implementation)
class PaymentGateway {
public:
    // Pure virtual function
    virtual void processPayment(double amount) = 0; 
    
    virtual ~PaymentGateway() {} // Virtual destructor for safety
};

// 2. Concrete Implementation 1
class CreditCardPayment : public PaymentGateway {
public:
    void processPayment(double amount) override {
        cout << "Processing ₹" << amount << " via Credit Card encryption.\n";
    }
};

// 3. Concrete Implementation 2
class UPIPayment : public PaymentGateway {
public:
    void processPayment(double amount) override {
        cout << "Processing ₹" << amount << " via UPI handle verification.\n";
    }
};

int: main() {
    // PaymentGateway pg; -> ERROR! Cannot instantiate abstract class.

    // Abstraction in action: We code against the abstract interface, 
    // without needing to know how each gateway handles payments under the hood.
    PaymentGateway* method1 = new CreditCardPayment();
    PaymentGateway* method2 = new UPIPayment();

    method1->processPayment(500.0); // Calls CreditCardPayment's version dynamically
    method2->processPayment(150.0); // Calls UPIPayment's version dynamically

    delete method1;
    delete method2;
    return 0;
}
```

- **Abstraction** hides *how* things work behind a clean interface.
- **Virtual functions** (and pure virtual functions) are the C++ mechanism that makes this possible at runtime, letting base class pointers dynamically trigger the correct derived class behavior.

### 3. Polymorphism

Polymorphism means "many forms." It allows a single interface to represent different underlying data types or behaviors. It is divided into two types:

1. **Compile-time (Static) Polymorphism:** Achieved via **Method Overloading** (functions or methods with the same name but different parameters). Both C++ and Java support this identically.
2. **Run-time (Dynamic) Polymorphism:** Achieved via **Method Overriding** (a subclass provides a specific implementation of a method already defined in its parent class).

- **C++ Implementation:** For run-time polymorphism to work, the base class method must be declared with the `virtual` keyword. C++ resolves this using virtual tables (vtables).
- **Java Implementation:** **All non-static methods are virtual by default** in Java. You do not need a `virtual` keyword; a subclass method automatically overrides a superclass method if signatures match. Java provides the `@Override` annotation for compiler safety.

### 4. Inheritance

Inheritance is one of the core pillars of Object-Oriented Programming (OOP), allowing a new class (derived or child class) to adopt the properties and behaviors of an existing class (base or parent class).

The structure in which classes inherit from one another determines the **type of inheritance**.

### 1. Single Inheritance

- **Definition:** A subclass inherits from a **single** base class. This is the simplest and most straightforward form of inheritance.
- **Example:** A class `Dog` inherits from a class `Animal`.
- **C++ &amp; Java Support:** Fully supported by both languages.

```
[ Base Class ]
      ▲
      │
[ Derived Class ]
```

### 2. Multilevel Inheritance

- **Definition:** A class is derived from another derived class, forming a "chain" or hierarchy of inheritance. The child class inherits from a parent, which in turn inherits from its own parent.
- **Example:** A class `Puppy` inherits from `Dog`, which inherits from `Animal`. Here, `Puppy` has access to features of both `Dog` and `Animal`.
- **C++ &amp; Java Support:** Fully supported by both languages.

```
[ Base Class A ]
      ▲
      │
[ Derived Class B ]
      ▲
      │
[ Derived Class C ]
```

### 3. Hierarchical Inheritance

- **Definition:** Multiple subclasses inherit from a **single** base class. It represents a one-to-many relationship, where one parent has multiple children sharing its core attributes.
- **Example:** Both `Dog` and `Cat` classes inherit from the same `Animal` base class.
- **C++ &amp; Java Support:** Fully supported by both languages.

```
[ Base Class A ]
         ▲          ▲
         │          │
[Derived Class B] [Derived Class C]
```

### 4. Multiple Inheritance

- **Definition:** A single subclass inherits from **more than one** base class. This allows the child to combine behaviors and attributes from multiple unrelated parents.
- **Example:** A `SmartPhone` class inherits from both a `Phone` class and a `Camera` class.
- **C++ &amp; Java Support:**
  - **C++:** **Fully supports** multiple inheritance directly.
  - **Java:** **Does not support** multiple inheritance for *classes* to avoid complexity and ambiguity (specifically the "Diamond Problem"). However, Java allows a class to implement **multiple interfaces**, which achieves multiple inheritance of behavior safely.

```
[Base Class A]   [Base Class B]
      ▲                ▲
      └───────┬────────┘
              │
      [ Derived Class C ]
```

## What is the Diamond problem?

The **Diamond Problem** is an ambiguity that occurs in languages supporting multiple inheritance when a class inherits from two classes that share a common base parent.

```
         [ Parent A ]
           /      \
    [ Class B ]  [ Class C ]
           \      /
         [ Class D ]
```

**The Core Issue:** `Class D` inherits two separate copies of `Parent A`'s data (causing memory waste) and faces ambiguity when trying to call a method defined in `Parent A`.

> - **C++ (Solves via Virtual Inheritance):** C++ allows multiple inheritance, so it uses **virtual inheritance** (`virtual public`) to force `Class D` to share a single, unified copy of `Parent A`.
> - **Java (Avoids It Entirely):** Java prevents the problem by **disallowing multiple inheritance for classes**. A class can only extend one parent, and multiple behaviors are achieved safely using **interfaces**.
