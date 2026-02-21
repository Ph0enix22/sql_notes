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
