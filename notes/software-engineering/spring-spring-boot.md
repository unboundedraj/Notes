---
title: Spring & Spring Boot
date: 2026-11-13
tags: [spring, springboot, java]
---

## What is Java.net?

`java.net` is a built-in Java package that provides foundational classes and interfaces for network communication.

**Key Components:**

- **Socket Programming:** `Socket` and `ServerSocket` for low-level TCP communication; `DatagramSocket` for UDP.
- **HTTP Handling:** `HttpURLConnection` and the modern `java.net.http.HttpClient` (introduced in Java 11) for managing HTTP requests and responses.
- **Addressing:** `InetAddress` for handling IP addresses and DNS resolution.

**Relevance to Spring / Spring Boot:** Spring Boot handles server configuration, routing, and HTTP abstractions automatically, but its embedded servers (like Tomcat), HTTP clients (`RestTemplate`, `WebClient`), and microservice communication ultimately rely on Java's underlying networking stack (`java.net`).

## What is a Web Server vs. a Servlet Container?

- **Web Server:** Software that listens for incoming HTTP/HTTPS requests from clients (browsers) and serves static content (HTML, CSS, images). Examples: Nginx, Apache HTTP Server.
- **Servlet Container (Web Container):** A specialized runtime environment that manages the lifecycle, instantiation, and execution of **Java Servlets**. It bridges the gap between the web server and your Java application code by:
  1. Converting incoming HTTP requests into Java objects (`HttpServletRequest`, `HttpServletResponse`).
  2. Invoking the appropriate servlet methods (`doGet`, `doPost`).
  3. Translating the Java response back into an HTTP response for the client.
  - *Examples:* Apache Tomcat, Jetty, Undertow.

**Relevance to Spring / Spring Boot:** Spring Boot applications run on an embedded servlet container (Tomcat by default) packaged directly inside the executable JAR file. This eliminates the need to manually install, configure, and deploy WAR files to an external standalone application server.

## What is Spring ecosystem?

The **Spring Ecosystem** is a comprehensive, modular framework ecosystem for building enterprise-grade Java applications. Originally created to simplify complex enterprise Java (J2EE) development through Dependency Injection (DI) and Inversion of Control (IoC), it has evolved into a vast collection of tools handling everything from web development and security to batch processing, cloud microservices, and AI integration.

**Key Pillars &amp; Modules:**

- **Spring Framework:** The foundational core providing IoC, Dependency Injection, transaction management, and the MVC web framework.
- **Spring Boot:** An opinionated extension that auto-configures Spring applications, bundles embedded servers (Tomcat), and eliminates boilerplate XML configuration to get apps running instantly.
- **Spring Data:** Simplifies database access across relational (JPA/Hibernate, JDBC) and non-relational (MongoDB, Redis) databases.
- **Spring Security:** Robust, customizable authentication and authorization framework for securing web apps and APIs.
- **Spring Cloud:** Tools for building distributed systems and microservice architectures (service discovery, API gateways, config management).
- **Spring Batch / AI:** Specialized modules for high-volume batch data processing and integrating AI/LLM capabilities.

**Core Philosophy:** Convention over configuration, modularity, and replacing cumbersome boilerplate code with clean, annotation-driven Java code.
