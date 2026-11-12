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

```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

## What is the difference between WHERE and HAVING?


| WHERE                                                    | HAVING                      |
| -------------------------------------------------------- | --------------------------- |
| Filters individual rows                                  | Filters groups              |
| Applied before GROUP BY                                  | Applied after GROUP BY      |
| Cannot directly use aggregate functions in its condition | Can use aggregate functions |
| Can be used without GROUP BY                             | Commonly used with GROUP BY |


Example:

```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
WHERE salary > 20000
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

Explanation:

1. WHERE removes employees whose salary is 20000 or below.
2. GROUP BY groups the remaining employees by department.
3. AVG() calculates the average salary of each department.
4. HAVING keeps only departments with an average salary above 50000.

## What is the difference between COUNT, SUM, and AVG?

- COUNT() returns the number of records or non-NULL values.
- SUM() returns the total of numeric values.
- AVG() returns the average of non-NULL numeric values.

Example:

```
SELECT
    COUNT(salary),
    SUM(salary),
    AVG(salary)
FROM employees;
```

## What is the logical execution order of a SELECT query?

This is a very important interview question.

Although we write SELECT first, SQL logically processes the query in a different order.

**Logical Order of SQL Clause Evaluation**


|          |            |                                                               |
| -------- | ---------- | ------------------------------------------------------------- |
| **Step** | **Clause** | **Purpose**                                                   |
| 1        | FROM       | Identifies the tables involved and forms the base result set. |
| 2        | ON         | Applies join conditions (if JOIN is used).                    |
| 3        | JOIN       | Combines rows from different tables.                          |
| 4        | WHERE      | Filters rows **before** grouping (non-aggregated filter).     |
| 5        | GROUP BY   | Groups rows into summary rows.                                |
| 6        | HAVING     | Filters groups (after aggregation).                           |
| 7        | SELECT     | Selects the columns to display, including aggregates.         |
| 8        | DISTINCT   | Removes duplicates from the final result.                     |
| 9        | ORDER BY   | Sorts the final result set.                                   |
| 10       | LIMIT      | Restricts the number of rows returned.                        |


Example:

```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
WHERE salary > 20000
GROUP BY department_id
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC
LIMIT 3;
```

Understanding this order helps explain why we cannot normally use an aggregate function in WHERE and why SELECT aliases can be used in ORDER BY but not WHERE.

## What is a JOIN, and what are its types?

A JOIN combines records from two or more tables based on a related column.

For example, employees and departments can be joined using department\_id.

Common types:

**1. INNER JOIN**

Returns only matching records from both tables.

**2. LEFT JOIN (LEFT OUTER JOIN)**

Returns all records from the left table and matching records from the right table. If no match exists, right-side columns contain NULL.

**3. RIGHT JOIN (RIGHT OUTER JOIN)**

Returns all records from the right table and matching records from the left table.

**4. FULL OUTER JOIN**

Returns all records from both tables, whether matching or not.

MySQL does not directly support FULL OUTER JOIN.

**5. CROSS JOIN**

Returns the Cartesian product of two tables.

**6. SELF JOIN**

Joins a table with itself.

## How does INNER JOIN work?

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees AS e
INNER JOIN departments AS d
    ON e.department_id = d.department_id;
```

Explanation:

- `e` is an alias for employees.
- `d` is an alias for departments.
- ON specifies the matching condition.
- Only employees having a matching department are returned.

The same result can be obtained using an implicit join:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e,
     departments d
WHERE e.department_id = d.department_id;
```

However, explicit JOIN syntax is generally preferred because it makes relationships and conditions easier to understand.

## How do LEFT JOIN and RIGHT JOIN work?

LEFT JOIN example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees AS e
LEFT JOIN departments AS d
    ON e.department_id = d.department_id;
```

Returns all employees, even if they are not assigned to a department.

RIGHT JOIN example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees AS e
RIGHT JOIN departments AS d
    ON e.department_id = d.department_id;
```

Returns all departments, even if no employee belongs to them.

