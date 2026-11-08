---
title: DBMS
date: 2026-11-08
tags: [dbms, mysql, rdbms]
---

## What is a Database Management System ?

Definition : A Database Management System (DBMS) is collection of interrelated data and various programs that are used to handle the data.  
The primary goal of DBMS is to provide a way to store and retrieve the required information from the database in convenient and efficient manner.  
For managing the data in the database two important tasks are conducted -

1.  Define the structure for storage of information.
2.  Provide mechanism for manipulation of information.

## What is a DBMS, and how does it differ from a file system?

A DBMS is software that stores, retrieves, and manages data in an organized, controlled way. A plain file system stores raw files with no built-in structure. A DBMS reduces redundancy and inconsistency, supports concurrent access, enforces integrity and security, provides backup and recovery, and offers a query language (SQL). In a file system, the application handles all of this itself.

## What are the different types of keys (primary, candidate, super, foreign, composite, alternate)?

### Types of keys

- **Super key:** any set of attributes that uniquely identifies a row (can include extra attributes).
- **Candidate key:** a minimal super key, with no redundant attribute.
- **Primary key:** the candidate key chosen to identify rows. It is unique and NOT NULL, and there is only one per table.
- **Alternate key:** a candidate key that was not chosen as primary.
- **Foreign key:** an attribute that references the primary key of another table.
- **Composite key:** a key made of two or more attributes.

```sql
CREATE TABLE student (
  id INT PRIMARY KEY,            -- primary key
  email VARCHAR(100) UNIQUE,     -- alternate key
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES dept(id)
);
```



> In a relational database table:
>
> - **Columns** are called **attributes** (or fields). They represent the specific properties or characteristics of an entity (e.g., `StudentID`, `Name`, `Email`).
> - **Rows** are called **tuples** or **records**. They represent a single, complete data entry or instance of an entity (e.g., information about one specific student).

## What is normalization? Explain 1NF, 2NF, 3NF, and BCNF.

Normalization organizes tables to reduce redundancy and avoid insert, update, and delete anomalies.

