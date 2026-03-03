## Numeric Functions

### ROUND()
- Used to round numeric values
- Syntax: ROUND(number, decimal_places)
- If decimal_places not given → rounds to nearest integer

Example:
```sql
SELECT ROUND(AVG(population))
FROM city;
```

### FLOOR()
- Rounds a number "down" to the nearest integer.
- Syntax: FLOOR(number)

Example:
```sql
SELECT FLOOR(AVG(population))
FROM city;
```