## How do you perform a FULL OUTER JOIN in MySQL?

MySQL does not directly support FULL OUTER JOIN.

We can simulate it using LEFT JOIN and RIGHT JOIN with UNION.

```sql
SELECT
    e.name,
    d.department_name
FROM employees AS e
LEFT JOIN departments AS d
    ON e.department_id = d.department_id

UNION

SELECT
    e.name,
    d.department_name
FROM employees AS e
RIGHT JOIN departments AS d
    ON e.department_id = d.department_id;
```

UNION combines both results and removes duplicate rows.

A more explicit alternative that preserves duplicate rows is:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id

UNION ALL

SELECT
    e.name,
    d.department_name
FROM departments d
LEFT JOIN employees e
    ON e.department_id = d.department_id
WHERE e.emp_id IS NULL;
```

This second approach adds only departments that did not find a matching employee.

## What is a CROSS JOIN?

A CROSS JOIN returns every possible combination of rows from two tables.

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
CROSS JOIN departments d;
```

If employees contains 5 records and departments contains 3 records, the result contains:

5 × 3 = 15 rows.

Interview follow-up: What is a Cartesian product?

A Cartesian product is the result of combining every row from one table with every row from another table.

## How do you find records present in one table but not another?

This is commonly asked in interviews.

Example: Find departments that do not have any employees.

```
SELECT d.department_id,
       d.department_name
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.emp_id IS NULL;
```

Explanation:

1. LEFT JOIN keeps all departments.
2. Matching employees are joined.
3. Departments without employees have NULL in employee columns.
4. WHERE filters those departments.

This technique is called an anti-join pattern.

## What is a subquery, and when is it used?

A subquery is a SQL query nested inside another SQL query.

It is used when:

- We need to filter records using the result of another query.
- We need to compare values with an aggregate result.
- We need to fetch related information indirectly.
- We need to create a temporary result set for another query.

## What is a subquery in the FROM clause?

A subquery inside FROM is also called a derived table.

Example: Find departments whose average salary is greater than 50000.

```sql
SELECT department_id,
       avg_salary
FROM (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) AS dept_avg
WHERE avg_salary > 50000;
```

Explanation:

1. The inner query calculates the average salary for each department.
2. Its result behaves like a temporary table.
3. The outer query filters departments based on their average salary.

Note: MySQL requires a derived table to have an alias.

## What is a correlated subquery?

A correlated subquery depends on the outer query.

Example: Retrieve every employee's department name.

```sql
SELECT
    name,
    (
        SELECT department_name
        FROM departments
        WHERE departments.department_id =
              employees.department_id
    ) AS dept_name
FROM employees;
```

The inner query refers to `employees.department_id`, which comes from the outer query.

Interview follow-up: What is the difference between a normal subquery and a correlated subquery?

- A normal subquery can execute independently of the outer query.
- A correlated subquery depends on the outer query's current row.

A correlated subquery is conceptually evaluated for each relevant outer row, although the optimizer may transform its execution.

## How do you use IN with a subquery?

Example: Find employees working in departments having more than one employee.

```sql
SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING COUNT(*) > 1
);
```

The inner query returns department IDs having more than one employee.

The outer query retrieves employees belonging to those departments.

## What is a nested subquery?

A nested subquery is a subquery placed inside another subquery.

Example: Find employees earning more than the highest-paid employee in HR.

```sql
SELECT name, salary
FROM employees
WHERE salary > (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id = (
        SELECT department_id
        FROM departments
        WHERE department_name = 'HR'
    )
);
```

Explanation:

1. The innermost query finds the HR department ID.
2. The middle query finds the highest salary in HR.
3. The outer query finds employees earning more than that salary.

## When should you use a subquery versus a JOIN?

- Return one calculated value: Scalar subquery.
- Filter records based on a list: IN subquery.
- Retrieve related columns from another table: JOIN.
- Perform aggregation on an intermediate result: Derived table or subquery in FROM.

