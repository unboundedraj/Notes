---
title: System Design
date: 2026-11-04
tags: [system design]
---

# **What is System Design?**

System design is the process of defining the architecture, components, modules, and data flow of a system to satisfy a set of requirements. It covers how different parts of an application talk to each other, how data moves through the system, and how the whole thing holds up under load. Engineers use it to plan systems before writing code, balancing trade-offs like cost, performance, and reliability.

## **How to approach System Design?**

Approaching a system design problem starts with clarifying requirements: what the system needs to do, how many users it serves, and what scale it must handle. From there, the design moves through estimating capacity, sketching a high-level architecture, and drilling into individual components like databases, caches, and load balancers. Trade-offs get revisited throughout, since no design fits every constraint at once.

## **Latency vs Throughput**

Latency is the time it takes to complete a single operation, such as the time between a request and its response. Throughput is the number of operations a system can process in a given time period. The two are related but not interchangeable: a system can have low latency but limited throughput, or high throughput with noticeable latency per request.

## **Availability vs Consistency**

In a distributed system, availability and consistency often pull in opposite directions when a network partition happens. A system can either keep serving requests using potentially stale data, favoring availability, or refuse to respond until all nodes agree, favoring consistency. Which one a system prioritizes depends on the use case.

### **CAP Theorem**

The CAP theorem states that a distributed system can only guarantee two out of three properties at the same time: consistency, availability, and partition tolerance. Since network partitions are unavoidable in real systems, the practical choice comes down to consistency versus availability during a partition. Designers use CAP as a framework to reason about these trade-offs rather than as a strict rule for every scenario.

## **Consistency Patterns**

Consistency patterns describe how a distributed system keeps multiple copies of the same data in sync across nodes. Different patterns trade off how quickly all replicas reflect a write against how available the system stays during network issues. The common patterns are weak, eventual, and strong consistency, each suited to different types of applications.

### **Weak Consistency**

Weak consistency means that after a write, reads are not guaranteed to see that write immediately, or at all. This model works for use cases where occasional data loss or staleness is acceptable, such as real-time voice or video calls, where getting the latest packet matters more than getting every packet.

### **Strong Consistency**

After an update is made to the data, it will be immediately visible to any subsequent read operations. The data is replicated in a synchronous manner, ensuring that all copies of the data are updated at the same time.

### **Eventual Consistency**

Eventual consistency guarantees that, given enough time without new writes, all replicas of the data will converge to the same value. Reads immediately after a write might return stale data, but the system resolves this over time. DNS and systems like Cassandra rely on this model to stay highly available.
