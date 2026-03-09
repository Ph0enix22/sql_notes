# SQLBolt Notes

Source: https://sqlbolt.com  

---

# Lesson 1 — SELECT queries

## Syntax

```sql
SELECT column1, column2, ...
FROM table_name;
```

## Select all columns

```sql
SELECT *
FROM table_name;
```

## Notes

- SELECT retrieves data
- FROM specifies table
- `*` means all columns

---

# Lesson 2 — WHERE clause

## Syntax

```sql
SELECT column1, ...
FROM table_name
WHERE condition
  AND/OR another_condition
  AND/OR ...;
```

## WHERE Clause Operators

| Operator | Condition | Example |
|--------|-----------|---------|
| `=` | Equal to | `age = 18` |
| `!=` | Not equal to | `age != 18` |
| `<` | Less than | `age < 18` |
| `<=` | Less than or equal | `age <= 18` |
| `>` | Greater than | `age > 18` |
| `>=` | Greater than or equal | `age >= 18` |
| `BETWEEN ... AND ...` | Within range (inclusive) | `age BETWEEN 18 AND 25` |
| `NOT BETWEEN ... AND ...` | Outside range | `age NOT BETWEEN 18 AND 25` |
| `IN (...)` | Matches any value in list | `age IN (18, 21, 25)` |
| `NOT IN (...)` | Does not match any value in list | `age NOT IN (18, 21, 25)` |

## Notes

- WHERE filters rows

---

# Lesson 3 — WHERE with Text Data

## Syntax

```sql
SELECT column1, ...
FROM table_name
WHERE condition;
```

## Text Comparison Operators

| Operator | Meaning | Example |
|---------|---------|---------|
| `=` | Exact match | `title = "Toy Story"` |
| `!=` or `<>` | Not equal | `title != "Cars"` |
| `LIKE` | Pattern match | `title LIKE "Toy%"` |
| `NOT LIKE` | Does not match pattern | `title NOT LIKE "Toy%"` |
| `IN (...)` | Matches any value in list | `director IN ("John Lasseter", "Brad Bird")` |
| `NOT IN (...)` | Does not match any value in list | `director NOT IN ("John Lasseter")` |

## Wildcards

### `%` → Matches zero or more characters

```sql
title LIKE "%Toy%"
```

Matches:
- Toy Story  
- Toy Story 2  

### `_` → Matches exactly one character

```sql
title LIKE "WALL-_"
```

Matches:
- WALL-E  
- WALL-G  

Does NOT match:
- WALL-EE

## Key Points

- Use `LIKE` for pattern matching  
- `%` matches multiple characters  
- `_` matches one character  
- Use `IN` for matching multiple values  
- Always use quotes for text values

---

# Lesson 4 — DISTINCT, ORDER BY, LIMIT, OFFSET

## DISTINCT — Remove duplicate values

Returns only unique values from a column.

### Syntax

```sql
SELECT DISTINCT column1, column2, ...
FROM table_name
WHERE condition(s);
```

## ORDER BY — Sort results

Sorts query results in ascending or descending order.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column_name ASC;
```

```sql
SELECT column_name
FROM table_name
ORDER BY column_name DESC;
```

- `ASC` → ascending (default)
- `DESC` → descending

## LIMIT — Restrict number of rows

Returns only a specified number of rows.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
LIMIT num;
```

## OFFSET — Skip rows

Skips a specified number of rows before returning results.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
LIMIT num_limit OFFSET num_offset;
```

## Combined Example

```sql
SELECT title, year
FROM movies
ORDER BY year DESC
LIMIT 5 OFFSET 5;
```

Skips first 5 newest movies and returns the next 5 newest movies.

## Key Points

- `DISTINCT` removes duplicate values  
- `ORDER BY` sorts results  
- `ASC` = ascending, `DESC` = descending  
- `LIMIT` restricts number of rows returned  
- `OFFSET` skips rows before returning results  

---

# Lesson 5 — Review: Simple SELECT Queries

## Full Query Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT number OFFSET number;
```

## Key Points

- Combine multiple clauses in one query  
- `WHERE` filters rows  
- `ORDER BY` sorts rows  
- `LIMIT` restricts results  
- `OFFSET` skips rows  
- All clauses work together to answer specific questions

---

# Lesson 6 — Multi-table Queries with INNER JOIN