- To make normalization concrete, let's trace a poorly designed table and see how it evolves step-by-step through each normal form.

  Imagine we are tracking **Students**, their **Courses**, and their **Instructors** in a single unnormalized table.
  ### Unnormalized Table (Pre-1NF)
  
  | StudentID | StudentName | CoursesEnrolled | InstructorName       | InstructorOffice   |
  | --------- | ----------- | --------------- | -------------------- | ------------------ |
  | 101       | Alice       | Math, Physics   | Dr. Smith            | Room 302           |
  | 102       | Bob         | Chemistry       | Dr. Jones            | Room 405           |
  | 103       | Charlie     | Math, Chemistry | Dr. Smith, Dr. Jones | Room 302, Room 405 |
  
  - **The Problem:** Notice that Alice has multiple courses (`Math, Physics`) jammed into a single cell, and Charlie has multiple instructors and offices listed in comma-separated strings. This violates atomicity.
  ### 1. First Normal Form (1NF)
  - **Rule:** Every cell must contain a single, atomic (indivisible) value, and each row must be unique. No repeating groups or lists in a single cell.

  **Table after 1NF:**
  
  | StudentID | StudentName | Course    | InstructorName | InstructorOffice |
  | --------- | ----------- | --------- | -------------- | ---------------- |
  | 101       | Alice       | Math      | Dr. Smith      | Room 302         |
  | 101       | Alice       | Physics   | Dr. Smith      | Room 302         |
  | 102       | Bob         | Chemistry | Dr. Jones      | Room 405         |
  | 103       | Charlie     | Math      | Dr. Smith      | Room 302         |
  | 103       | Charlie     | Chemistry | Dr. Jones      | Room 405         |
  
  - **Composite Primary Key:** `(StudentID, Course)` is now required to uniquely identify each row.
  - **Remaining Issue:** Redundancy. If Dr. Smith changes his office, we have to update multiple rows. If a student drops a course, we might accidentally delete instructor data.
  ### 2. Second Normal Form (2NF)
  - **Rule:** Must be in 1NF, and **no partial dependencies**. Every non-key attribute must depend on the *entire* primary key, not just a part of it.
  - **Analysis:** Our primary key is `(StudentID, Course)`.
    - Does `StudentName` depend on *both* StudentID and Course? No, it depends *only* on `StudentID`. (Partial dependency!)
    - Does `InstructorName` and `InstructorOffice` depend on the student? No, they depend *only* on the `Course`.

  To fix this, we split the table into separate tables:

  **Table 1: Students**
  
  | StudentID | StudentName |
  | --------- | ----------- |
  | 101       | Alice       |
  | 102       | Bob         |
  | 103       | Charlie     |
  

  **Table 2: Student\_Courses (Junction Table)**
  
  | StudentID | Course    |
  | --------- | --------- |
  | 101       | Math      |
  | 101       | Physics   |
  | 102       | Chemistry |
  | 103       | Math      |
  | 103       | Chemistry |
  

  **Table 3: Courses\_Instructors**
  
  | Course    | InstructorName | InstructorOffice |
  | --------- | -------------- | ---------------- |
  | Math      | Dr. Smith      | Room 302         |
  | Physics   | Dr. Smith      | Room 302         |
  | Chemistry | Dr. Jones      | Room 405         |
  
  ### 3. Third Normal Form (3NF)
  - **Rule:** Must be in 2NF, and **no transitive dependencies** (a non-key attribute cannot depend on another non-key attribute).
  - **Looking at Table 3 (**`Courses_Instructors`**):**
    - Primary Key: `Course`
    - `InstructorName` depends on `Course`.
    - `InstructorOffice` depends on `InstructorName` (e.g., Dr. Smith always sits in Room 302).
    - Because `InstructorOffice` depends on a non-key attribute (`InstructorName`), we have a transitive dependency (`Course` →\\rightarrow→ `InstructorName` →\\rightarrow→ `InstructorOffice`).

  To fix this, we split Table 3 into two:

  **Table A: Courses**
  
  | Course    | InstructorName |
  | --------- | -------------- |
  | Math      | Dr. Smith      |
  | Physics   | Dr. Smith      |
  | Chemistry | Dr. Jones      |
  

  **Table B: Instructors**
  
  | InstructorName | InstructorOffice |
  | -------------- | ---------------- |
  | Dr. Smith      | Room 302         |
  | Dr. Jones      | Room 405         |
  
  ### 4. Boyce-Codd Normal Form (BCNF)
  - **Rule:** A stricter version of 3NF. For every functional dependency X→YX \\rightarrow YX→Y, **XXX must be a super key**.
  - **Scenario where 3NF isn't enough:** Imagine a table tracking **Students**, the **Subjects** they study, and their assigned **Advisors**:
    - Suppose a student can have multiple advisors for different subjects, but a specific advisor only teaches one specific subject (e.g., Advisor →\\rightarrow→ Subject).
    - If the table schema is `(StudentID, Advisor, Subject)`:
      - Primary/Candidate Keys: `(StudentID, Subject)` can identify the advisor, and `(StudentID, Advisor)` can identify the subject.
      - Functional Dependency: `Advisor` →\\rightarrow→ `Subject` (Because an advisor only handles one subject).
      - **The Violation:** `Advisor` determines `Subject`, but `Advisor` is **not** a super key on its own.

  **How BCNF fixes it:** We decompose the table so that every determinant is a candidate key:
  1. **Advisor\_Subject Table:** `(Advisor, Subject)`
  2. **Student\_Advisor Table:** `(StudentID, Advisor)`

  By breaking them down this way, data anomalies are eliminated, ensuring your database remains clean, scalable, and easy to maintain.

## What is denormalization, and when would you use it?

Denormalization deliberately adds redundancy (for example, duplicating a column or precomputing aggregates) to reduce joins and speed up reads. Use it in read-heavy systems, reporting, and analytics, where read speed matters more than storage and write simplicity. The cost is extra storage, harder updates, and a risk of inconsistency.

