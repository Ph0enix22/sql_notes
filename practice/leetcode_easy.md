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

## 181. Employees Earning More Than Their Managers  
**Concept:** Self JOIN  

### Requirement
- Compare each employee’s salary  
- With their manager’s salary  
- Return employees earning more than their manager  

### Solution

```sql
SELECT e1.name AS Employee
FROM employee e1
JOIN employee e2
    ON e1.managerid = e2.id
WHERE e1.salary > e2.salary;
```

---

## 620. Not Boring Movies  
**Concept:** WHERE filtering, MOD operator, ORDER BY  

### Requirement
- Select movies with odd `id`  
- Exclude movies with description = "boring"  
- Sort by rating in descending order  

### Solution

```sql
SELECT *
FROM cinema
WHERE id % 2 != 0
  AND description != 'boring'
ORDER BY rating DESC;
```

---