In normalized databases, related data is stored in separate tables.

Example:
- `movies` → movie info
- `boxoffice` → ratings and sales

JOIN combines related data using a common key (`movie_id`).

## INNER JOIN Syntax

```sql
SELECT table1.column, table2.column
FROM table1
INNER JOIN table2
    ON table1.common_column = table2.common_column
WHERE condition(s)
ORDER BY COLUMN, ... ASC/DESC
LIMIT num OFFSET num;
```

## How INNER JOIN works

- Matches rows from both tables
- Uses a shared key (`id`, `movie_id`, etc.)
- Returns only matching rows
- Combines columns from both tables

---

## Example Tables

movies:
- id
- title
- director
- year

boxoffice:
- movie_id
- rating
- domestic_sales
- international_sales

Common key:
```sql
movies.id = boxoffice.movie_id
```

## Column Reference Format

Use this format when working with multiple tables:

```sql
table_name.column_name
```

Example:

```sql
movies.title
boxoffice.rating
```

Prevents ambiguity.

## Key Points

- `INNER JOIN` combines rows from two tables  
- Uses common key with `ON`  
- Returns only matching rows  
- Use `table.column` format  
- Can combine with `WHERE`, `ORDER BY`, `LIMIT`

---

# Lesson 7 — OUTER JOINs (LEFT, RIGHT, FULL)

## Problem with INNER JOIN

`INNER JOIN` returns only matching rows in both tables.

Unmatched rows are excluded.

## OUTER JOIN Types

| JOIN Type | Returns |
|----------|---------|
| `LEFT JOIN` | All rows from left table + matching rows from right table |
| `RIGHT JOIN` | All rows from right table + matching rows from left table |
| `FULL JOIN` | All rows from both tables |

Unmatched values appear as `NULL`(means no matching data exists).

## Syntax

```sql
SELECT table1.column, table2.column
FROM table1
LEFT/RIGHT/FULL JOIN table2
    ON table1.common_column = table2.common_column
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

## Key Points

- `LEFT JOIN` keeps all rows from left table  
- `RIGHT JOIN` keeps all rows from right table  
- `FULL JOIN` keeps all rows from both tables  
- Unmatched rows show `NULL`  
- Use LEFT JOIN when you want all records from primary table  
- INNER JOIN excludes unmatched rows

---

# Lesson 8 — NULL Values

## What is NULL?

`NULL` means missing, unknown, or no value.

It is NOT:
- 0
- empty string ""
- false

It represents absence of data.

## Why NULL exists

Occurs when:

- Data is missing
- Data is not assigned yet
- Using OUTER JOIN
- Incomplete records

Example:

```
name       building
---------  --------
Oliver P.  NULL
```

## Checking for NULL

Use `IS NULL` or `IS NOT NULL`

```sql
building IS NULL
building IS NOT NULL
```

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name IS NULL;
```

```sql
SELECT column_name
FROM table_name
WHERE column_name IS NOT NULL;
```

## Why normal comparison doesn't work

NULL is not equal to anything, including itself.

This fails:

```sql
building = NULL
```

Because NULL means unknown value.

## Key Points

- `NULL` means missing or unknown data  
- Use `IS NULL` to find missing values  
- Use `IS NOT NULL` to find existing values  
- Cannot use `=` or `!=` with NULL  
- Common when using OUTER JOIN

---

# Lesson 9 — Queries with Expressions and Aliases

An expression performs calculations or transformations on column values.

Examples:
- Arithmetic operations
- Mathematical functions
- String functions

## Expression Syntax

```sql
SELECT column1 + column2
FROM table_name;
```

## Using Aliases (AS)

Aliases rename columns in the output for readability.

### Syntax

```sql
SELECT expression AS alias_name
FROM table_name;
```

## Expression Examples

### Combined sales

```sql
SELECT domestic_sales + international_sales AS total_sales
FROM boxoffice;
```

Output column will be named `total_sales`.

### Convert sales to millions

```sql
SELECT (domestic_sales + international_sales) / 1000000 AS total_sales_millions
FROM boxoffice;
```

### Convert rating to percentage

```sql
SELECT rating * 10 AS rating_percent
FROM boxoffice;
```

### Find movies released in even years

```sql
SELECT title, year
FROM movies
WHERE year % 2 = 0;
```

`%` is modulo operator (returns remainder).

## Table Aliases

