---
title: Computer Engineer's Guide
date: 2026-10-29
tags: [GK]
pinned: true
---

## Difference between Data and Information

**Data** refers to raw, unprocessed facts and figures that have no meaning on their own. It can be numbers, words, measurements, or symbols that have not yet been organized or analyzed.

- Example: 25, 37, 19, 42 (just numbers with no context)

**Information** is data that has been processed, organized, and given context, making it meaningful and useful for decision-making.

- Example: "The average score of students in Class 10 is 30.75" (data arranged and interpreted)

## What is the internet?

The Internet is a worldwide network that connects computers, mobile phones, servers, and other devices so they can share information with each other.

## What is DNS?

DNS stands for **Domain Name System**. It is like the phonebook of the internet. It translates website names that humans can easily remember into IP addresses that computers use to find servers.

## What is IP address

An IP address (Internet Protocol address) is a numerical address assigned to a device or network interface so it can be identified and communicate over an IP network.

## Difference between Authentication and Authorization

#### [**1. Authentication (AuthN)**](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-1-authentication-authn)

Authentication is the process of verifying *who* is trying to access a system. It ensures that the entity (a user, device, or system) is who they claim to be.

- **How it works:** The user provides a form of identification and proof.
- **Common Factors:**
  - *Something you know:* Passwords, PINs, security questions.
  - *Something you have:* Smartphones (for OTPs/push notifications), hardware security keys (FIDO2/WebAuthn).
  - [*Something you are:* Fingerprints, facial recognition, iris scans\*\*.\*\*](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-something-you-are-fingerprints-facial-recognition-iris-scans)

#### [**2. Authorization (AuthZ)**](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-2-authorization-authz)

Authorization is the process of deciding *what* an authenticated user is permitted to do. Even if a system knows your exact identity, it must check whether you have the necessary clearance to view a file, edit a database, or execute a command.

- **How it works:** The system checks the user's roles, groups, or permissions against the requested resource.
- **Common Models:**
  - **RBAC (Role-Based Access Control):** Permissions are assigned to roles (e.g., "Manager", "Employee"), and users are assigned to those roles.
  - **ABAC (Attribute-Based Access Control):** Access is granted based on attributes like user location, time of day, and security clearance level.

## What are the stages a source code file goes through from compilation to execution?

The Steps in That Pipeline:

1. **Preprocessing:** The preprocessor strips comments and processes directives (like `#include` in C++), inserting header contents and expanding macros.
2. **Compilation:** The compiler translates the high-level source code into intermediate assembly code tailored to the target CPU architecture.
3. **Assembly:** The assembler converts the assembly code into machine-readable binary code, producing an object file (`.o` or `.obj`).
4. **Linking:** The linker combines all compiled object files with external libraries (like the standard library) to resolve references and create a single, unified executable file.
5. **Loading:** The operating system's loader reads the executable file from disk, allocates virtual memory in RAM, sets up the call stack and heap, and hands control over to the CPU to start execution.

## What is client server architecture?

**Client-server architecture** is a computing model in which tasks and workloads are distributed between the service providers (**servers**) and service requesters (**clients**).

In this structure, the **client** (such as a web browser, mobile app, or desktop software) initiates a request for data or functionality, and the **server** (a powerful remote computer, database, or application host) processes that request and sends back the appropriate response.

## **What is Call Stack?**

The **call stack** is a special region of computer memory that manages function execution in a program using a Last-In, First-Out (LIFO) structure. Whenever a function is called, a new block of memory called a **stack frame** (or activation record) is pushed onto the stack to store its parameters, local variables, and return address. Once the function finishes executing, its frame is automatically popped off, returning control and restoring the execution context of the calling function.

## What is the MVC Architecture?

**MVC (Model-View-Controller)** is a software design pattern that splits an application into three connected parts, so that data, UI, and logic are kept separate. This makes code easier to organize, test, and maintain.

### The three parts

**1. Model**  
Manages the application’s **data and business logic**. It talks to the database, validates data, and defines rules. It knows nothing about how data is displayed.

**2. View**  
The **user interface**: what the user sees (HTML, templates, screens). It displays data from the model and sends user actions to the controller.

**3. Controller**  
The **middleman**. It receives user input, decides what to do, asks the model to fetch or update data, and chooses which view to show.

### Flow

```
User → Controller → Model
          ↓           ↓
        View  ←───────┘
          ↓
        User sees result
```

1. User interacts (clicks, submits a form)
2. **Controller** handles the request
3. **Model** is read or updated
4. **View** is refreshed with the new data and shown to the user

### Example: web app (e.g., Spring Boot, Django, Rails)

- **Model**: `User` class + database logic
- **View**: HTML/Thymeleaf page showing the user profile
- **Controller**: `UserController` that handles `GET /users/1`, fetches the user from the model, and returns the profile view

### Advantages

- **Separation of concerns**: UI, logic, and data are independent
- **Reusability**: one model can power multiple views
- **Easier testing**: each layer can be tested on its own
- **Parallel development**: frontend and backend teams can work separately

### Disadvantages

- Can become complex for small apps
- In client-side apps, bidirectional updates between views and models can get tangled (the issue Flux solved)

## What is Graphical User Interface (GUI)?

A **Graphical User Interface (GUI)** is a type of user interface that allows people to interact with electronic devices such as computers, smartphones, and smart appliances through visual elements rather than text-based commands.  
Key Characteristics of a GUI

- **Visual Interaction:** Actions are performed directly by clicking, tapping, dragging, or swiping rather than memorizing and typing syntax.
- **The WIMP Paradigm:** Most modern GUIs are built around **W**indows, **I**cons, **M**enus, and **P**ointer architecture.
- **Multitasking:** GUIs make it easy to run, view, and switch between multiple applications simultaneously using overlapping windows.

## What is Command Line Interface (CLI)?

A **Command Line Interface (CLI)** is a text-based user interface used to interact with operating systems, software, and servers. Instead of clicking on visual icons, windows, or buttons with a mouse, users type explicit text commands and press Enter to execute them.  
Key Advantages of a CLI  
While GUIs are more intuitive for everyday consumers, CLIs are indispensable for developers, system administrators, and power users due to several distinct advantages:

- **Speed and Efficiency:** Once you learn the commands, performing complex operations via keyboard is often significantly faster than navigating deep menus and clicking through graphical dialogs.
- **Automation and Scripting:** Commands can be easily chained together into shell scripts or configuration files to automate repetitive workflows, testing, deployments, and backups.
- **Resource Efficiency:** Text interfaces consume minimal memory and processing power. This makes them ideal for running on lightweight servers or embedded systems where a graphical desktop environment would be a waste of resources.
- **Remote Management:** CLIs can be run efficiently over low-bandwidth network connections (such as via SSH), making it practical to manage cloud servers located anywhere in the world.

### Common Examples of CLIs

- **Bash / Zsh:** The default shells for Linux distributions and macOS.
- **PowerShell / Command Prompt:** The standard command-line environments for Windows.
- **Developer Tools:** Specialized CLIs like Git, Docker, and the AWS CLI used for building, containerizing, and managing cloud infrastructure.