Both JOINs and subqueries can often solve the same problem. The best choice depends on readability, correctness, and execution performance.

## What is the difference between UNION and UNION ALL?

Both combine results from multiple SELECT statements.

UNION

Combines results and removes duplicate rows.

```
SELECT name
FROM employees

UNION

SELECT name
FROM managers;
```

UNION ALL

Combines results without removing duplicates.

```
SELECT name
FROM employees

UNION ALL

SELECT name
FROM managers;
```

Comparison:


| UNION                          | UNION ALL                              |
| ------------------------------ | -------------------------------------- |
| Removes duplicates             | Keeps duplicates                       |
| Usually slower                 | Usually faster                         |
| Performs duplicate elimination | Does not perform duplicate elimination |


Important rules:

- Both queries must return the same number of columns.
- Corresponding columns must have compatible data types.
- Column names in the result generally come from the first SELECT.

## How do you add IF/ELSE logic to a SQL query?

Use CASE.

CASE works similarly to if/else conditions in programming languages.

Example:

```
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_band
FROM employees;
```

Explanation:

- Salary greater than or equal to 80000 → High.
- Salary greater than or equal to 50000 → Medium.
- All remaining salaries → Low.

### What happens if none of the CASE conditions match and ELSE is not provided?

CASE returns NULL.

## What is COALESCE in SQL?

COALESCE returns the first non-NULL value from a list of expressions.

Example:

```
SELECT
    name,
    COALESCE(phone_number, 'No number') AS phone
FROM employees;
```

If phone\_number is NULL, it returns 'No number'.

Otherwise, it returns the actual phone number.

## What is a VIEW in SQL?

A VIEW is a saved SQL query that behaves like a virtual table.

It generally does not store the actual result data. Instead, it retrieves data from the underlying tables whenever queried.

Example:

```
CREATE VIEW high_earners AS
SELECT name, salary
FROM employees
WHERE salary > 80000;
```

Retrieve data:

```
SELECT *
FROM high_earners;
```

Delete the view:

```
DROP VIEW high_earners;
```

Advantages:

- Simplifies complex queries.
- Provides an additional layer of security by exposing selected columns.
- Makes frequently used queries reusable.
- Helps organize database logic.

### Does a VIEW store data?

A normal view does not store its result data. It stores the query definition.

### Can we perform INSERT, UPDATE, and DELETE on a VIEW?

Yes, some views are updatable.

However, views involving operations such as GROUP BY, aggregate functions, DISTINCT, and certain joins may not be directly updatable.

### What is the difference between a VIEW and a TABLE?

- A table physically stores data.
- A normal view stores a query definition and displays data from underlying tables.

## What is an INDEX in SQL?

An index is a database object that helps retrieve records faster.

It works similarly to the index of a book: instead of scanning every page, we can locate the required information more efficiently.

Example:

```
CREATE INDEX idx_salary
ON employees(salary);
```

Delete an index:

```
DROP INDEX idx_salary
ON employees;
```

### When should you use indexes?

- On columns frequently used in WHERE conditions.
- On columns used in JOIN conditions.
- On columns used in ORDER BY.
- On foreign key columns.
- On large tables where read performance is important.

Disadvantages:

- Indexes consume additional storage.
- They can slow down INSERT, UPDATE, and DELETE operations because indexes also need to be maintained.
- Too many indexes can negatively affect performance.

### What are the different types of indexes in MySQL?

Common types include:

1. PRIMARY KEY index – Created automatically for the primary key.
2. UNIQUE index – Prevents duplicate indexed values, with MySQL's NULL handling rules.
3. INDEX (non-unique index) – Improves data retrieval.
4. FULLTEXT index – Supports full-text searching.
5. SPATIAL index – Supports spatial data searching.

MySQL InnoDB also uses clustered primary-key storage and secondary indexes.

## What is a TRIGGER in SQL?

A trigger is a database object that automatically executes when a specified event occurs on a table.

Triggers can execute before or after:

- INSERT
- UPDATE
- DELETE

Example:

