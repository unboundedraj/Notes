---
title: Computer Engineer's Guide
date: 2026-10-29
tags: [GK]
---

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
  - [*Something you are:* Fingerprints, facial recognition, iris scans**.**](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-something-you-are-fingerprints-facial-recognition-iris-scans)

#### [**2. Authorization (AuthZ)**](https://cortex-psi-rose.vercel.app/notes/software-engineering/authentication-vs-authorization#h-2-authorization-authz)

Authorization is the process of deciding *what* an authenticated user is permitted to do. Even if a system knows your exact identity, it must check whether you have the necessary clearance to view a file, edit a database, or execute a command.

- **How it works:** The system checks the user's roles, groups, or permissions against the requested resource.
- **Common Models:**
  - **RBAC (Role-Based Access Control):** Permissions are assigned to roles (e.g., "Manager", "Employee"), and users are assigned to those roles.
  - **ABAC (Attribute-Based Access Control):** Access is granted based on attributes like user location, time of day, and security clearance level.
