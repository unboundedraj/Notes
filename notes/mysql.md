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

> To check if mysql is installed on your local machine run
>
> ```sql
> mysql --version
> ```
>
> Confirm the server is running and which edition it is:
>
> ```sql
> mysql -u root -p
> ```

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

## What happens when a query is run?

When you run `SELECT name FROM employee WHERE dept = 'IT';`, it goes through these stages:

### 1. Connection

The client (app, Workbench, or CLI) connects to the server. The server authenticates the user and checks permissions, and a connection or thread is assigned (usually from a pool).

### 2. Parsing

- **Lexical/syntax check:** the SQL text is split into tokens and checked against grammar rules. A typo like `SELCT` fails here.
- **Parse tree:** a structured representation of the query is built.

### 3. Semantic check (binding)

The database verifies that the tables and columns exist, that data types make sense, and that the user has privileges. `SELECT nme ...` fails here with “unknown column”.

### 4. Optimization

The **query optimizer** generates several possible execution plans and picks the cheapest using statistics (table size, index selectivity, data distribution). It decides:

- Whether to use an index or do a full table scan.
- The join order and algorithm (nested loop, hash, or sort-merge).
- How to rewrite the query (e.g. pushing filters down, flattening subqueries).

You can inspect the chosen plan with `EXPLAIN`.

### 5. Execution

The **execution engine** runs the plan, requesting rows from the storage engine. It first checks the **buffer pool/cache** and reads from disk only if the data isn’t in memory. Along the way it applies locks or MVCC snapshots for concurrency, and performs filtering, joins, grouping, and sorting.

### 6. Returning results

Rows are sent back to the client, often streamed in batches. For `INSERT`/`UPDATE`/`DELETE`, the server returns the affected row count instead.

### For write queries

Extra steps keep the data safe:

- Changes are first recorded in the **write-ahead log** (redo log) for durability.
- Pages are modified in memory, then flushed to disk later by a background process.
- On `COMMIT`, the log is flushed and locks are released. On `ROLLBACK`, the changes are undone using the undo log.

### Quick summary

```
Client → Connection → Parser → Semantic check → Optimizer → Executor → Storage engine → Result
```

```sql
EXPLAIN SELECT name FROM employee WHERE dept = 'IT';
```

This shows the plan the optimizer chose, such as whether it used an index on `dept`

## What are different SQL Datatypes?

SQL DATATYPES:


|               |                                 |                            |
| ------------- | ------------------------------- | -------------------------- |
| **Category**  | **Data Type**                   | **Description**            |
| **Numeric**   | INT, FLOAT, DECIMAL, BIGINT     | Numbers (whole or decimal) |
| **Text**      | CHAR(n), VARCHAR(n), TEXT       | Characters or strings      |
| **Date/Time** | DATE, TIME, DATETIME, TIMESTAMP | Date and time values       |
| **Boolean**   | BOOLEAN or BIT                  | True/False (1/0)           |
| **Binary**    | BLOB, BINARY, VARBINARY         | Binary data (e.g., images) |


## What is the difference between CHAR and VARCHAR?


| CHAR                                  | VARCHAR                                            |
| ------------------------------------- | -------------------------------------------------- |
| Fixed-length string                   | Variable-length string                             |
| Pads values to the defined length     | Stores values according to actual length           |
| Suitable for fixed-size values        | Suitable for variable-size values                  |
| Can use more space for shorter values | Generally more space-efficient for varying lengths |


## What is the difference between DELETE, DROP, and TRUNCATE?

DELETE

Removes records from a table.

```
DELETE FROM employees
WHERE emp_id = 101;
```

TRUNCATE

Removes all records but retains the table structure.

```
TRUNCATE TABLE employees;
```

DROP

Permanently removes the table itself, including its structure and data.

```
DROP TABLE employees;
```

Comparison:


