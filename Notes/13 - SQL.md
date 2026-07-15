# SQL — Comprehensive Interview Preparation Guide

> **How to use this guide:** Read top-to-bottom for fundamentals, jump to sections for revision, and drill the **Cheat Sheet** + **Top Interview Problems** before interviews.

---

## Table of Contents

1. [SQL Basics](#1-sql-basics)
2. [Database Fundamentals](#2-database-fundamentals)
3. [DDL — Data Definition Language](#3-ddl--data-definition-language)
4. [DML — Data Manipulation Language](#4-dml--data-manipulation-language)
5. [DCL — Data Control Language](#5-dcl--data-control-language)
6. [TCL — Transaction Control Language](#6-tcl--transaction-control-language)
7. [Constraints & Keys](#7-constraints--keys)
8. [Joins](#8-joins)
9. [Subqueries & CTEs](#9-subqueries--ctes)
10. [Window Functions](#10-window-functions)
11. [Aggregates, GROUP BY & HAVING](#11-aggregates-group-by--having)
12. [EXISTS, ANY & ALL](#12-exists-any--all)
13. [CASE Expressions](#13-case-expressions)
14. [Views, Procedures, Functions & Triggers](#14-views-procedures-functions--triggers)
15. [Transactions & ACID](#15-transactions--acid)
16. [Normalization & Denormalization](#16-normalization--denormalization)
17. [Indexes](#17-indexes)
18. [Query Execution & Optimization](#18-query-execution--optimization)
19. [Pagination](#19-pagination)
20. [Common Coding Questions](#20-common-coding-questions)
21. [Top Interview SQL Problems](#21-top-interview-sql-problems)
22. [Scenario Questions](#22-scenario-questions)
23. [Cheat Sheet](#23-cheat-sheet)

---

## Sample Schema (used throughout)

```sql
-- Employees
CREATE TABLE departments (
    dept_id   INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL
);

CREATE TABLE employees (
    emp_id     INT PRIMARY KEY,
    name       VARCHAR(100) NOT NULL,
    salary     DECIMAL(10,2),
    dept_id    INT,
    manager_id INT,
    hire_date  DATE,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id),
    FOREIGN KEY (manager_id) REFERENCES employees(emp_id)
);

CREATE TABLE orders (
    order_id   INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    amount     DECIMAL(10,2)
);
```

---

## 1. SQL Basics

### Q: What is SQL?

**A:** SQL (Structured Query Language) is a declarative language for defining, querying, and manipulating relational databases. You describe *what* data you want; the database engine decides *how* to fetch it.

### Q: What are the main categories of SQL commands?

| Category | Purpose | Commands |
|----------|---------|----------|
| **DDL** | Define structure | CREATE, ALTER, DROP, TRUNCATE, RENAME |
| **DML** | Manipulate data | SELECT, INSERT, UPDATE, DELETE, MERGE |
| **DCL** | Control access | GRANT, REVOKE |
| **TCL** | Manage transactions | COMMIT, ROLLBACK, SAVEPOINT |

### Q: What is the difference between SQL and a DBMS?

**A:** SQL is the *language*. A DBMS (MySQL, PostgreSQL, SQL Server, Oracle) is the *software* that implements SQL, stores data, enforces constraints, and optimizes queries.

### Q: What is a relational database?

**A:** Data is organized in **tables** (relations) of rows and columns. Relationships between tables are expressed via **keys** (primary/foreign keys).

### Basic SELECT syntax

```sql
SELECT column1, column2
FROM   table_name
WHERE  condition
ORDER BY column1 ASC
LIMIT  10;
```

### Q: What is the difference between `WHERE` and `HAVING`?

**A:** `WHERE` filters **rows before** grouping. `HAVING` filters **groups after** `GROUP BY`.

```sql
-- Employees earning > 50k in Sales dept
SELECT dept_id, AVG(salary)
FROM   employees
WHERE  salary > 50000
GROUP BY dept_id
HAVING AVG(salary) > 60000;
```

### Q: What is `NULL`?

**A:** `NULL` means *unknown* or *missing*, not zero or empty string. Use `IS NULL` / `IS NOT NULL`; never `= NULL`.

```sql
SELECT * FROM employees WHERE manager_id IS NULL;  -- top-level managers
```

### Q: What is the difference between `DISTINCT` and `GROUP BY`?

**A:** `DISTINCT` removes duplicate rows. `GROUP BY` groups rows for aggregation. `SELECT DISTINCT dept_id` ≈ `SELECT dept_id GROUP BY dept_id` (without aggregates).

---

## 2. Database Fundamentals

### Q: What is a schema?

**A:** A schema is the logical structure of a database — tables, views, indexes, constraints, and relationships.

### Q: What is a primary key vs a foreign key?

**A:**
- **Primary key:** Uniquely identifies each row in a table. NOT NULL + UNIQUE.
- **Foreign key:** Column(s) referencing a primary key in another table, enforcing referential integrity.

### Q: What is referential integrity?

**A:** Rules ensuring relationships remain consistent. You cannot insert a child row with a non-existent parent FK, and you cannot delete a parent if children exist (unless CASCADE is set).

### Q: What is cardinality?

**A:** Describes relationship multiplicity:
- **1:1** — One employee ↔ one parking spot
- **1:N** — One department → many employees
- **M:N** — Many students ↔ many courses (requires a junction table)

### Q: OLTP vs OLAP?

| | OLTP | OLAP |
|---|------|------|
| Purpose | Day-to-day transactions | Analytics & reporting |
| Queries | Short, frequent writes/reads | Complex aggregations |
| Schema | Normalized | Often denormalized/star schema |
| Examples | Banking, e-commerce checkout | Data warehouse dashboards |

### Q: What is a junction (bridge) table?

```sql
CREATE TABLE student_course (
    student_id INT,
    course_id  INT,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id)  REFERENCES courses(id)
);
```

---

## 3. DDL — Data Definition Language

### Q: What does DDL do?

**A:** Defines and modifies database objects (tables, indexes, views, schemas).

### CREATE TABLE

```sql
CREATE TABLE products (
    product_id   INT          PRIMARY KEY AUTO_INCREMENT,
    name         VARCHAR(200) NOT NULL,
    price        DECIMAL(10,2) CHECK (price > 0),
    category     VARCHAR(50),
    created_at   TIMESTAMP    DEFAULT CURRENT_TIMESTAMP
);
```

### ALTER TABLE

```sql
ALTER TABLE products ADD COLUMN stock INT DEFAULT 0;
ALTER TABLE products MODIFY COLUMN price DECIMAL(12,2);
ALTER TABLE products DROP COLUMN category;
ALTER TABLE products ADD CONSTRAINT uk_name UNIQUE (name);
```

### DROP vs TRUNCATE vs DELETE

| Command | Type | Rollback? | Removes structure? | Triggers? |
|---------|------|-----------|-------------------|-----------|
| `DELETE` | DML | Yes (in transaction) | No | Fires |
| `TRUNCATE` | DDL | No* | No | Usually no |
| `DROP` | DDL | No | Yes | N/A |

```sql
TRUNCATE TABLE products;   -- fast, resets identity, no WHERE
DROP TABLE products;      -- removes table entirely
```

### Q: What is AUTO_INCREMENT / IDENTITY / SERIAL?

**A:** Database-generated sequential integer for primary keys.

```sql
-- PostgreSQL
CREATE TABLE t (id SERIAL PRIMARY KEY);

-- SQL Server
CREATE TABLE t (id INT IDENTITY(1,1) PRIMARY KEY);

-- MySQL
CREATE TABLE t (id INT AUTO_INCREMENT PRIMARY KEY);
```

---

## 4. DML — Data Manipulation Language

### INSERT

```sql
INSERT INTO employees (emp_id, name, salary, dept_id)
VALUES (1, 'Alice', 75000, 10);

INSERT INTO employees (name, salary)
SELECT name, salary FROM temp_hires;
```

### UPDATE

```sql
UPDATE employees
SET    salary = salary * 1.10
WHERE  dept_id = 10;
```

### DELETE

```sql
DELETE FROM employees WHERE emp_id = 5;
```

### MERGE / UPSERT (dialect-specific)

```sql
-- PostgreSQL
INSERT INTO employees (emp_id, name, salary)
VALUES (2, 'Bob', 80000)
ON CONFLICT (emp_id) DO UPDATE SET salary = EXCLUDED.salary;

-- MySQL
INSERT INTO employees (emp_id, name, salary)
VALUES (2, 'Bob', 80000)
ON DUPLICATE KEY UPDATE salary = VALUES(salary);
```

### Q: Can you UPDATE or DELETE with JOIN?

```sql
-- MySQL example
UPDATE employees e
JOIN   departments d ON e.dept_id = d.dept_id
SET    e.salary = e.salary * 1.05
WHERE  d.dept_name = 'Engineering';
```

---

## 5. DCL — Data Control Language

### Q: What is DCL?

**A:** Controls who can access what — permissions and roles.

```sql
GRANT SELECT, INSERT ON employees TO analyst_role;
GRANT analyst_role TO jane;

REVOKE INSERT ON employees FROM analyst_role;
```

### Common privileges

`SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `DROP`, `ALTER`, `EXECUTE`, `ALL PRIVILEGES`

---

## 6. TCL — Transaction Control Language

```sql
BEGIN;  -- or START TRANSACTION

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

SAVEPOINT sp1;
DELETE FROM audit_log WHERE log_date < '2020-01-01';

ROLLBACK TO sp1;  -- undo only the DELETE
COMMIT;           -- persist the two UPDATEs
```

### Q: What is a savepoint?

**A:** A marker within a transaction allowing partial rollback without undoing the entire transaction.

---

## 7. Constraints & Keys

### Constraint types

| Constraint | Purpose |
|------------|---------|
| `PRIMARY KEY` | Unique + NOT NULL identifier |
| `FOREIGN KEY` | Referential integrity |
| `UNIQUE` | No duplicate values (NULLs allowed*) |
| `NOT NULL` | Value required |
| `CHECK` | Custom validation rule |
| `DEFAULT` | Value when none provided |

```sql
CREATE TABLE orders (
    order_id    INT PRIMARY KEY,
    customer_id INT NOT NULL,
    status      VARCHAR(20) DEFAULT 'pending'
                  CHECK (status IN ('pending','shipped','cancelled')),
    UNIQUE (customer_id, order_id)
);
```

---

### Primary Key

**Q: What is a primary key?**

**A:** A column (or set of columns) that uniquely identifies each row. Only one per table. Implies NOT NULL and UNIQUE. Creates a clustered index in SQL Server; in PostgreSQL/MySQL behavior varies.

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email   VARCHAR(255) UNIQUE
);
```

---

### Foreign Key

**Q: What is a foreign key?**

**A:** A column referencing a primary/unique key in another table.

```sql
ALTER TABLE employees
ADD CONSTRAINT fk_dept
FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
ON DELETE SET NULL
ON UPDATE CASCADE;
```

**ON DELETE / ON UPDATE actions:** `CASCADE`, `SET NULL`, `SET DEFAULT`, `RESTRICT` / `NO ACTION`

---

### Unique Key

**Q: Primary key vs unique key?**

| | Primary Key | Unique Key |
|---|-------------|------------|
| Count per table | One | Multiple |
| NULLs | Not allowed | Usually one NULL allowed |
| Index | Clustered (SQL Server) | Non-clustered |

```sql
ALTER TABLE employees ADD CONSTRAINT uk_email UNIQUE (email);
```

---

### Composite Key

**Q: What is a composite key?**

**A:** A primary or foreign key made of **two or more columns** together uniquely identifying a row.

```sql
CREATE TABLE order_items (
    order_id   INT,
    product_id INT,
    quantity   INT,
    PRIMARY KEY (order_id, product_id)  -- composite primary key
);
```

---

### Candidate Key

**Q: What is a candidate key?**

**A:** Any column (or set) that **could** serve as the primary key — minimal super key. A table can have multiple candidate keys.

**Example:** In `employees`, both `emp_id` and `email` could be candidate keys.

---

### Super Key

**Q: What is a super key?**

**A:** Any set of attributes that **uniquely identifies** a row. A super key may contain redundant columns.

**Example:** `{emp_id}`, `{emp_id, name}`, `{email}` are all super keys for employees.

---

### Alternate Key

**Q: What is an alternate key?**

**A:** A candidate key that is **not** chosen as the primary key. Enforced via `UNIQUE` constraint.

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,           -- primary key
    email  VARCHAR(255) UNIQUE,       -- alternate key
    ssn    VARCHAR(11) UNIQUE         -- alternate key
);
```

### Key hierarchy (interview diagram)

```
Super Key  ⊃  Candidate Key  =  Primary Key  +  Alternate Keys
```

---

## 8. Joins

### Q: What is a JOIN?

**A:** Combines rows from two or more tables based on a related column.

### Types of Joins

| Join | Returns |
|------|---------|
| **INNER JOIN** | Matching rows only |
| **LEFT JOIN** | All left rows + matching right (NULL if no match) |
| **RIGHT JOIN** | All right rows + matching left |
| **FULL OUTER JOIN** | All rows from both; NULLs where no match |
| **CROSS JOIN** | Cartesian product (every combo) |
| **SELF JOIN** | Table joined to itself |

### INNER JOIN

```sql
SELECT e.name, d.dept_name
FROM   employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

### LEFT JOIN

```sql
-- All departments, even with zero employees
SELECT d.dept_name, COUNT(e.emp_id) AS headcount
FROM   departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```

### FULL OUTER JOIN

```sql
SELECT e.name, d.dept_name
FROM   employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id;
-- MySQL lacks FULL OUTER; emulate with UNION of LEFT and RIGHT
```

### SELF Join

**Q: When do you use a self join?**

**A:** When rows in the same table relate to each other — org charts, hierarchies, sequential records.

```sql
-- Employee with their manager's name
SELECT e.name AS employee,
       m.name AS manager
FROM   employees e
LEFT JOIN employees m ON e.manager_id = m.emp_id;
```

```sql
-- Find employees earning more than their manager
SELECT e.name, e.salary, m.name AS manager, m.salary AS mgr_salary
FROM   employees e
JOIN   employees m ON e.manager_id = m.emp_id
WHERE  e.salary > m.salary;
```

### CROSS Join

**Q: What is a cross join?**

**A:** Produces the Cartesian product: every row in A paired with every row in B. `|A| × |B|` rows.

```sql
SELECT e.name, d.dept_name
FROM   employees e
CROSS JOIN departments d;  -- rarely intended; use INNER JOIN with ON instead
```

**Use case:** Generate combinations (all sizes × all colors), or when no join condition exists intentionally.

### Join vs Subquery?

**A:** Often equivalent in result; optimizer may treat them similarly. Prefer JOINs for readability when combining tables; subqueries when filtering or computing intermediate values.

---

## 9. Subqueries & CTEs

### Subquery (nested query)

**Q: What is a subquery?**

**A:** A query nested inside another query — in `WHERE`, `FROM`, `SELECT`, or `HAVING`.

```sql
-- Employees earning above company average
SELECT name, salary
FROM   employees
WHERE  salary > (SELECT AVG(salary) FROM employees);
```

```sql
-- Departments with at least 5 employees
SELECT dept_id
FROM   employees
GROUP BY dept_id
HAVING COUNT(*) >= 5;
```

### Subquery in FROM (derived table)

```sql
SELECT dept_id, avg_sal
FROM (
    SELECT dept_id, AVG(salary) AS avg_sal
    FROM   employees
    GROUP BY dept_id
) dept_avg
WHERE avg_sal > 70000;
```

### Correlated Subquery

**Q: What is a correlated subquery?**

**A:** Inner query references columns from the outer query. Executed once **per outer row** — can be slower than JOINs.

```sql
-- Employees earning more than their department average
SELECT e.name, e.salary, e.dept_id
FROM   employees e
WHERE  e.salary > (
    SELECT AVG(salary)
    FROM   employees
    WHERE  dept_id = e.dept_id   -- correlated reference
);
```

```sql
-- Departments where ALL employees earn > 50k (see ALL section too)
SELECT d.dept_name
FROM   departments d
WHERE  NOT EXISTS (
    SELECT 1 FROM employees e
    WHERE  e.dept_id = d.dept_id AND e.salary <= 50000
);
```

### CTE (Common Table Expression)

**Q: What is a CTE?**

**A:** A named temporary result set defined with `WITH`, readable and reusable within the same query.

```sql
WITH dept_stats AS (
    SELECT dept_id,
           COUNT(*)     AS emp_count,
           AVG(salary)  AS avg_salary
    FROM   employees
    GROUP BY dept_id
)
SELECT d.dept_name, ds.emp_count, ds.avg_salary
FROM   dept_stats ds
JOIN   departments d ON ds.dept_id = d.dept_id
WHERE  ds.avg_salary > 60000;
```

### Recursive CTE

**Q: What is a recursive CTE?**

**A:** A CTE that references itself — used for hierarchies, graphs, date series, bill of materials.

```sql
-- Org chart: all reports under manager 1 (including indirect)
WITH RECURSIVE report_chain AS (
    -- Anchor: direct reports
    SELECT emp_id, name, manager_id, 1 AS level
    FROM   employees
    WHERE  manager_id = 1

    UNION ALL

    -- Recursive: reports of reports
    SELECT e.emp_id, e.name, e.manager_id, rc.level + 1
    FROM   employees e
    JOIN   report_chain rc ON e.manager_id = rc.emp_id
)
SELECT * FROM report_chain;
```

```sql
-- Generate numbers 1 to 10
WITH RECURSIVE nums AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1 FROM nums WHERE n < 10
)
SELECT * FROM nums;
```

**Note:** PostgreSQL/SQL Server use `WITH RECURSIVE`; Oracle uses `CONNECT BY` (legacy) or recursive CTE; MySQL 8+ supports recursive CTEs.

### CTE vs Subquery vs Temp Table?

| | CTE | Subquery | Temp Table |
|---|-----|----------|------------|
| Readability | High | Medium | High for multi-step |
| Reuse in query | Yes (same statement) | Limited | Across statements |
| Materialized | Usually not* | No | Yes |
| Best for | Readable complex queries | Simple nesting | Large intermediate data |

---

## 10. Window Functions

### Q: What is a window function?

**A:** Performs a calculation across a set of rows **related to the current row** without collapsing rows into groups (unlike `GROUP BY`). Uses `OVER (...)`.

### Syntax

```sql
function_name(args) OVER (
    [PARTITION BY column]
    [ORDER BY column]
    [ROWS | RANGE between_clause]
)
```

### ROW_NUMBER, RANK, DENSE_RANK

```sql
SELECT name, dept_id, salary,
    ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rn,
    RANK()       OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rnk,
    DENSE_RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS drnk
FROM employees;
```

| Function | Ties behavior | Gaps after ties? |
|----------|---------------|------------------|
| `ROW_NUMBER()` | Arbitrary unique numbers | N/A |
| `RANK()` | Same rank for ties | Yes (1,1,3) |
| `DENSE_RANK()` | Same rank for ties | No (1,1,2) |

### LEAD & LAG

**Q: What do LEAD and LAG do?**

**A:** Access subsequent (LEAD) or previous (LAG) row values without a self-join.

```sql
SELECT name, hire_date, salary,
    LAG(salary)  OVER (ORDER BY hire_date) AS prev_salary,
    LEAD(salary) OVER (ORDER BY hire_date) AS next_salary,
    salary - LAG(salary) OVER (ORDER BY hire_date) AS raise_amount
FROM employees;
```

### PARTITION BY

**Q: What does PARTITION BY do in window functions?**

**A:** Divides rows into independent groups (like GROUP BY) but **keeps all rows** in the output.

```sql
-- Running total of salary per department
SELECT name, dept_id, salary,
    SUM(salary) OVER (
        PARTITION BY dept_id
        ORDER BY hire_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM employees;
```

### Other useful window functions

```sql
SELECT name, salary,
    NTILE(4)  OVER (ORDER BY salary)          AS quartile,
    FIRST_VALUE(salary) OVER (PARTITION BY dept_id ORDER BY salary DESC) AS top_in_dept,
    AVG(salary) OVER (PARTITION BY dept_id)   AS dept_avg
FROM employees;
```

### Top N per group (classic interview pattern)

```sql
WITH ranked AS (
    SELECT name, dept_id, salary,
           ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rn
    FROM employees
)
SELECT name, dept_id, salary
FROM ranked
WHERE rn <= 3;  -- top 3 earners per department
```

---

## 11. Aggregates, GROUP BY & HAVING

### Aggregate Functions

| Function | Purpose |
|----------|---------|
| `COUNT(*)` | Row count |
| `COUNT(col)` | Non-NULL values in col |
| `SUM(col)` | Total |
| `AVG(col)` | Mean |
| `MIN(col)` / `MAX(col)` | Min / max |
| `STRING_AGG` / `GROUP_CONCAT` | Concatenate strings |

```sql
SELECT dept_id,
       COUNT(*)           AS headcount,
       AVG(salary)        AS avg_sal,
       MAX(salary)        AS max_sal,
       MIN(salary)        AS min_sal
FROM   employees
GROUP BY dept_id;
```

### Q: Can you SELECT non-aggregated columns with GROUP BY?

**A:** Only columns in `GROUP BY` or wrapped in aggregate functions. Otherwise the result is undefined (MySQL permissive mode is an exception).

```sql
-- WRONG (in strict SQL)
SELECT dept_id, name, AVG(salary) FROM employees GROUP BY dept_id;

-- CORRECT
SELECT dept_id, AVG(salary) FROM employees GROUP BY dept_id;
```

### HAVING

```sql
SELECT dept_id, AVG(salary) AS avg_sal
FROM   employees
GROUP BY dept_id
HAVING AVG(salary) > 65000
   AND COUNT(*) >= 3;
```

### Q: WHERE vs HAVING vs GROUP BY order?

See [Query Execution Order](#18-query-execution--optimization).

### FILTER clause (PostgreSQL) / conditional aggregation

```sql
SELECT dept_id,
       COUNT(*) FILTER (WHERE salary > 80000) AS high_earners,
       SUM(CASE WHEN salary > 80000 THEN 1 ELSE 0 END) AS high_earners_std
FROM employees
GROUP BY dept_id;
```

---

## 12. EXISTS, ANY & ALL

### EXISTS

**Q: What does EXISTS do?**

**A:** Returns TRUE if the subquery returns **at least one row**. Stops at first match — often faster than `IN` for large sets.

```sql
-- Departments that have at least one employee
SELECT d.dept_name
FROM   departments d
WHERE  EXISTS (
    SELECT 1 FROM employees e WHERE e.dept_id = d.dept_id
);

-- Employees with no manager (NOT EXISTS pattern)
SELECT name FROM employees e
WHERE NOT EXISTS (
    SELECT 1 FROM employees m WHERE m.emp_id = e.manager_id
);
```

### IN vs EXISTS

```sql
-- Find customers who placed orders
-- IN: good when subquery is small
SELECT * FROM customers
WHERE customer_id IN (SELECT customer_id FROM orders);

-- EXISTS: often better when outer table is small / subquery is correlated
SELECT * FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.customer_id);
```

### ANY (SOME)

```sql
-- Employees earning more than ANY employee in dept 10
SELECT name, salary
FROM   employees
WHERE  salary > ANY (SELECT salary FROM employees WHERE dept_id = 10);
-- Equivalent: salary > MIN(salary in dept 10)
```

### ALL

```sql
-- Employees earning more than ALL employees in dept 10
SELECT name, salary
FROM   employees
WHERE  salary > ALL (SELECT salary FROM employees WHERE dept_id = 10);
-- Equivalent: salary > MAX(salary in dept 10)
```

```sql
-- Departments where every employee earns > 50k
SELECT dept_id
FROM   employees
GROUP BY dept_id
HAVING MIN(salary) > 50000;
```

---

## 13. CASE Expressions

### Simple CASE

```sql
SELECT name, salary,
    CASE dept_id
        WHEN 10 THEN 'Engineering'
        WHEN 20 THEN 'Sales'
        ELSE 'Other'
    END AS department_label
FROM employees;
```

### Searched CASE

```sql
SELECT name, salary,
    CASE
        WHEN salary >= 100000 THEN 'Senior'
        WHEN salary >= 70000  THEN 'Mid'
        ELSE 'Junior'
    END AS band
FROM employees;
```

### Pivot-style aggregation with CASE

```sql
SELECT dept_id,
    SUM(CASE WHEN salary < 60000 THEN 1 ELSE 0 END) AS junior_count,
    SUM(CASE WHEN salary >= 60000 AND salary < 90000 THEN 1 ELSE 0 END) AS mid_count,
    SUM(CASE WHEN salary >= 90000 THEN 1 ELSE 0 END) AS senior_count
FROM employees
GROUP BY dept_id;
```

### Q: CASE vs COALESCE vs IFNULL?

```sql
SELECT COALESCE(manager_id, 0) AS mgr;           -- first non-NULL
SELECT IFNULL(manager_id, 0) AS mgr;             -- MySQL/SQL Server
SELECT NULLIF(salary, 0) AS salary;              -- NULL if salary = 0
```

---

## 14. Views, Procedures, Functions & Triggers

### Views

**Q: What is a view?**

**A:** A virtual table defined by a stored SELECT. No data duplication (usually); simplifies complex queries and restricts column access.

```sql
CREATE VIEW v_active_employees AS
SELECT emp_id, name, salary, dept_id
FROM   employees
WHERE  hire_date >= '2020-01-01';

SELECT * FROM v_active_employees WHERE dept_id = 10;
```

**Materialized view** (PostgreSQL, Oracle): physically stores results; must be refreshed.

```sql
CREATE MATERIALIZED VIEW mv_dept_summary AS
SELECT dept_id, COUNT(*) AS cnt, AVG(salary) AS avg_sal
FROM employees GROUP BY dept_id;
REFRESH MATERIALIZED VIEW mv_dept_summary;
```

### Stored Procedures

**Q: What is a stored procedure?**

**A:** Precompiled SQL logic stored in the DB — can have parameters, loops, conditionals. Called with `CALL` / `EXEC`.

```sql
-- SQL Server example
CREATE PROCEDURE give_raise @emp_id INT, @pct DECIMAL(5,2)
AS
BEGIN
    UPDATE employees
    SET salary = salary * (1 + @pct / 100)
    WHERE emp_id = @emp_id;
END;

EXEC give_raise @emp_id = 5, @pct = 10;
```

### Functions

**Q: Procedure vs function?**

| | Stored Procedure | Function |
|---|------------------|----------|
| Returns value | Optional (OUT params) | Must return a value |
| Use in SELECT | No | Yes |
| DML allowed | Yes | Usually read-only (varies) |

```sql
-- PostgreSQL
CREATE FUNCTION dept_avg_salary(p_dept_id INT)
RETURNS DECIMAL AS $$
    SELECT AVG(salary) FROM employees WHERE dept_id = p_dept_id;
$$ LANGUAGE SQL;

SELECT dept_avg_salary(10);
```

### Triggers

**Q: What is a trigger?**

**A:** Code that runs automatically on INSERT, UPDATE, or DELETE (BEFORE/AFTER).

```sql
CREATE TRIGGER trg_audit_salary
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    IF OLD.salary <> NEW.salary THEN
        INSERT INTO salary_audit (emp_id, old_sal, new_sal, changed_at)
        VALUES (NEW.emp_id, OLD.salary, NEW.salary, NOW());
    END IF;
END;
```

**Interview tip:** Triggers add hidden complexity and can hurt performance — use judiciously.

---

## 15. Transactions & ACID

### Q: What is a transaction?

**A:** A logical unit of work — either all statements succeed (`COMMIT`) or all are undone (`ROLLBACK`).

```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;
```

### ACID Properties

| Property | Meaning | Example |
|----------|---------|---------|
| **Atomicity** | All or nothing | Transfer: debit + credit both happen or neither |
| **Consistency** | DB moves from valid state to valid state | Constraints never violated after commit |
| **Isolation** | Concurrent transactions don't interfere improperly | Two transfers don't corrupt balance |
| **Durability** | Committed data survives crashes | WAL/redo logs persist changes |

### Isolation Levels

| Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|-------|------------|---------------------|--------------|
| READ UNCOMMITTED | Possible | Possible | Possible |
| READ COMMITTED | No | Possible | Possible |
| REPEATABLE READ | No | No | Possible* |
| SERIALIZABLE | No | No | No |

*MySQL InnoDB REPEATABLE READ also prevents phantoms via MVCC/gap locks.

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

### Q: What is a deadlock?

**A:** Two transactions each hold a lock the other needs. DB kills one transaction (victim) and rolls it back.

---

## 16. Normalization & Denormalization

### Q: Why normalize?

**A:** Reduce redundancy, avoid update/insert/delete anomalies, improve data integrity.

### Normal Forms

| NF | Rule | Fix example |
|----|------|-------------|
| **1NF** | Atomic values; no repeating groups | Split `phone1, phone2` → separate rows or phone table |
| **2NF** | 1NF + no partial dependency on composite PK | Move non-key attrs depending on part of PK to separate table |
| **3NF** | 2NF + no transitive dependency | Move `dept_name` out of employees → departments table |
| **BCNF** | Every determinant is a candidate key | Split when non-key determines part of key |

### Denormalization

**Q: When do you denormalize?**

**A:** When read performance matters more than write consistency — reporting, analytics, caching aggregates.

```sql
-- Denormalized: store dept_name on every employee row (faster reads, stale risk)
-- Normalized: JOIN departments for dept_name (slower read, single source of truth)
```

**Trade-offs:**

| Normalize | Denormalize |
|-----------|-------------|
| Less redundancy | Faster reads |
| Safer updates | Fewer JOINs |
| More JOINs | Risk of inconsistency |

---

## 17. Indexes

### Q: What is an index?

**A:** A data structure (usually B-Tree) that speeds up lookups at the cost of extra storage and slower writes.

```sql
CREATE INDEX idx_emp_dept ON employees(dept_id);
CREATE INDEX idx_emp_name_salary ON employees(name, salary);  -- composite
```

### Clustered Index

**Q: What is a clustered index?**

**A:** Determines the **physical order** of table data. Only **one** per table (usually the primary key).

- **SQL Server:** PK creates clustered index by default
- **MySQL InnoDB:** PK is clustered; secondary indexes store PK pointer
- **PostgreSQL:** No clustered index (uses heap); `CLUSTER` command reorders physically

### Non-Clustered Index

**Q: What is a non-clustered index?**

**A:** Separate structure with pointers to data rows. A table can have many non-clustered indexes.

### Index types

| Type | Best for |
|------|----------|
| B-Tree (default) | Range queries, equality, sorting |
| Hash | Equality only (PostgreSQL, MySQL MEMORY) |
| Full-text | Text search |
| Composite | Multi-column WHERE / ORDER BY |
| Covering index | Query answered entirely from index (INCLUDE cols) |

```sql
-- Covering index (SQL Server)
CREATE INDEX idx_cover ON employees(dept_id) INCLUDE (name, salary);
```

### When NOT to index

- Small tables
- Columns with low cardinality (e.g., boolean gender) unless highly selective filters
- Tables with heavy write load
- Columns rarely in WHERE/JOIN/ORDER BY

### Q: What is index selectivity?

**A:** Ratio of distinct values to total rows. High selectivity (e.g., email) = good index candidate.

---

## 18. Query Execution & Optimization

### Logical Query Execution Order

**Q: What order does SQL logically execute clauses?**

```
1. FROM (+ JOINs)
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT  (including DISTINCT, window functions)
6. ORDER BY
7. LIMIT / OFFSET
```

**Not the written order!** This explains why you cannot use a SELECT alias in WHERE:

```sql
-- ERROR: alias not visible in WHERE
SELECT salary * 12 AS annual FROM employees WHERE annual > 100000;

-- FIX: repeat expression or use subquery/CTE
SELECT annual FROM (
    SELECT salary * 12 AS annual FROM employees
) t WHERE annual > 100000;
```

### Query Optimization Tips

1. **Index** columns in WHERE, JOIN, ORDER BY
2. **Avoid** `SELECT *` — fetch only needed columns
3. **Replace** correlated subqueries with JOINs when possible
4. **Use EXPLAIN** / execution plans
5. **Avoid** functions on indexed columns: `WHERE YEAR(hire_date) = 2024` → use range
6. **Limit** early when possible
7. **Use EXISTS** over `IN` for large subqueries
8. **Batch** large UPDATEs/DELETEs

### Execution Plan

**Q: How do you read an execution plan?**

```sql
EXPLAIN ANALYZE SELECT * FROM employees WHERE dept_id = 10;  -- PostgreSQL
EXPLAIN SELECT * FROM employees WHERE dept_id = 10;        -- MySQL
SET SHOWPLAN_TEXT ON; GO                                    -- SQL Server
```

**Look for:**
- **Seq Scan / Table Scan** — full table read (bad on large tables)
- **Index Scan / Index Seek** — using index (good)
- **Nested Loop** — good for small sets
- **Hash Join / Merge Join** — large joins
- **High cost** nodes — optimization targets
- **Rows estimate vs actual** — stale statistics?

---

## 19. Pagination

### OFFSET pagination (simple, slow on large offsets)

```sql
SELECT * FROM employees
ORDER BY emp_id
LIMIT 10 OFFSET 20;  -- page 3, size 10
```

**Problem:** `OFFSET 1000000` still scans/skips a million rows.

### Keyset (cursor) pagination (preferred at scale)

```sql
-- First page
SELECT * FROM employees ORDER BY emp_id LIMIT 10;

-- Next page (last seen emp_id = 10)
SELECT * FROM employees
WHERE emp_id > 10
ORDER BY emp_id
LIMIT 10;
```

### Pagination with tie-breaker

```sql
SELECT * FROM employees
WHERE (hire_date, emp_id) > ('2023-01-15', 42)
ORDER BY hire_date, emp_id
LIMIT 10;
```

---

## 20. Common Coding Questions

### Q1: Find duplicate emails

```sql
SELECT email, COUNT(*) AS cnt
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

### Q2: Delete duplicates keeping one row

```sql
-- Using ROW_NUMBER
WITH dupes AS (
    SELECT emp_id,
           ROW_NUMBER() OVER (PARTITION BY email ORDER BY emp_id) AS rn
    FROM employees
)
DELETE FROM employees
WHERE emp_id IN (SELECT emp_id FROM dupes WHERE rn > 1);
```

### Q3: Second highest salary

```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);

-- Or with DENSE_RANK
WITH r AS (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS dr
    FROM employees
)
SELECT DISTINCT salary FROM r WHERE dr = 2;
```

### Q4: Nth highest salary

```sql
SELECT DISTINCT salary
FROM employees e
WHERE N = (
    SELECT COUNT(DISTINCT salary) FROM employees
    WHERE salary >= e.salary
);
-- Replace N with desired rank
```

### Q5: Employees with no orders

```sql
SELECT c.*
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.order_id IS NULL;
```

### Q6: Running total

```sql
SELECT order_date, amount,
    SUM(amount) OVER (ORDER BY order_date) AS running_total
FROM orders;
```

### Q7: Month-over-month growth

```sql
WITH monthly AS (
    SELECT DATE_TRUNC('month', order_date) AS month,
           SUM(amount) AS revenue
    FROM orders
    GROUP BY 1
)
SELECT month, revenue,
    LAG(revenue) OVER (ORDER BY month) AS prev_revenue,
    ROUND(100.0 * (revenue - LAG(revenue) OVER (ORDER BY month))
          / LAG(revenue) OVER (ORDER BY month), 2) AS pct_growth
FROM monthly;
```

### Q8: Consecutive login days (streak)

```sql
WITH dated AS (
    SELECT user_id, login_date,
           login_date - ROW_NUMBER() OVER (
               PARTITION BY user_id ORDER BY login_date
           )::INT AS grp
    FROM logins
)
SELECT user_id, MIN(login_date) AS streak_start,
       MAX(login_date) AS streak_end, COUNT(*) AS streak_len
FROM dated
GROUP BY user_id, grp
HAVING COUNT(*) >= 3;
```

### Q9: Pivot — rows to columns

```sql
SELECT dept_id,
    MAX(CASE WHEN YEAR(hire_date) = 2022 THEN salary END) AS sal_2022,
    MAX(CASE WHEN YEAR(hire_date) = 2023 THEN salary END) AS sal_2023
FROM employees
GROUP BY dept_id;
```

### Q10: Find gaps in sequential IDs

```sql
SELECT id + 1 AS gap_start, next_id - 1 AS gap_end
FROM (
    SELECT id, LEAD(id) OVER (ORDER BY id) AS next_id
    FROM sequence_table
) t
WHERE next_id - id > 1;
```

---

## 21. Top Interview SQL Problems

### 1. Rank employees by salary within department

```sql
SELECT name, dept_id, salary,
       DENSE_RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS sal_rank
FROM employees;
```

### 2. Department with highest average salary

```sql
SELECT dept_id
FROM employees
GROUP BY dept_id
ORDER BY AVG(salary) DESC
LIMIT 1;
```

### 3. Customers who bought all products

```sql
SELECT customer_id
FROM orders
GROUP BY customer_id
HAVING COUNT(DISTINCT product_id) = (SELECT COUNT(*) FROM products);
```

### 4. Median salary per department

```sql
SELECT dept_id, AVG(salary) AS median_salary
FROM (
    SELECT dept_id, salary,
           ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary) AS rn,
           COUNT(*)    OVER (PARTITION BY dept_id) AS cnt
    FROM employees
) t
WHERE rn IN (FLOOR((cnt + 1) / 2.0), CEIL((cnt + 1) / 2.0))
GROUP BY dept_id;
```

### 5. Self-join: find pairs with same salary

```sql
SELECT a.name, b.name, a.salary
FROM employees a
JOIN employees b ON a.salary = b.salary AND a.emp_id < b.emp_id;
```

### 6. Rolling 7-day average

```sql
SELECT order_date, amount,
    AVG(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS rolling_7d_avg
FROM orders;
```

### 7. Exchange seats (LeetCode 626)

```sql
SELECT CASE
    WHEN id = (SELECT MAX(id) FROM seat) AND id % 2 = 1 THEN id
    WHEN id % 2 = 1 THEN id + 1
    ELSE id - 1
END AS id, student
FROM seat
ORDER BY id;
```

### 8. Department top 3 salaries (LeetCode 185)

```sql
WITH ranked AS (
    SELECT d.name AS Department, e.name AS Employee, e.salary,
           DENSE_RANK() OVER (PARTITION BY e.dept_id ORDER BY e.salary DESC) AS rk
    FROM employees e
    JOIN departments d ON e.dept_id = d.dept_id
)
SELECT Department, Employee, salary
FROM ranked WHERE rk <= 3;
```

### 9. Delete duplicate rows

```sql
DELETE e1 FROM employees e1
JOIN employees e2
  ON e1.email = e2.email AND e1.emp_id > e2.emp_id;
```

### 10. Cumulative distinct count

```sql
SELECT order_date, product_id,
    COUNT(DISTINCT product_id) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS cumulative_distinct_products
FROM orders;
```

---

## 22. Scenario Questions

### Scenario 1: Slow query on production

**Q: A `SELECT` on a 50M-row table is slow. How do you investigate?**

**A:**
1. Get the exact query and `EXPLAIN ANALYZE` output
2. Check for full table scans — add/fix indexes on filter/join columns
3. Check SELECT list — avoid `SELECT *`
4. Verify statistics are up to date (`ANALYZE` / `UPDATE STATISTICS`)
5. Check for implicit conversions, functions on indexed columns
6. Consider partitioning, archiving old data, read replicas for reporting

---

### Scenario 2: Prevent double-spending

**Q: How do you safely transfer money between accounts?**

**A:** Use a transaction with row-level locking:

```sql
BEGIN;
SELECT balance FROM accounts WHERE id = 1 FOR UPDATE;
SELECT balance FROM accounts WHERE id = 2 FOR UPDATE;

UPDATE accounts SET balance = balance - 100 WHERE id = 1 AND balance >= 100;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

COMMIT;
```

---

### Scenario 3: Soft delete vs hard delete

**Q: When would you use soft delete?**

**A:** When audit trail or recovery is needed. Add `deleted_at TIMESTAMP`; filter `WHERE deleted_at IS NULL`. Trade-off: unique constraints and queries become more complex.

```sql
ALTER TABLE employees ADD COLUMN deleted_at TIMESTAMP NULL;
SELECT * FROM employees WHERE deleted_at IS NULL;
```

---

### Scenario 4: Schema migration without downtime

**A:**
1. Add new column (nullable)
2. Backfill in batches
3. Dual-write in application
4. Switch reads to new column
5. Add NOT NULL + constraints
6. Drop old column

---

### Scenario 5: Find fraudulent duplicate transactions

```sql
SELECT customer_id, amount, order_date, COUNT(*) AS txn_count
FROM orders
WHERE order_date >= CURRENT_DATE - INTERVAL '1' DAY
GROUP BY customer_id, amount, order_date
HAVING COUNT(*) > 3;
```

---

### Scenario 6: Design a URL shortener schema

```sql
CREATE TABLE urls (
    id          BIGSERIAL PRIMARY KEY,
    short_code  VARCHAR(10) UNIQUE NOT NULL,
    long_url    TEXT NOT NULL,
    created_at  TIMESTAMP DEFAULT NOW(),
    expires_at  TIMESTAMP
);

CREATE INDEX idx_short_code ON urls(short_code);

CREATE TABLE clicks (
    id         BIGSERIAL PRIMARY KEY,
    url_id     BIGINT REFERENCES urls(id),
    clicked_at TIMESTAMP DEFAULT NOW(),
    ip_address INET
);
```

---

### Scenario 7: Handle hierarchical categories

**A:** Use **adjacency list** (`parent_id`), **closure table**, or **recursive CTE** for queries. Materialized path (`/1/5/12/`) speeds reads but complicates moves.

---

### Scenario 8: Reporting DB vs production DB

**A:** Use read replica, ETL to warehouse, materialized views, or event streaming (CDC). Never run heavy analytics on primary OLTP.

---

## 23. Cheat Sheet

### SQL Command Categories

```
DDL: CREATE, ALTER, DROP, TRUNCATE
DML: SELECT, INSERT, UPDATE, DELETE, MERGE
DCL: GRANT, REVOKE
TCL: COMMIT, ROLLBACK, SAVEPOINT
```

### Joins at a glance

```
INNER     → intersection only
LEFT      → all left + match right
RIGHT     → all right + match left
FULL      → union of both
CROSS     → A × B
SELF      → table joined to itself
```

### Keys

```
Primary Key    → unique identifier (1 per table)
Foreign Key    → references another table's PK
Unique Key     → no duplicates (multiple per table)
Composite Key  → multi-column key
Candidate Key  → could be PK
Super Key      → uniquely identifies (may have extras)
Alternate Key  → candidate key not chosen as PK
```

### NULL rules

```
IS NULL / IS NOT NULL
COALESCE(a, b, 0)
NULL in comparisons → UNKNOWN (filtered out by WHERE)
COUNT(*) counts rows; COUNT(col) skips NULLs
```

### Aggregates + filters

```
WHERE   → filter rows (before group)
GROUP BY → collapse rows
HAVING  → filter groups (after group)
```

### Window functions

```
ROW_NUMBER()  → unique 1,2,3,4
RANK()        → ties, gaps: 1,1,3,4
DENSE_RANK()  → ties, no gaps: 1,1,2,3
LAG/LEAD      → prev/next row
PARTITION BY  → group without collapsing
ORDER BY      → define window frame
```

### Subquery patterns

```
IN (subquery)           → membership
EXISTS (subquery)       → semi-join (often faster)
NOT EXISTS              → anti-join
> ANY / > ALL           → compare to some/every row
Correlated              → inner refs outer column
```

### Index quick reference

```
Clustered     → 1 per table, physical order (SQL Server PK)
Non-clustered → many allowed, pointer to data
Composite     → multi-column index (leftmost prefix rule)
Covering      → index contains all queried columns
```

### ACID

```
Atomicity     → all or nothing
Consistency   → valid state to valid state
Isolation     → concurrent txn separation
Durability    → survives crash after commit
```

### Normal forms

```
1NF → atomic values
2NF → no partial key dependency
3NF → no transitive dependency
BCNF → every determinant is candidate key
```

### Query execution order

```
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → DISTINCT
→ WINDOW → ORDER BY → LIMIT
```

### Pagination

```
OFFSET/LIMIT     → simple, slow at high offset
Keyset/cursor    → WHERE id > last_id ORDER BY id LIMIT n
```

### Performance checklist

```
□ EXPLAIN the query
□ Index WHERE/JOIN/ORDER BY columns
□ Avoid SELECT *
□ Avoid functions on indexed columns
□ Prefer EXISTS over IN (large sets)
□ Use keyset pagination at scale
□ Keep statistics updated
```

### DELETE vs TRUNCATE vs DROP

```
DELETE    → row-by-row, rollback OK, has WHERE
TRUNCATE  → all rows fast, resets identity, DDL
DROP      → removes table object
```

### Common interview one-liners

| Question | Answer |
|----------|--------|
| Clustered vs non-clustered? | Clustered = physical order, one per table |
| WHERE vs HAVING? | WHERE = rows; HAVING = groups |
| UNION vs UNION ALL? | UNION removes dupes; ALL keeps all |
| CHAR vs VARCHAR? | CHAR fixed length; VARCHAR variable |
| DELETE vs TRUNCATE? | DELETE is DML + WHERE; TRUNCATE is DDL all rows |
| 1NF example violation? | Multiple phone numbers in one column |
| Why denormalize? | Read performance, fewer JOINs in analytics |
| What causes deadlock? | Circular lock wait between transactions |
| Covering index? | Index alone satisfies query — no table lookup |

### UNION

```sql
SELECT name FROM employees WHERE dept_id = 10
UNION                          -- removes duplicates
SELECT name FROM contractors WHERE dept_id = 10;

-- UNION ALL → faster, keeps duplicates
```

### Date arithmetic (portable patterns)

```sql
-- Last 30 days
WHERE order_date >= CURRENT_DATE - INTERVAL '30' DAY

-- This month
WHERE DATE_TRUNC('month', order_date) = DATE_TRUNC('month', CURRENT_DATE)
```

---

## Quick Revision Checklist

- [ ] Explain ACID and isolation levels
- [ ] Write INNER/LEFT/SELF JOIN from memory
- [ ] Solve top-N-per-group with `ROW_NUMBER`
- [ ] Explain correlated subquery vs JOIN
- [ ] Write a recursive CTE for hierarchy
- [ ] Explain clustered vs non-clustered index
- [ ] State logical query execution order
- [ ] Solve second/Nth highest salary
- [ ] Explain 1NF through 3NF with examples
- [ ] Read a basic EXPLAIN plan

---

*Last updated: June 2026 — dialect notes included for PostgreSQL, MySQL, and SQL Server where behavior differs.*
