## CASE Statement

Used for conditional logic in SQL (similar to if/else).

### Syntax:
```sql
SELECT
CASE
    WHEN condition THEN value
    WHEN condition THEN value
    ELSE value
END
FROM table;
```

### Example:
```sql
SELECT
CASE
    WHEN A + B <= C OR A + C <= B OR B + C <= A THEN 'Not A Triangle'
    WHEN A = B AND B = C THEN 'Equilateral'
    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
    ELSE 'Scalene'
END
FROM TRIANGLES;
```

Note:
- CASE executes top → bottom.
- Order of conditions matters.