Used to shorten table names.

### Syntax

```sql
SELECT t.column_name
FROM table_name AS t;
```

## Column Alias Example with JOIN

```sql
SELECT m.title,
       (b.domestic_sales + b.international_sales) AS total_sales
FROM movies AS m
INNER JOIN boxoffice AS b
    ON m.id = b.movie_id;
```

## Key Points

- Expressions perform calculations in queries  
- Use `AS` to rename columns  
- Improves readability  
- Can combine multiple columns  
- Can use arithmetic operators  
- Table aliases simplify complex queries

---

# Lesson 10 — Aggregate Functions (Pt. 1)

Aggregate functions perform calculations on multiple rows and return a single value.

Used for:
- Counting rows
- Finding averages
- Finding minimum/maximum values
- Finding totals

## Basic Syntax

```sql
SELECT AGG_FUNCTION(column_name) AS alias_name
FROM table_name;
```

## Common Aggregate Functions

| Function | Description |
|--------|-------------|
| `COUNT(*)` | Counts total number of rows |
| `COUNT(column)` | Counts non-NULL values |
| `MIN(column)` | Finds smallest value |
| `MAX(column)` | Finds largest value |
| `AVG(column)` | Finds average value |
| `SUM(column)` | Finds total sum |

## GROUP BY — Aggregate by groups

Groups rows with same value and applies aggregate function to each group.

### Syntax

```sql
SELECT column, AGG_FUNCTION(column_or_expression)
FROM table_name
GROUP BY column;
```

## Important Notes

Without GROUP BY:
- Aggregate runs on entire table
- Returns one row

With GROUP BY:
- Aggregate runs per group
- Returns multiple rows

## Key Points

- Aggregate functions summarize data  
- `GROUP BY` groups rows for aggregation  
- Use `AS` to name results clearly

---

# Lesson 11 — HAVING Clause (Filtering Aggregated Data)

## Problem

`WHERE` filters rows before grouping.

But how do you filter after `GROUP BY`?

Solution: Use `HAVING`.

## HAVING Syntax

```sql
SELECT group_by_column, AGG_FUNC(column) AS agg_alias, ...
FROM table_name
WHERE condition
GROUP BY column
HAVING group_condition;
```

## WHERE vs HAVING

| Clause | Filters |
|------|---------|
| WHERE | Individual rows |
| HAVING | Groups |

## Key Points

- `HAVING` filters grouped data  
- Used with `GROUP BY`  
- `WHERE` filters rows before grouping  
- `HAVING` filters after grouping  
- Can use aggregate functions in HAVING

---

# Lesson 12 — Order of Execution of a Query

## Complete SELECT Query Structure

```sql
SELECT DISTINCT column, AGG_FUNCTION(column_or_expression), ...
FROM table AS t
JOIN another_table as a
    ON t.column = a.column
WHERE condition
GROUP BY column
HAVING constraint_expression
ORDER BY column ASC/DESC
LIMIT num OFFSET num;
```

## Actual Execution Order

SQL executes queries in this order:

```text
1. FROM / JOIN
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. DISTINCT
7. ORDER BY
8. LIMIT / OFFSET
```

## Explanation

### 1. FROM / JOIN
- Selects tables
- Combines tables using JOIN

### 2. WHERE
- Filters rows
- Removes unwanted rows

### 3. GROUP BY
- Groups rows with same values
- Used with aggregate functions

### 4. HAVING
- Filters grouped data

### 5. SELECT
- Chooses columns
- Computes expressions

### 6. DISTINCT
- Removes duplicate rows

### 7. ORDER BY
- Sorts results

### 8. LIMIT / OFFSET
- Limits number of rows
- Skips rows

## Important Rules

- `WHERE` filters before grouping  
- `HAVING` filters after grouping  
- Cannot use SELECT alias in WHERE  
- Can use SELECT alias in ORDER BY  
- LIMIT runs last  

## Visual Flow

```text
FROM → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT
```

## Key Points

- SQL does NOT execute in written order  
- Execution order is fixed internally  
- Understanding order prevents logical errors  
- Essential for GROUP BY and HAVING queries

---

# Lesson 13 — INSERT (Adding Data)

## What is a Schema?

A schema defines:
- Table structure
- Column names
- Data types

Example table:

```
movies
------
id (INTEGER)
title (TEXT)
director (TEXT)
year (INTEGER)
length_minutes (INTEGER)
```

