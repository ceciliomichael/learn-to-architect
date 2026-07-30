# Module 10: Compose Queries with Subqueries and CTEs

## What You Will Learn

In this module, you will learn how to write scalar subqueries, list subqueries, correlated subqueries using `EXISTS`, and Common Table Expressions (`WITH cte AS (...)`) in MySQL 8.0+.

---

## Subqueries in MySQL

### 1. Scalar Subquery
```sql
SELECT `title`, `unit_price`
FROM `items`
WHERE `unit_price` > (SELECT AVG(`unit_price`) FROM `items`);
```

### 2. Correlated Subquery with `EXISTS`
```sql
SELECT c.`name`
FROM `customers` c
WHERE EXISTS (
  SELECT 1 FROM `orders` o WHERE o.`customer_id` = c.`id` AND o.`amount` > 500.00
);
```

---

## Common Table Expressions (CTEs in MySQL 8.0+)

Starting in MySQL 8.0, CTEs (`WITH` clauses) provide modular query structure:

```sql
WITH `regional_totals` AS (
  SELECT `region`, SUM(`amount`) AS `total`
  FROM `sales`
  GROUP BY `region`
)
SELECT `region`, `total`
FROM `regional_totals`
WHERE `total` > 1000.00;
```

---

## Check Your Understanding

1. In what version of MySQL were Common Table Expressions (`WITH` syntax) introduced?
2. How does `EXISTS` evaluate correlated subqueries?
