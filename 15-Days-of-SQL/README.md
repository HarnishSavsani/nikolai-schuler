# SQL Revision Guide for PostgreSQL 📚

A concise, interactive guide for last-minute SQL prep in PostgreSQL! 🚀 Each topic is organized with general syntax, a single example in a collapsible section, and tables for functions. Let’s ace your SQL prep! 💪

---

## Table of Contents

1. [Basic Queries](#basic-queries)
2. [Aggregate Functions](#aggregate-functions)
3. [String Functions](#string-functions)
4. [Date and Time Functions](#date-and-time-functions)
5. [Math Functions](#math-functions)
6. [Conditional Expressions](#conditional-expressions)
7. [Joins](#joins)
8. [Set Operations](#set-operations)
9. [Subqueries](#subqueries)
10. [Database and Table Management](#database-and-table-management)
11. [Views and Materialized Views](#views-and-materialized-views)
12. [Window Functions](#window-functions)
13. [Advanced Grouping](#advanced-grouping)
14. [Special Joins](#special-joins)
15. [Functions and Transactions](#functions-and-transactions)
16. [User Management](#user-management)
17. [Indexes](#indexes)
18. [Common Table Expressions (CTEs)](#common-table-expressions-ctes)

---

## Basic Queries 📝

### SELECT
- **Syntax**: `SELECT column1, column2 FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT name, age 
FROM users;
```
</details>

### ORDER BY
- **Syntax**: `SELECT column FROM table_name ORDER BY column [ASC|DESC];`

<details><summary>Example</summary>

```sql
SELECT name, salary 
FROM employees 
ORDER BY salary DESC;
```
</details>

### DISTINCT
- **Syntax**: `SELECT DISTINCT column FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT DISTINCT department 
FROM employees;
```
</details>

### LIMIT
- **Syntax**: `SELECT column FROM table_name LIMIT n;`

<details><summary>Example</summary>

```sql
SELECT name 
FROM products LIMIT 5;
```
</details>

### WHERE
- **Syntax**: `SELECT column FROM table_name WHERE condition;`

<details><summary>Example</summary>

```sql
SELECT name 
FROM customers WHERE age > 30;
```
</details>

### BETWEEN ... AND
- **Syntax**: `SELECT column FROM table_name WHERE column BETWEEN value1 AND value2;`

<details><summary>Example</summary>

```sql
SELECT product_name 
FROM products 
WHERE price BETWEEN 10 AND 50;
```
</details>

### IN
- **Syntax**: `SELECT column FROM table_name WHERE column IN (value1, value2, ...);`

<details><summary>Example</summary>

```sql
SELECT name 
FROM employees 
WHERE department IN ('HR', 'IT');
```
</details>

### LIKE
- **Syntax**: `SELECT column FROM table_name WHERE column LIKE 'pattern';`

<details><summary>Example</summary>

```sql
SELECT name 
FROM customers 
WHERE name LIKE 'J%';
```
</details>

---

## Aggregate Functions 📊

### SUM
- **Syntax**: `SELECT SUM(column) FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT SUM(salary) 
FROM employees;
```
</details>

### AVG
- **Syntax**: `SELECT AVG(column) FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT AVG(price) 
FROM products;
```
</details>

### MIN
- **Syntax**: `SELECT MIN(column) FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT MIN(salary) 
FROM employees;
```
</details>

### MAX
- **Syntax**: `SELECT MAX(column) FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT MAX(price) 
FROM products;
```
</details>

### COUNT
- **Syntax**: `SELECT COUNT(column) FROM table_name;`

<details><summary>Example</summary>

```sql
SELECT COUNT(*) 
FROM orders;
```
</details>

### GROUP BY
- **Syntax**: `SELECT column, AGG_FUNC(column) FROM table_name GROUP BY column;`

<details><summary>Example</summary>

```sql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department;
```
</details>

### GROUP BY (Multi-Column)
- **Syntax**: `SELECT column1, column2, AGG_FUNC(column) FROM table_name GROUP BY column1, column2;`

<details><summary>Example</summary>

```sql
SELECT department, job_title, AVG(salary) 
FROM employees 
GROUP BY department, job_title;
```
</details>

### HAVING
- **Syntax**: `SELECT column, AGG_FUNC(column) FROM table_name GROUP BY column HAVING condition;`

<details><summary>Example</summary>

```sql
SELECT department, AVG(salary) 
FROM employees 
GROUP BY department 
HAVING AVG(salary) > 60000;
```
</details>

---

## String Functions 🧵

| Function       | Use                    | Example Use                     |
|----------------|------------------------|---------------------------------|
| `UPPER`        | Convert to uppercase   | `UPPER('hello')` → 'HELLO'      |
| `LOWER`        | Convert to lowercase   | `LOWER('HELLO')` → 'hello'      |
| `LENGTH`       | String length          | `LENGTH('hello')` → 5           |
| `LEFT`         | Extract left chars     | `LEFT('hello', 2)` → 'he'       |
| `RIGHT`        | Extract right chars    | `RIGHT('hello', 2)` → 'lo'      |
| `\|\|`           | Concatenate strings    | `'hi' \|\| ' there'` → 'hi there' |
| `POSITION`     | Find substring position| `POSITION('l' IN 'hello')` → 3  |
| `SUBSTRING`    | Extract substring      | `SUBSTRING('hello' FROM 2 FOR 3)` → 'ell' |

<details><summary>Example</summary>

```sql
SELECT UPPER(name) || ' (' || LENGTH(name) || ')' 
FROM employees;
```
</details>

---

## Date and Time Functions ⏰

### EXTRACT
- **Syntax**: `EXTRACT(unit FROM date)` (Units: `DAY`, `DOW`, `DOY`, `HOUR`, `MONTH`, `QUARTER`, `WEEK`, `YEAR`, `MINUTE`, `SECOND`)

<details><summary>Example</summary>

```sql
SELECT EXTRACT(MONTH FROM order_date) 
FROM orders;
```
</details>

### TO_CHAR
| Format   | Use                      | Example Use                     |
|----------|--------------------------|---------------------------------|
| `HH`     | Hour (01-12)            | `TO_CHAR(ts, 'HH')` → '10'      |
| `HH12`   | Hour (01-12)            | `TO_CHAR(ts, 'HH12')` → '10'    |
| `HH24`   | Hour (00-23)            | `TO_CHAR(ts, 'HH24')` → '22'    |
| `MI`     | Minute                  | `TO_CHAR(ts, 'MI')` → '45'      |
| `SS`     | Second                  | `TO_CHAR(ts, 'SS')` → '30'      |
| `YYYY`   | Four-digit year         | `TO_CHAR(ts, 'YYYY')` → '2025'  |
| `YY`     | Two-digit year          | `TO_CHAR(ts, 'YY')` → '25'      |
| `MONTH`  | Full month name (upper) | `TO_CHAR(ts, 'MONTH')` → 'JUNE' |
| `month`  | Full month name (lower) | `TO_CHAR(ts, 'month')` → 'june' |
| `Month`  | Full month name (title) | `TO_CHAR(ts, 'Month')` → 'June' |
| `MON`    | Abbr. month (upper)     | `TO_CHAR(ts, 'MON')` → 'JUN'    |
| `Mon`    | Abbr. month (title)     | `TO_CHAR(ts, 'Mon')` → 'Jun'    |
| `mon`    | Abbr. month (lower)     | `TO_CHAR(ts, 'mon')` → 'jun'    |
| `DAY`    | Full day name (upper)   | `TO_CHAR(ts, 'DAY')` → 'FRIDAY' |
| `Day`    | Full day name (title)   | `TO_CHAR(ts, 'Day')` → 'Friday' |
| `day`    | Full day name (lower)   | `TO_CHAR(ts, 'day')` → 'friday' |
| `Dy`     | Abbr. day (title)       | `TO_CHAR(ts, 'Dy')` → 'Fri'     |
| `dy`     | Abbr. day (lower)       | `TO_CHAR(ts, 'dy')` → 'fri'     |

<details><summary>Example</summary>

```sql
SELECT TO_CHAR(CURRENT_TIMESTAMP, 'Mon-DD-YYYY HH24:MI');
```
</details>

### INTERVAL, TIMESTAMP, CURRENT_DATE, CURRENT_TIMESTAMP
- **Syntax**: `CURRENT_DATE`, `CURRENT_TIMESTAMP`, `timestamp + INTERVAL 'value unit'`

<details><summary>Example</summary>

```sql
SELECT CURRENT_TIMESTAMP + INTERVAL '1 day';
```
</details>

---

## Math Functions 🔢

| Function   | Use                | Example Use         |
|------------|--------------------|---------------------|
| `+`        | Addition           | `5 + 3` → 8        |
| `-`        | Subtraction        | `5 - 3` → 2        |
| `*`        | Multiplication     | `5 * 3` → 15       |
| `/`        | Division           | `6 / 2` → 3        |
| `%`        | Modulus            | `7 % 2` → 1        |
| `^`        | Exponentiation     | `2 ^ 3` → 8        |
| `ABS`      | Absolute value     | `ABS(-5)` → 5      |
| `ROUND`    | Round number       | `ROUND(3.56)` → 4  |
| `CEILING`  | Round up           | `CEILING(3.1)` → 4 |
| `FLOOR`    | Round down         | `FLOOR(3.9)` → 3   |

<details><summary>Example</summary>

```sql
SELECT ROUND(price * 1.1, 2) 
FROM products;
```
</details>

---

## Conditional Expressions 🤔

### CASE WHEN
- **Syntax**: `CASE WHEN condition THEN result [ELSE result] END`

<details><summary>Example</summary>

```sql
SELECT name, 
CASE 
    WHEN salary > 50000 THEN 'High' 
    ELSE 'Low' 
END AS salary_level 
FROM employees;
```
</details>

### CASE WHEN with SUM
- **Syntax**: `SUM(CASE WHEN condition THEN value ELSE 0 END)`

<details><summary>Example</summary>

```sql
SELECT 
SUM(
    CASE 
        WHEN department = 'IT' THEN salary 
        ELSE 0 
    END) AS it_salary 
FROM employees;
```
</details>

### COALESCE
- **Syntax**: `COALESCE(value1, value2, ...)`

<details><summary>Example</summary>

```sql
SELECT COALESCE(phone, 'N/A') 
FROM employees;
```
</details>

### CAST
- **Syntax**: `CAST(value AS type)`

<details><summary>Example</summary>

```sql
SELECT CAST(age AS TEXT) 
FROM employees;
```
</details>

### REPLACE
- **Syntax**: `REPLACE(string, old, new)`

<details><summary>Example</summary>

```sql
SELECT REPLACE(name, 'John', 'Jon') 
FROM employees;
```
</details>

---

## Joins 🤝

### INNER JOIN
- **Venn Diagram Description**: Returns only the overlapping rows where both tables match (like the intersection of two circles).
- **Syntax**: `SELECT columns FROM table1 INNER JOIN table2 ON condition;`

<details><summary>Example</summary>

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.id;
```
</details>

### LEFT OUTER JOIN
- **Venn Diagram Description**: Returns all rows from the left table, plus matched rows from the right table (left circle fully included, right circle partially if matched, otherwise NULL).
- **Syntax**: `SELECT columns FROM table1 LEFT OUTER JOIN table2 ON condition;`

<details><summary>Example</summary>

```sql
SELECT e.name, d.department_name
FROM employees e
LEFT OUTER JOIN departments d ON e.department_id = d.id;
```
</details>

### RIGHT OUTER JOIN
- **Venn Diagram Description**: Returns all rows from the right table, plus matched rows from the left table (right circle fully included, left circle partially if matched, otherwise NULL).
- **Syntax**: `SELECT columns FROM table1 RIGHT OUTER JOIN table2 ON condition;`

<details><summary>Example</summary>

```sql
SELECT e.name, d.department_name
FROM employees e
RIGHT OUTER JOIN departments d ON e.department_id = d.id;
```
</details>

### FULL OUTER JOIN
- **Venn Diagram Description**: Returns all rows from both tables, with matches where available (full union of both circles, with NULLs for non-matching rows).
- **Special Case**: Includes rows from either table even if the other table has no match (NULLs appear).
- **Syntax**: `SELECT columns FROM table1 FULL OUTER JOIN table2 ON condition;`

<details><summary>Example</summary>

```sql
SELECT e.name, d.department_name
FROM employees e
FULL OUTER JOIN departments d ON e.department_id = d.id;
```
</details>

---

## Set Operations 🧩

### UNION
- **Syntax**: `SELECT column FROM table1 UNION SELECT column FROM table2;`

<details><summary>Example</summary>

```sql
SELECT name FROM employees 
UNION 
SELECT name FROM contractors;
```
</details>

### UNION ALL
- **Syntax**: `SELECT column FROM table1 UNION ALL SELECT column FROM table2;`

<details><summary>Example</summary>

```sql
SELECT name FROM employees 
UNION ALL 
SELECT name FROM contractors;
```
</details>

---

## Subqueries 🔍

### Subquery in WHERE
- **Syntax**: `SELECT column FROM table_name WHERE column [op] (SELECT ...);`
- **Tip**: Use when filtering based on a condition from another query.

<details><summary>Example</summary>

```sql
SELECT name 
FROM employees 
WHERE department_id IN (SELECT id 
                        FROM departments 
                        WHERE location = 'NY');
```
</details>

### Subquery in FROM
- **Syntax**: `SELECT column FROM (SELECT ...) AS subquery;`
- **Tip**: Use to treat a query result as a temporary table.

<details><summary>Example</summary>

```sql
SELECT avg_salary 
FROM (SELECT AVG(salary) AS avg_salary 
      FROM employees 
      GROUP BY department) AS dept_avg;
```
</details>

### Subquery in SELECT
- **Syntax**: `SELECT column, (SELECT ...) FROM table_name;`
- **Tip**: Use to compute a value for each row.

<details><summary>Example</summary>

```sql
SELECT name, 
(SELECT AVG(salary) 
FROM employees) AS avg_salary 
FROM employees;
```
</details>

### Correlated Subquery in WHERE
- **Syntax**: `SELECT column FROM table_name WHERE [op] (SELECT ... WHERE condition);`
- **Tip**: Use when the subquery depends on the outer query’s row.

<details><summary>Example</summary>

```sql
SELECT name 
FROM employees e 
WHERE EXISTS (SELECT 1 
              FROM departments d 
              WHERE d.id = e.department_id);
```
</details>

### Correlated Subquery in SELECT
- **Syntax**: `SELECT column, (SELECT ... WHERE condition) FROM table_name;`
- **Tip**: Use to compute a per-row value based on another table.

<details><summary>Example</summary>

```sql
SELECT name, 
(SELECT department_name 
FROM departments d 
WHERE d.id = e.department_id) AS dept 
FROM employees e;
```
</details>

---

## Database and Table Management 🛠️

### CREATE DATABASE
- **Syntax**: `CREATE DATABASE db_name [WITH ENCODING 'encoding'];`

<details><summary>Example</summary>

```sql
CREATE DATABASE mydb WITH ENCODING 'UTF8';
```
</details>

### Data Types
- **Numeric**: `INT`, `SMALLINT`, `BIGINT`, `NUMERIC`, `SERIAL`
- **String**: `VARCHAR(n)`, `CHAR(n)`, `TEXT`
- **DateTime**: `DATE`, `TIME`, `TIMESTAMP`
- **Others**: `BOOLEAN`, `ENUM`, `ARRAY`

### Constraints
- **Syntax**: `column type [NOT NULL | UNIQUE | DEFAULT value | PRIMARY KEY | REFERENCES table(col) | CHECK (condition)]`

<details><summary>Example</summary>

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT CHECK (age >= 18)
);
```
</details>

### CREATE TABLE
- **Syntax**: `CREATE TABLE table_name (column type [constraints]);`

<details><summary>Example</summary>

```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```
</details>

### INSERT
- **Syntax**: `INSERT INTO table_name (columns) VALUES (values);`

<details><summary>Example</summary>

```sql
INSERT INTO products (name) VALUES ('Laptop');
```
</details>

### INSERT with Columns
- **Syntax**: `INSERT INTO table_name (column1, column2) VALUES (value1, value2);`

<details><summary>Example</summary>

```sql
INSERT INTO employees (name, salary) VALUES ('Alice', 60000);
```
</details>

### ALTER TABLE
- **Syntax**: `ALTER TABLE table_name [ADD column type | DROP column | ALTER COLUMN column TYPE type | RENAME COLUMN old TO new | ALTER COLUMN column SET DEFAULT value | ALTER COLUMN column SET NOT NULL];`

<details><summary>Example</summary>

```sql
ALTER TABLE employees 
ADD email VARCHAR(100);
```
</details>

### DROP and TRUNCATE
- **Syntax**: `DROP TABLE table_name; TRUNCATE TABLE table_name;`

<details><summary>Example</summary>

```sql
TRUNCATE TABLE logs;
```
</details>

### UPDATE
- **Syntax**: `UPDATE table_name SET column = value WHERE condition;`

<details><summary>Example</summary>

```sql
UPDATE employees 
SET salary = salary + 5000 
WHERE department = 'IT';
```
</details>

### DELETE
- **Syntax**: `DELETE FROM table_name WHERE condition;`

<details><summary>Example</summary>

```sql
DELETE FROM orders 
WHERE status = 'cancelled';
```
</details>

---

## Views and Materialized Views 🖼️

### CREATE TABLE AS
- **Syntax**: `CREATE TABLE table_name AS SELECT ...;`

<details><summary>Example</summary>

```sql
CREATE TABLE high_paid 
AS 
SELECT name, salary FROM employees WHERE salary > 70000;
```
</details>

### CREATE VIEW
- **Syntax**: `CREATE VIEW view_name AS SELECT ...;`

<details><summary>Example</summary>

```sql
CREATE VIEW active_users 
AS 
SELECT name FROM users WHERE active = TRUE;
```
</details>

### CREATE MATERIALIZED VIEW
- **Syntax**: `CREATE MATERIALIZED VIEW view_name AS SELECT ...;`

<details><summary>Example</summary>

```sql
CREATE MATERIALIZED VIEW sales_summary 
AS 
SELECT product_id, SUM(amount) FROM sales GROUP BY product_id;
```
</details>

### REFRESH MATERIALIZED VIEW
- **Syntax**: `REFRESH MATERIALIZED VIEW view_name;`

<details><summary>Example</summary>

```sql
REFRESH MATERIALIZED VIEW sales_summary;
```
</details>

### View Management
- **Syntax**: `ALTER VIEW view_name RENAME TO new_name; ALTER VIEW view_name RENAME COLUMN old TO new;`

<details><summary>Example</summary>

```sql
ALTER VIEW active_users 
RENAME TO current_users;
```
</details>

---

## Window Functions 📈

### OVER
- **Syntax**: `FUNCTION() OVER ()`

<details><summary>Example</summary>

```sql
SELECT name, 
salary, 
AVG(salary) OVER () AS avg_salary 
FROM employees;
```
</details>

### OVER with PARTITION BY
- **Syntax**: `FUNCTION() OVER (PARTITION BY column)`

<details><summary>Example</summary>

```sql
SELECT name, 
salary, 
AVG(salary) OVER (PARTITION BY department) AS dept_avg 
FROM employees;
```
</details>

### OVER with ORDER BY (Running Total)
- **Syntax**: `FUNCTION() OVER (ORDER BY column)`

<details><summary>Example</summary>

```sql
SELECT name, 
salary, 
SUM(salary) OVER (ORDER BY salary) AS running_total 
FROM employees;
```
</details>

### OVER with PARTITION BY and ORDER BY
- **Syntax**: `FUNCTION() OVER (PARTITION BY column ORDER BY column)`

<details><summary>Example</summary>

```sql
SELECT name, 
salary, 
SUM(salary) OVER (PARTITION BY department ORDER BY salary) AS dept_running_total 
FROM employees;
```
</details>

### RANK, ROW_NUMBER, FIRST_VALUE, LAST_VALUE, LEAD, LAG
| Function      | Use                           | Example Use                              |
|---------------|-------------------------------|------------------------------------------|
| `RANK`        | Rank within window           | `RANK() OVER (ORDER BY salary)`          |
| `ROW_NUMBER`  | Unique row number            | `ROW_NUMBER() OVER (ORDER BY salary)`    |
| `FIRST_VALUE` | First value in window        | `FIRST_VALUE(name) OVER (PARTITION BY dept)` |
| `LAST_VALUE`  | Last value in window         | `LAST_VALUE(name) OVER (PARTITION BY dept)`  |
| `LEAD`        | Next row’s value             | `LEAD(salary) OVER (ORDER BY salary)`    |
| `LAG`         | Previous row’s value         | `LAG(salary) OVER (ORDER BY salary)`     |

<details><summary>Example</summary>

```sql
SELECT name, 
salary, 
ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary) 
FROM employees;
```
</details>

---

## Advanced Grouping 🗂️

### GROUPING SETS
- **Syntax**: `GROUP BY GROUPING SETS ((column1, column2), (column1), ())`

<details><summary>Example</summary>

```sql
SELECT department, 
job_title, 
SUM(salary) 
FROM employees 
GROUP BY 
    GROUPING SETS ((department, job_title), (department), ());
```
</details>

### ROLLUP
- **Syntax**: `GROUP BY ROLLUP (column1, column2)`

<details><summary>Example</summary>

```sql
SELECT department, 
job_title, 
SUM(salary) 
FROM employees 
GROUP BY 
ROLLUP (department, job_title);
```
</details>

### CUBE
- **Syntax**: `GROUP BY CUBE (column1, column2)`

<details><summary>Example</summary>

```sql
SELECT department, 
job_title, 
SUM(salary) 
FROM employees 
GROUP BY 
CUBE (department, job_title);
```
</details>

---

## Special Joins 🤲

### SELF JOIN
- **Venn Diagram Description**: Joins a table to itself (like overlapping a circle with itself).
- **Syntax**: `SELECT columns FROM table_name t1 JOIN table_name t2 ON condition;`

<details><summary>Example</summary>

```sql
SELECT e1.name, e2.name AS manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.id;
```
</details>

### CROSS JOIN
- **Venn Diagram Description**: Combines all rows from both tables (Cartesian product, like combining every point of two circles).
- **Syntax**: `SELECT columns FROM table1 CROSS JOIN table2;`

<details><summary>Example</summary>

```sql
SELECT e.name, d.department_name
FROM employees e
CROSS JOIN departments d;
```
</details>

### NATURAL JOIN
- **Venn Diagram Description**: Joins tables on columns with the same name (like an automatic INNER JOIN).
- **Syntax**: `SELECT columns FROM table1 NATURAL JOIN table2;`

<details><summary>Example</summary>

```sql
SELECT name, department_name
FROM employees 
NATURAL JOIN departments;
```
</details>

---

## Functions and Transactions ⚙️

### FUNCTION
- **Syntax**: `CREATE FUNCTION name(params) LANGUAGE plpqsql RETURNS type AS $$ body $$;`

<details><summary>Example</summary>

```sql
CREATE FUNCTION add_numbers(a INT, b INT) 
    RETURNS INT 
    LANGUAGE plpqsql
AS 
$$
DECLARE
result INT;
BEGIN
    SELECT a + b
    INTO result
    RETURN result;
END;
$$;
```
</details>

### TRANSACTION (SAVEPOINT, ROLLBACK)
- **Syntax**: `BEGIN; SAVEPOINT name; ROLLBACK TO name; COMMIT;`

<details><summary>Example</summary>

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
SAVEPOINT sp1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
ROLLBACK TO sp1;
COMMIT;
```
</details>

### STORED PROCEDURE
- **Syntax**: `CREATE PROCEDURE name(params) LANGUAGE plpqsql AS $$ body $$;`

<details><summary>Example</summary>

```sql
CREATE PROCEDURE update_salary(emp_id INT, amount NUMERIC)
LANGUAGE plpgsql
AS 
$$
BEGIN
    UPDATE employees SET salary =salary + amount WHERE id = emp_id;
COMMIT;
END;
$$;
```
</details>

---

## User Management 🔐

### CREATE USER
- **Syntax**: `CREATE USER name WITH PASSWORD 'password';`

<details><summary>Example</summary>

```sql
CREATE USER john 
WITH PASSWORD 'secure123';
```
</details>

### CREATE ROLE
- **Syntax**: `CREATE ROLE role_name;`

<details><summary>Example</summary>

```sql
CREATE ROLE analyst;
```
</details>

### GRANT
- **Syntax**: `GRANT privilege ON table_name TO user_or_role;`

<details><summary>Example</summary>

```sql
GRANT SELECT ON employees TO analyst;
```
</details>

### REVOKE
- **Syntax**: `REVOKE privilege ON table_name FROM user_or_role;`

<details><summary>Example</summary>

```sql
REVOKE SELECT ON employees FROM analyst;
```
</details>

---

## Indexes ⚡

### BTREE INDEX
- **Syntax**: `CREATE INDEX index_name ON table_name (column);`

<details><summary>Example</summary>

```sql
CREATE INDEX idx_name ON employees (name);
```
</details>

### BITMAP INDEX
- **Syntax**: `CREATE INDEX index_name ON table_name USING BITMAP (column);`

<details><summary>Example</summary>

```sql
CREATE INDEX idx_dept_bitmap ON employees USING BITMAP (department);
```
</details>

---

## Common Table Expressions (CTEs) 🌳

### CTE
- **Syntax**: `WITH cte_name AS (SELECT ...) SELECT ... FROM cte_name;`

<details><summary>Example</summary>

```sql
WITH dept_avg AS (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT name, salary
FROM employees e
JOIN dept_avg da ON e.department = da.department
WHERE e.salary > da.avg_salary;
```
</details>

### MULTIPLE CTEs
- **Syntax**: `WITH cte1 AS (...), cte2 AS (...) SELECT ...;`

<details><summary>Example</summary>

```sql
WITH dept_count AS (
    SELECT department, COUNT(*) AS emp_count
    FROM employees
    GROUP BY department
), dept_avg AS (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT dc.department, dc.emp_count, da.avg_salary
FROM dept_count dc
JOIN dept_avg da ON dc.department = da.department;
```
</details>

### RECURSIVE CTE
- **Syntax**: `WITH RECURSIVE cte_name AS (base_query UNION [ALL] recursive_query) SELECT ...;`

<details><summary>Example</summary>

```sql
WITH RECURSIVE hierarchy AS (
    SELECT id, name, manager_id
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.id, e.name, e.manager_id
    FROM employees e
    JOIN hierarchy h ON e.manager_id = h.id
)
SELECT * FROM hierarchy;
```
</details>

---

Happy revising! 🎉