| Feature                       | DELETE                        | TRUNCATE | DROP          |
| ----------------------------- | ----------------------------- | -------- | ------------- |
| Deletes records               | Yes                           | Yes, all | Yes           |
| Deletes structure             | No                            | No       | Yes           |
| WHERE condition               | Yes                           | No       | No            |
| Command category              | DML                           | DDL      | DDL           |
| Resets AUTO\_INCREMENT        | No                            | Yes      | Table removed |
| Transaction rollback in MySQL | Yes, for transactional tables | No       | No            |


Important: TRUNCATE and DROP cause implicit commits in MySQL. DELETE can be rolled back when used within a transaction on a transactional table such as InnoDB.

## What is ENUM in MySQL?

ENUM is a data type that restricts a column to a predefined list of values.

It behaves similarly to a dropdown list.

Example:

```
CREATE TABLE employees (
    name VARCHAR(50),
    gender ENUM('M', 'F', 'Other')
);
```

Advantages:

- Restricts invalid input.
- Saves storage because MySQL internally stores ENUM values using numeric indexes.
- Makes allowed values visible in the table definition.

## What is a database, table, row, and column?

- Database: A collection of related tables and other database objects.
- Table: Stores data in a structured format.
- Row: Represents one complete record.
- Column: Represents a particular attribute of a record.

## What is a primary key?

A primary key uniquely identifies every record in a table.A table can have only one primary key constraint, but that primary key can contain multiple columns, which is called a composite primary key.  
Important characteristics:

- Values must be unique.
- NULL values are not allowed.
- A table can have only one primary key constraint.
- A primary key can consist of one or multiple columns.

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

## What is a composite primary key?

A composite primary key consists of two or more columns that together uniquely identify a record.

Individual columns may contain duplicate values, but their combination must be unique.

Example:

```sql
CREATE TABLE project_assignments (
    project_id INT,
    emp_id INT,
    assigned_date DATE,

    PRIMARY KEY (project_id, emp_id)
);
```

## What is a foreign key?

A foreign key is a column or combination of columns that references a candidate key, usually the primary key, in another table.

It establishes a relationship between two tables and maintains referential integrity.

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

### Can a foreign key contain NULL values?

Yes, provided the column does not have a NOT NULL constraint.

### Can a table have multiple foreign keys?

Yes. A table can have multiple foreign keys referencing different tables or even the same table.

## How do you create a table, and what does each part mean?

Create the parent table first (departments), then the child table (employees) that references it.

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,                        -- Only one primary key per table; unique + not null
    department_name VARCHAR(100) UNIQUE NOT NULL          -- UNIQUE: no two departments can share a name
);

CREATE TABLE employees (                                  -- Creates a new table called 'employees'
    emp_id INT PRIMARY KEY,                               -- Integer; acts as Primary Key (unique & not null)
    name VARCHAR(100) NOT NULL,                           -- String up to 100 characters; cannot be null
    department_id INT,                                    -- Integer; linked to the 'departments' table
    salary DECIMAL(10, 2) DEFAULT 30000,                  -- Fixed-point: 8 digits before decimal, 2 after; defaults to 30000
    hire_date DATE,                                       -- Date field (YYYY-MM-DD)
    CONSTRAINT fk_dept                                    -- Names the constraint 'fk_dept'
        FOREIGN KEY (department_id)                       -- Declares department_id as a foreign key
        REFERENCES departments(department_id)             -- Links it to departments.department_id
);
```

> *Column-level constraints (NOT NULL, UNIQUE, DEFAULT) can be written in any order. Table-level constraints (like a composite PRIMARY KEY (col1, col2)) are usually written at the end of the column list for readability. MySQL doesn't care about position as long as the syntax is valid.*

## What are constraints in SQL?

Constraints are rules applied to table columns to maintain data accuracy and integrity.

Types of constraints:

1. PRIMARY KEY – Uniquely identifies each record.
2. FOREIGN KEY – Establishes relationships between tables.
3. NOT NULL – Prevents NULL values.
4. UNIQUE – Prevents duplicate values.
5. DEFAULT – Provides a default value.
6. CHECK – Validates a condition before accepting data.

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    salary DECIMAL(10,2)
        CHECK (salary >= 10000),
    department_id INT
);
```