## What are ACID properties?

- **Atomicity:** a transaction either fully completes or has no effect.
- **Consistency:** a transaction moves the database from one valid state to another, respecting all constraints.
- **Isolation:** concurrent transactions do not interfere with each other.
- **Durability:** once committed, data survives crashes.

## What are the types of relationships (1:1, 1:N, M:N), and how do you model them?

- **One-to-one (1:1):** one person has one passport. Put a unique foreign key on either side.
- **One-to-many (1:N):** one department has many employees. Put the foreign key on the “many” side.
- **Many-to-many (M:N):** students and courses. Needs a junction (bridge) table.

```sql
CREATE TABLE enrollment (
  student_id INT REFERENCES student(id),
  course_id  INT REFERENCES course(id),
  PRIMARY KEY (student_id, course_id)
);
```

## What is an ER diagram?

An Entity-Relationship diagram is a visual blueprint of the database. **Entities** (rectangles) are things like Student, **attributes** (ovals) are their properties, and **relationships** (diamonds) show how entities connect, with cardinality such as 1:N. It is used in the design phase and later converted into tables.

## What is the difference between DDL, DML, DCL, and TCL?

- **DDL** (Data Definition): `CREATE`, `ALTER`, `DROP`, `TRUNCATE`. Defines structure.
- **DML** (Data Manipulation): `INSERT`, `UPDATE`, `DELETE`, `SELECT`. Works on data.
- **DCL** (Data Control): `GRANT`, `REVOKE`. Manages permissions.
- **TCL** (Transaction Control): `COMMIT`, `ROLLBACK`, `SAVEPOINT`. Manages transactions.

## What are dirty reads, non-repeatable reads, and phantom reads?

- **Dirty read:** T1 reads data that T2 has changed but not yet committed. If T2 rolls back, T1 holds invalid data.
- **Non-repeatable read:** T1 reads a row twice, and T2 updates or deletes that row in between, so the two reads differ.
- **Phantom read:** T1 runs the same range query twice, and T2 inserts or deletes matching rows in between, so new “phantom” rows appear.

## What is a deadlock, and how do you prevent or handle it?

A deadlock occurs when two or more transactions wait on each other’s locks forever (T1 holds A and wants B, T2 holds B and wants A).

- **Prevention:** acquire locks in a consistent order, keep transactions short, use lower isolation levels or lock timeouts, and avoid user interaction inside a transaction.
- **Detection and handling:** the DBMS builds a wait-for graph, finds a cycle, and rolls back one transaction (the “victim”). The application should retry it.

##  What is the difference between optimistic and pessimistic locking?

- **Pessimistic:** assumes conflicts are likely. It locks the row up front (`SELECT ... FOR UPDATE`) so others must wait. Safe, but it reduces concurrency.
- **Optimistic:** assumes conflicts are rare. There is no lock while working, and a version column is checked at update time. If it changed, the update fails and is retried. Better for read-heavy workloads.

sql

```sql
-- Optimistic
UPDATE product SET stock = 9, version = version + 1
WHERE id = 1 AND version = 3;   -- 0 rows updated = conflict

-- Pessimistic
SELECT * FROM product WHERE id = 1 FOR UPDATE;
```

## What is MVCC (multi-version concurrency control)?

MVCC keeps multiple versions of a row so readers see a consistent snapshot while writers create new versions. Readers don’t block writers, and writers don’t block readers. Each transaction sees data as of its start (or statement) time. Old versions are cleaned up later (e.g. `VACUUM` in PostgreSQL). It is used by PostgreSQL, Oracle, and MySQL InnoDB.

## What is the difference between a clustered and a non-clustered index?

- **Clustered:** determines the physical order of rows on disk, so the table data is the index. There is only one per table (usually the primary key). Range queries are fast.
- **Non-clustered:** a separate structure holding indexed values and pointers to the rows. A table can have many. It needs an extra lookup to fetch the row.

sql

```sql
CREATE INDEX idx_email ON student(email);  -- typically non-clustered
```
