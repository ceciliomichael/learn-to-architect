# Module 10: Compose Queries with Subqueries and CTEs

## What You Will Learn

In this module, you will learn how to break complex queries into modular steps using scalar subqueries, list subqueries, correlated subqueries with `EXISTS`, and Common Table Expressions (CTEs) using the `WITH` clause.

---

## Subqueries

A subquery is a nested query enclosed in parentheses `(...)`.

### 1. Scalar Subquery (Returns a single value)
```sql
SELECT title, price 
FROM books 
WHERE price > (SELECT AVG(price) FROM books);
```

### 2. List Subquery (Returns a single column of multiple rows)
```sql
SELECT name FROM authors 
WHERE id IN (SELECT author_id FROM books WHERE price > 50.0);
```

### 3. Correlated Subquery with `EXISTS`
```sql
SELECT c.name 
FROM customers c 
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.customer_id = c.id AND o.amount > 100.0
);
```

---

## Common Table Expressions (CTEs)

A CTE defines a named temporary result set using the `WITH` keyword, making complex SQL far easier to read and maintain:

```sql
WITH high_value_orders AS (
  SELECT customer_id, SUM(amount) AS total_spent
  FROM orders
  GROUP BY customer_id
  HAVING SUM(amount) > 100.0
)
SELECT c.name, hvo.total_spent
FROM high_value_orders hvo
JOIN customers c ON hvo.customer_id = c.id;
```

---

## Check Your Understanding

1. What advantage does a CTE (`WITH` clause) offer over a complex nested subquery?
2. How does `EXISTS` evaluate row existence efficiently?
