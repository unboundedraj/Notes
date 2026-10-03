---
title: Authentication vs Authorization
date: 2026-10-03
tags: [GK]
---

#### 1. Authentication (AuthN)

Authentication is the process of verifying *who* is trying to access a system. It ensures that the entity (a user, device, or system) is who they claim to be.

- **How it works:** The user provides a form of identification and proof.
- **Common Factors:**
  - *Something you know:* Passwords, PINs, security questions.
  - *Something you have:* Smartphones (for OTPs/push notifications), hardware security keys (FIDO2/WebAuthn).
  - *Something you are:* Fingerprints, facial recognition, iris scans.
    ---

#### 2. Authorization (AuthZ)

Authorization is the process of deciding *what* an authenticated user is permitted to do. Even if a system knows your exact identity, it must check whether you have the necessary clearance to view a file, edit a database, or execute a command.

- **How it works:** The system checks the user's roles, groups, or permissions against the requested resource.
- **Common Models:**
  - **RBAC (Role-Based Access Control):** Permissions are assigned to roles (e.g., "Manager", "Employee"), and users are assigned to those roles.
  - **ABAC (Attribute-Based Access Control):** Access is granted based on attributes like user location, time of day, and security clearance level.