## INSERT Syntax (All Columns)

Insert values for all columns:

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

Example:

```sql
INSERT INTO movies
VALUES (15, "Toy Story 4", "Josh Cooley", 2019, 100);
```

## INSERT Syntax (Specific Columns)

Insert values into selected columns:

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

Example:

```sql
INSERT INTO movies (title, director, year, length_minutes)
VALUES ("Toy Story 4", "Josh Cooley", 2019, 100);
```

Useful when:
- ID is auto-generated
- Some columns have default values

## Insert Multiple Rows

```sql
INSERT INTO table_name (column1, column2)
VALUES 
    (value1, value2),
    (value3, value4);
```

Example:

```sql
INSERT INTO movies (title, director, year, length_minutes)
VALUES 
    ("Movie A", "Director A", 2020, 120),
    ("Movie B", "Director B", 2021, 110);
```

## Insert with Expressions

Expressions can be used while inserting:

```sql
INSERT INTO boxoffice (movie_id, rating, domestic_sales)
VALUES (15, 8.7, 340000000 / 1000000);
```

## Example: Insert Toy Story 4

Insert into movies table:

```sql
INSERT INTO movies (title, director, year, length_minutes)
VALUES ("Toy Story 4", "Josh Cooley", 2019, 100);
```

Insert into boxoffice table:

```sql
INSERT INTO boxoffice (movie_id, rating, domestic_sales, international_sales)
VALUES (15, 8.7, 340000000, 270000000);
```

## Key Points

- `INSERT INTO` adds new rows  
- Must match column order and values  
- Can insert into specific columns  
- Can insert multiple rows  
- Can use expressions  
- Useful for adding new data to database

---

# Lesson 14 — UPDATE (Modifying Existing Data)

`UPDATE` is used to modify existing data in a table.

## Basic Syntax

```sql
UPDATE table
SET column = value_or_expression
WHERE condition;
```

- `SET` specifies column and new value
- `WHERE` specifies which rows to update

## Update Multiple Columns

```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE condition;
```

## Example: Update multiple columns

```sql
UPDATE movies
SET title = "Toy Story 3",
    director = "Lee Unkrich"
WHERE id = 11;
```

## Important Warning

If you omit `WHERE`, ALL rows will be updated:

```sql
UPDATE movies
SET director = "Unknown";  -- affects entire table
```

Always use WHERE carefully.

## Best Practice

Test condition first with SELECT:

```sql
SELECT *
FROM movies
WHERE id = 11;
```

Then update:

```sql
UPDATE movies
SET title = "Toy Story 3"
WHERE id = 11;
```

## Using Expressions

```sql
UPDATE movies
SET year = year + 1
WHERE id = 3;
```

## Key Points

- `UPDATE` modifies existing rows  
- Use `SET` to assign new values  
- Use `WHERE` to select specific rows  
- Without WHERE, all rows are updated  
- Can update multiple columns  
- Can use expressions

---

# Lesson 15 — DELETE (Removing Data)

`DELETE` removes rows from a table.

## Basic Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

- `WHERE` specifies which rows to delete
- Only matching rows are removed

## Delete ALL rows

```sql
DELETE FROM table_name;
```

Removes every row in the table.

## Delete using multiple conditions

```sql
DELETE FROM movies
WHERE year < 2005 AND director = "John Lasseter";
```

## Key Points

- `DELETE` removes rows from a table  
- Use `WHERE` to select specific rows  
- Without WHERE, all rows are deleted  
- Always verify with SELECT first  
- Deleted data cannot be recovered easily

---

# Lesson 16 — CREATE TABLE (Creating New Tables)

`CREATE TABLE` is used to create a new table in a database.

Defines:
- Column names
- Data types
- Constraints
- Default values

## Basic Syntax

```sql
CREATE TABLE table_name (
    column_name DATA_TYPE,
    column_name DATA_TYPE
);
```

## CREATE TABLE with IF NOT EXISTS

Prevents error if table already exists:

```sql
CREATE TABLE IF NOT EXISTS table_name (
    column_name DATA_TYPE
);
```

## Example: Create Database Table

```sql
CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER
);
```

## Common Data Types