## How do you modify a table's structure using ALTER?

```sql
-- Add a column
ALTER TABLE employees
ADD email VARCHAR(100);

-- Modify a column's data type
ALTER TABLE employees
MODIFY salary DECIMAL(12, 2);

-- Remove a column
ALTER TABLE employees
DROP COLUMN email;

-- Add a constraint
ALTER TABLE employees
ADD CONSTRAINT chk_salary
CHECK (salary > 1000);

-- Rename a table
RENAME TABLE employees TO staff;

-- Rename a column (MySQL 8+)
ALTER TABLE employees
RENAME COLUMN name TO full_name;
```

### What is the difference between MODIFY and CHANGE?

- MODIFY changes a column's definition, such as its data type or constraints.
- CHANGE can change the column definition and also rename the column.

## How do you insert data into a table?

Syntax:

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

Example:

```sql
INSERT INTO departments
(department_id, department_name)
VALUES
(1, 'Engineering'),
(2, 'HR'),
(3, 'Marketing');
```

Text values such as CHAR, VARCHAR, and TEXT are written inside single quotes. Numeric values do not require quotes.

If you provide values for every column in the correct table order, you can skip the column list:

```sql
INSERT INTO departments
VALUES
(1, 'Engineering'),
(2, 'HR'),
(3, 'Marketing');
```

To skip a column, mention only the columns you want to populate:

```sql
INSERT INTO departments (department_id)
VALUES (4);
```

This works only if the omitted column allows NULL or has a DEFAULT value.

## How do you update data?

UPDATE modifies existing records.

```sql
UPDATE employees
SET salary = 50000
WHERE name = 'Bob';
```

Important: Always use WHERE when you intend to update specific records.

Without WHERE, all records in the table will be updated.

### Can we update multiple columns simultaneously?

Yes.

```sql
UPDATE employees
SET salary = 60000,
    department_id = 2
WHERE emp_id = 101;
```

## How do you delete data?

```sql
DELETE FROM employees
WHERE emp_id = 102;
```

This deletes only the employee whose ID is 102.

Without WHERE, all records are deleted, but the table structure remains.

## How do you retrieve data using SELECT?

SELECT is used to retrieve data from tables.

```sql
-- Retrieve specific columns
SELECT name, salary
FROM employees;

-- Retrieve all columns
SELECT *
FROM departments;

-- Retrieve records using a condition
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

## How do you sort and limit results?

ORDER BY sorts query results.

```
SELECT name, salary
FROM employees
ORDER BY salary DESC;
```

- ASC – Ascending order (default).
- DESC – Descending order.

To retrieve the top three highest-paid employees:

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

### What is the difference between ORDER BY and GROUP BY?

- ORDER BY sorts the result set.
- GROUP BY groups records based on common column values, generally to perform aggregate calculations.

## How do you remove duplicates from query results?

Use DISTINCT.

```
SELECT DISTINCT department_id
FROM employees;
```

This returns each department ID only once.

### Can DISTINCT work on multiple columns?

Yes.

```
SELECT DISTINCT department_id, gender
FROM employees;
```

Here, duplicate combinations of department ID and gender are removed.

## How does pattern matching work with LIKE?

LIKE is used to search for patterns in strings.

Two important wildcards:

- `%` – Matches zero or more characters.
- `_` – Matches exactly one character.

Examples:

```sql
-- Names starting with A
SELECT name
FROM employees
WHERE name LIKE 'A%';

-- Names ending with e
SELECT name
FROM employees
WHERE name LIKE '%e';

-- Names containing ar
SELECT name
FROM employees
WHERE name LIKE '%ar%';

-- Names with exactly four characters
SELECT name
FROM employees
WHERE name LIKE '____';
```

## How do you use IN and BETWEEN?

IN: Checks whether a value matches any value in a specified list.

```sql
SELECT name
FROM employees
WHERE department_id IN (1, 3);
```

This is equivalent to:

```sql
WHERE department_id = 1
   OR department_id = 3;
