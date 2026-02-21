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

