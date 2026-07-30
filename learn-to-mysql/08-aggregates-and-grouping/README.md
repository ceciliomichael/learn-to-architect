# Module 08: Group and Aggregate Data

## What You Will Learn

In this module, you will learn how to summarize data using MySQL aggregate functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`), group summary rows using `GROUP BY`, filter groups using `HAVING`, and understand MySQL's strict `ONLY_FULL_GROUP_BY` SQL mode.

---

## Aggregate Functions

```sql
SELECT 
  COUNT(*) AS `total_orders`,
  SUM(`amount`) AS `revenue`,
  AVG(`amount`) AS `avg_order_value`
FROM `orders`;
```

---

## `GROUP BY` and Strict `ONLY_FULL_GROUP_BY`

In modern MySQL (version 5.7+ and 8.0+), the `ONLY_FULL_GROUP_BY` SQL mode is enabled by default.

This mode requires that **every non-aggregated column in the `SELECT` list MUST be explicitly included in the `GROUP BY` clause**.

```sql
-- VALID (Every non-aggregated column is in GROUP BY)
SELECT `category`, `status`, COUNT(*) AS `cnt`
FROM `products`
GROUP BY `category`, `status`;

-- INVALID under ONLY_FULL_GROUP_BY (status is missing from GROUP BY)
-- Throws ERROR 1055 (42000)
SELECT `category`, `status`, COUNT(*) AS `cnt`
FROM `products`
GROUP BY `category`;
```

---

## Filtering Groups with `HAVING`

```sql
SELECT `category`, COUNT(*) AS `item_count`
FROM `products`
GROUP BY `category`
HAVING COUNT(*) > 10;
```

---

## Check Your Understanding

1. What error occurs if you select a non-aggregated column that is absent from `GROUP BY` under default MySQL settings?
2. How does `HAVING` differ from `WHERE`?
