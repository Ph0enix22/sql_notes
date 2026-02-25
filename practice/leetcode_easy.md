# LeetCode Easy – SQL

---

## 175. Combine Two Tables
**Concept:** LEFT JOIN  

### The problem requires:
- All persons
- Address if available
- NULL if not available

### Solution

```sql
SELECT p.firstname, p.lastname, a.city, a.state
FROM person AS p
LEFT JOIN address AS a
    ON p.personid = a.personid;
```

---