| Data Type | Description |
|---------|-------------|
| `INTEGER` | Whole numbers |
| `FLOAT`, `REAL`, `DOUBLE` | Decimal numbers |
| `TEXT` | String or text |
| `CHAR(n)` | Fixed-length string |
| `VARCHAR(n)` | Variable-length string |
| `BOOLEAN` | True or false |
| `DATE` | Date |
| `DATETIME` | Date and time |
| `BLOB` | Binary data |

## Common Constraints

| Constraint | Description |
|----------|-------------|
| `PRIMARY KEY` | Unique identifier for each row |
| `AUTOINCREMENT` | Automatically increments value |
| `UNIQUE` | No duplicate values |
| `NOT NULL` | Cannot store NULL |
| `CHECK` | Ensures condition is true |
| `FOREIGN KEY` | Links to another table |

## Example with Constraints

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE NOT NULL,
    age INTEGER CHECK(age >= 0)
);
```

## Key Points

- `CREATE TABLE` creates new tables  
- Defines structure and schema  
- Must specify column names and data types  
- Constraints control allowed values  
- `IF NOT EXISTS` prevents errors  
- Required before inserting data

---

# Lesson 17 — ALTER TABLE (Modifying Table Structure)

`ALTER TABLE` is used to modify an existing table.

Used to:
- Add columns
- Remove columns
- Rename table
- Modify schema

## Add Column Syntax

```sql
ALTER TABLE table_name
ADD column_name DATA_TYPE;
```

## Add Column with Default Value

```sql
ALTER TABLE table_name
ADD column_name DATA_TYPE OptionalTableConstraint
  DEFAULT default_value;
```

## Remove Column Syntax

```sql
ALTER TABLE table_name
DROP column_name;
```

## Rename Table Syntax

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

## Example: Add Multiple Columns

```sql
ALTER TABLE movies
ADD Aspect_ratio FLOAT;

ALTER TABLE movies
ADD Language TEXT DEFAULT "English";
```

## What happens after adding column

- New column added to table
- Existing rows get default value or NULL
- New rows use default value if not specified

## Key Points

- `ALTER TABLE` modifies existing tables  
- `ADD` adds new column  
- Can specify default value  
- `RENAME TO` renames table  
- Some databases (SQLite) don't support DROP COLUMN  
- Used to update schema without deleting table

---

# Lesson 18 — DROP TABLE (Deleting Tables)

`DROP TABLE` permanently removes a table and its data.

Removes:
- All rows
- All columns
- Table structure (schema)

## Basic Syntax

```sql
DROP TABLE table_name;
```

## Safe Syntax (Recommended)

Avoids error if table does not exist:

```sql
DROP TABLE IF EXISTS table_name;
```

## Drop Multiple Tables

```sql
DROP TABLE IF EXISTS movies;
DROP TABLE IF EXISTS boxoffice;
```

## DROP vs DELETE

| Command | Removes Data | Removes Table Structure |
|--------|--------------|------------------------|
| DELETE | Yes | No |
| DROP TABLE | Yes | Yes |

## Important Warning

- Cannot recover dropped table easily
- All data is permanently lost
- Use carefully

## Foreign Key Note

If table is referenced by another table:

- Must remove dependency first
- Or drop dependent tables

## Key Points

- `DROP TABLE` deletes entire table  
- Removes both data and schema  
- Use `IF EXISTS` to prevent errors  
- Cannot be undone easily  
- Different from DELETE

---

# SQL Topic — Subqueries

A subquery is a query inside another query.

Used to:
- Filter data
- Compare values
- Generate dynamic values

Subquery runs first, outer query runs second.

## Basic Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name OPERATOR (
    SELECT column_name
    FROM table_name
);
```

## Subquery with IN

Used to match values from another table.

```sql
SELECT *
FROM employees
WHERE department IN (
    SELECT department
    FROM departments
);
```

## Subquery in FROM (Derived Table)

```sql
SELECT *
FROM (
    SELECT title, year
    FROM movies
) AS movie_list;
```

Subquery acts like a temporary table.

## Correlated Subquery

Inner query depends on outer query.