```

BETWEEN: Checks whether a value falls within a specified range. Both endpoints are inclusive.

```sql
SELECT name, salary
FROM employees
WHERE salary BETWEEN 45000 AND 60000;
```

Example for employees hired in 2022:

```sql
SELECT name
FROM employees
WHERE hire_date BETWEEN '2022-01-01'
                    AND '2022-12-31';
```

## How do you check NULL values?

Use:

- IS NULL
- IS NOT NULL

Never use `= NULL` or `!= NULL`.

```
SELECT name
FROM employees
WHERE department_id IS NULL;

SELECT name
FROM employees
WHERE salary IS NOT NULL;
```

## How do you combine multiple conditions?

Use AND, OR, and NOT.

Example: Find employees hired in 2021 whose names contain the letter 'e' and whose salary is not NULL.

```sql
SELECT name, hire_date, salary
FROM employees
WHERE name LIKE '%e%'
  AND hire_date BETWEEN '2021-01-01'
                    AND '2021-12-31'
  AND salary IS NOT NULL;
```

## How do you concatenate columns into one string?

Use CONCAT() in MySQL.

```sql
SELECT CONCAT(
    vend_name,
    ' (',
    vend_country,
    ')'
)
FROM vendors
ORDER BY vend_name;
```

CONCAT combines multiple strings into one string.

In MySQL, CONCAT returns NULL if any argument is NULL.

## What are aggregate functions in SQL?

Aggregate functions perform calculations on multiple rows and return a single result per group.

Common aggregate functions:

- COUNT() – Counts rows.
- SUM() – Calculates the total.
- AVG() – Calculates the average.
- MAX() – Finds the maximum value.
- MIN() – Finds the minimum value.

Examples:

```sql
-- Count all employees
SELECT COUNT(*) AS total_employees
FROM employees;

-- Count employees having a salary
SELECT COUNT(salary) AS with_salary
FROM employees;

-- Calculate total salary
SELECT SUM(salary) AS total_salaries
FROM employees;

-- Calculate average salary
SELECT AVG(salary) AS avg_salary
FROM employees;

-- Find highest salary
SELECT MAX(salary) AS top_salary
FROM employees;

-- Find lowest salary
SELECT MIN(salary) AS min_salary
FROM employees;
```

## What is the difference between COUNT(\*) and COUNT(column\_name)?

- COUNT(\*) counts all rows, including rows containing NULL values.
- COUNT(column\_name) counts only rows where that particular column is NOT NULL.

Example:

Suppose a table contains five records, but two records have NULL salary values.

```
SELECT COUNT(*) FROM employees;
-- Returns 5

SELECT COUNT(salary) FROM employees;
-- Returns 3
```

### Do aggregate functions ignore NULL values?

Most aggregate functions, such as SUM(), AVG(), MIN(), and MAX(), ignore NULL values.

COUNT(\*) is the exception because it counts rows regardless of NULL values.

## How does GROUP BY work?

GROUP BY divides rows into groups based on one or more columns.

It is commonly used with aggregate functions.

Example: Find the total number of employees in each department.

```sql
SELECT department_id,
       COUNT(*) AS total_employees
FROM employees
GROUP BY department_id;
```

Example: Find the average salary in each department.

```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

### Can we use GROUP BY on multiple columns?

Yes.

```sql
SELECT department_id,
       gender,
       COUNT(*) AS total_employees
FROM employees
GROUP BY department_id, gender;
```

This groups employees based on the combination of department and gender.

### Can we use GROUP BY without aggregate functions?

Yes. GROUP BY can group records even without aggregate functions, although DISTINCT is often more appropriate when the goal is simply to retrieve unique combinations.

## What does HAVING do?

HAVING filters groups after GROUP BY has been applied.

Example: Find departments having more than one employee.

```
SELECT department_id,
       COUNT(*) AS emp_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 1;
```

Example: Find departments whose average salary is greater than 50000.

```
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```