```sql
DELIMITER //

CREATE TRIGGER before_insert_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN

    IF NEW.salary < 0 THEN

        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary cannot be negative';

    END IF;

END //

DELIMITER ;
```

Explanation:

- DELIMITER changes the statement delimiter in the MySQL client so that semicolons inside the trigger body do not terminate the CREATE TRIGGER statement.
- BEFORE INSERT executes before a new record is inserted.
- FOR EACH ROW executes the trigger for every affected row.
- NEW refers to the incoming row.
- SIGNAL generates an error if the condition is violated.

Delete the trigger:

```
DROP TRIGGER before_insert_check_salary;
```

### What is the difference between NEW and OLD in triggers?

- NEW represents the new row values.
- OLD represents the existing row values.

Usage:


| Trigger | NEW | OLD |
| ------- | --- | --- |
| INSERT  | Yes | No  |
| UPDATE  | Yes | Yes |
| DELETE  | No  | Yes |


## What is a TRANSACTION in SQL?

A transaction is a group of SQL operations treated as one logical unit of work.

Either all operations succeed and are committed, or the transaction can be rolled back to undo the changes.

Example: Transferring 100 from one bank account to another.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

COMMIT;
```

If something goes wrong before committing:

```
ROLLBACK;
```

This undoes the uncommitted changes.

## What are the ACID properties of a transaction?

ACID represents four important transaction properties.

1. Atomicity

All operations in a transaction succeed together, or none of them are applied.

Example: If money is deducted from one account but cannot be credited to another, the transaction should be rolled back.

2. Consistency

A transaction should take the database from one valid state to another valid state, maintaining database constraints and rules.

3. Isolation

Concurrent transactions should not interfere with each other in ways that violate the chosen isolation level.

4. Durability

Once a transaction is committed, its changes are expected to persist even after a system failure, subject to the database's durability configuration.

### Why is ACID important?

ACID ensures reliable and consistent database operations, especially in banking, payment systems, and other applications where data accuracy is critical.

## What is the difference between COMMIT and ROLLBACK?


| COMMIT                       | ROLLBACK                                                             |
| ---------------------------- | -------------------------------------------------------------------- |
| Saves transaction changes    | Undoes uncommitted changes                                           |
| Makes changes permanent      | Returns to the previous transaction state                            |
| Ends the current transaction | Ends the current transaction when rolling back the whole transaction |


## What are WINDOW FUNCTIONS in SQL?

Window functions perform calculations across a set of related rows without combining those rows into a single result.

Unlike GROUP BY, window functions preserve individual rows.

Common window functions:

- ROW\_NUMBER()
- RANK()
- DENSE\_RANK()
- LEAD()
- LAG()
- SUM() OVER()
- AVG() OVER()

Example:

```sql
SELECT
    name,
    department_id,
    salary,

    ROW_NUMBER() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS row_num

FROM employees;
```

Explanation:

- PARTITION BY divides employees into departments.
- ORDER BY sorts employees by salary within each department.
- ROW\_NUMBER assigns a unique sequential number within each department.

## What is the difference between ROW\_NUMBER(), RANK(), and DENSE\_RANK()?

This is one of the most important SQL interview questions.

Suppose the salaries are:


| Employee | Salary |
| -------- | ------ |
| A        | 90000  |
| B        | 80000  |
| C        | 80000  |
| D        | 70000  |


Results:


| Employee | ROW\_NUMBER | RANK | DENSE\_RANK |
| -------- | ----------- | ---- | ----------- |
| A        | 1           | 1    | 1           |
| B        | 2           | 2    | 2           |
| C        | 3           | 2    | 2           |
| D        | 4           | 4    | 3           |


ROW\_NUMBER()

Assigns a unique sequential number to each row.

RANK()

Assigns the same rank to tied values but skips the next rank.

DENSE\_RANK()

Assigns the same rank to tied values without skipping the next rank.

Example:

```sql
SELECT
    name,
    salary,

    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num,

    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank,

    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS dense_salary_rank

FROM employees;
```