Runs once per outer row.

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(revenue_generated)
    FROM employees AS dept
    WHERE dept.department = employees.department
);
```

Calculates average per department.

## EXISTS / NOT IN Example

```sql
SELECT *
FROM movies
WHERE id IN (
    SELECT movie_id
    FROM boxoffice
);
```

Returns movies that exist in boxoffice.

## Key Points

- Subquery = query inside query  
- Written inside parentheses `()`  
- Executes before outer query  
- Can be used in SELECT, FROM, WHERE  
- Correlated subquery runs per row  
- Useful for dynamic filtering

# SQL Topic — UNION, INTERSECT, EXCEPT

Set operators combine results of multiple SELECT queries.

Requirements:
- Same number of columns
- Same column order
- Same data types

## UNION

Combines results and removes duplicates.

```sql
SELECT column_name
FROM table1
UNION
SELECT column_name
FROM table2;
```

## UNION ALL

Combines results and keeps duplicates.

```sql
SELECT column_name
FROM table1
UNION ALL
SELECT column_name
FROM table2;
```

## INTERSECT

Returns only common rows in both queries.

```sql
SELECT column_name
FROM table1
INTERSECT
SELECT column_name
FROM table2;
```

## EXCEPT

Returns rows from first query NOT in second query.

```sql
SELECT column_name
FROM table1
EXCEPT
SELECT column_name
FROM table2;
```

Order matters.

## Execution Order

```text
SELECT → UNION / INTERSECT / EXCEPT → ORDER BY → LIMIT
```

## Key Differences

| Operator | Result |
|--------|--------|
| UNION | Combines, removes duplicates |
| UNION ALL | Combines, keeps duplicates |
| INTERSECT | Common rows only |
| EXCEPT | Rows only in first query |

## Key Points

- Combines results from multiple queries  
- Queries must have same structure  
- UNION removes duplicates  
- UNION ALL keeps duplicates  
- INTERSECT finds common rows  
- EXCEPT finds unique rows in first query

---

# Advanced Understanding — Subquery Mental Models

## IN Subquery — Mental Model

### Core Idea

IN subquery works in 2 steps:

```
Step 1: Inner query creates a list
Step 2: Outer query checks each row against that list
```

### Example Tables

customers:

| id | name |
|---|---|
| 1 | Alice |
| 2 | Bob |
| 3 | Charlie |
| 4 | David |

orders:

| order_id | customer_id |
|---|---|
| 101 | 1 |
| 102 | 3 |

---

### Query

```sql
SELECT *
FROM customers
WHERE id IN (
    SELECT customer_id
    FROM orders
);
```

### Step 1 — Inner query runs first

```sql
SELECT customer_id FROM orders;
```

Result:

```
[1, 3]
```

Database creates list:

```
LIST = [1, 3]
```

### Step 2 — Outer query checks each row

```
Alice   id=1 → in list → YES
Bob     id=2 → in list → NO
Charlie id=3 → in list → YES
David   id=4 → in list → NO
```

### Final Result

```
Alice
Charlie
```

### Mental Model

```
Build list → Check each row
```

### Key Rule

IN subquery runs inner query ONCE.

---

## Correlated Subquery — Mental Model

### Core Idea

Correlated subquery runs inner query for EACH row.

```
FOR EACH ROW → run inner query using that row
```

### Example Table

numbers:

| num |
|---|
| 1 |
| 2 |
| 3 |
| 4 |

### Query

```sql
SELECT num
FROM numbers n1
WHERE num > (
    SELECT AVG(num)
    FROM numbers n2
    WHERE n2.num <= n1.num
);
```

### Execution Visualization

num = 1  
inner query → avg(1) = 1  
check → 1 > 1 → NO  

num = 2  
inner query → avg(1,2) = 1.5  
check → 2 > 1.5 → YES  

num = 3  
inner query → avg(1,2,3) = 2  
check → YES  

num = 4  
inner query → avg(1,2,3,4) = 2.5  
check → YES  

### Final Result

```
2
3
4
```

### Mental Model

Inner query changes per row:

```
num=1 → run query using 1
num=2 → run query using 2
num=3 → run query using 3
num=4 → run query using 4
```

### Key Rule

Correlated subquery runs MANY times (once per row).

## Final Intuition Summary

Existence(IN) subquery:

```
Make list → check list
```

Correlated subquery:

```
For each row → run query again
```

JOIN:

```
Combine tables directly
```

----------------------------------

# SQLBolt Course: Fully Completed

Date completed: 21-02-2026

---

# Notes Purpose

This document serves as:

- Personal SQL reference
- Revision guide
- Long-term knowledge base

----------------------------------

End of SQLBolt Notes 💖
