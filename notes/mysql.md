---
title: MySQL
date: 2026-11-11
tags: [sql, mysql]
---

## What is MySQL?

**MySQL** is an open-source **relational database management system (RDBMS)** that stores data in tables and uses **SQL** (Structured Query Language) to create, query, and manage it. It was created in 1995 by the Swedish company MySQL AB, later acquired by Sun Microsystems, and is now owned by **Oracle**.  
**Key characteristics**

- **Client-server architecture:** the MySQL server runs as a process, and applications, command-line tools, or GUIs (MySQL Workbench) connect to it over a network.
- **Pluggable storage engines:** **InnoDB** (the default) supports ACID transactions, row-level locking, foreign keys, and MVCC. **MyISAM** is an older engine with no transactions. Others include MEMORY and ARCHIVE.
- **Cross-platform:** runs on Linux, Windows, and macOS.
- **Fast and lightweight:** well suited to read-heavy web workloads.
- **Replication and scaling:** supports leader-follower replication, clustering, and partitioning.
- **Wide ecosystem:** connectors for Java (JDBC), Python, Node.js, PHP, and more, so it works with frameworks like Spring Boot.

## What is Structured Query Language?

Introduction to Structured Query Language (SQL)

1. SQL stands for Structured Query Language.
2. It is the language of databases and almost all companies use databases to store their data.
3. SQL makes use of query. A Query is a set of instruction given to the database management system. It tells any database what information we would like to get from the database.
4. SQL is case- insensitive. However it has become standard in SQL community to use all capital letters for SQL keywords.
5. SQL is a standard language for Relational Database Management System (RDBMS).  
There are various RDBMS software that are popularly used. It includes MySQL, Oracle, MS ACCESS, Microsoft SQL Server, Sybase and so on.
6. Query is a statement used for requesting the retrieval of information. This retrieval of information using some specific language is called query language.

> SQL statements fall into the categories you saw earlier:
>
>
> | Category                            | Purpose          | Commands                               |
> | ----------------------------------- | ---------------- | -------------------------------------- |
> | DDL<br>Data definition Language     | Define structure | `CREATE`, `ALTER`, `DROP`              |
> | DML<br>Data Manipulation Language   | Work with data   | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
> | DCL<br>Data Control Language        | Permissions      | `GRANT`, `REVOKE`                      |
> | TCL<br>Transaction Control Language | Transactions     | `COMMIT`, `ROLLBACK`                   |
>
