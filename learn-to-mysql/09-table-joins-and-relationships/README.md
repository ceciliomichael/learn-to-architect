# Module 09: Join Tables and Model Relational Schema

## What You Will Learn

In this module, you will learn how to connect multiple MySQL tables using `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `CROSS JOIN`, alias table identifiers, and handle multi-table relational relationships in production schemas.

---

## MySQL Join Types

- **`INNER JOIN`**: Returns matching records from both tables.
- **`LEFT JOIN`** (or `LEFT OUTER JOIN`): Returns all records from left table; unmatched right fields return `NULL`.
- **`RIGHT JOIN`** (or `RIGHT OUTER JOIN`): Returns all records from right table; unmatched left fields return `NULL`.
- **`CROSS JOIN`**: Cartesian product combining every row from left table with every row from right table.

```sql
SELECT 
  c.`name` AS `customer_name`,
  o.`id` AS `order_id`,
  o.`amount`
FROM `customers` c
INNER JOIN `orders` o ON c.`id` = o.`customer_id`;
```

---

## Multi-Table Joins & Junction Tables

For many-to-many relationships, join through a junction table:

```sql
SELECT 
  s.`name` AS `student`,
  c.`title` AS `course`
FROM `students` s
JOIN `enrollments` e ON s.`id` = e.`student_id`
JOIN `courses` c ON e.`course_id` = c.`id`;
```

---

## Check Your Understanding

1. How does `RIGHT JOIN` differ from `LEFT JOIN`?
2. What is a junction table used for in database design?
