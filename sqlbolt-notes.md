# SQLBolt Notes

Source: https://sqlbolt.com  
Status: Completed ✅  

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

