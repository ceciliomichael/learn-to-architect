# Module 14: Window Functions and Native JSON Data Handling

## What You Will Learn

In this module, you will learn how to use MySQL 8.0+ window functions (`ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LAG()`, `LEAD()`), store JSON data natively in `JSON` columns, and extract values using JSON operators (`->` and `->>`).

---

## Window Functions in MySQL 8.0+

```sql
SELECT 
  `name`,
  `dept_id`,
  `salary`,
  DENSE_RANK() OVER(PARTITION BY `dept_id` ORDER BY `salary` DESC) AS `dept_salary_rank`
FROM `employees`;
```

---

## Native `JSON` Data Type & Operators

MySQL 8.0 natively validates and stores binary JSON documents.

- `->` operator (shorthand for `JSON_EXTRACT()`): Returns JSON value with quotes.
- `->>` operator (shorthand for `JSON_UNQUOTE(JSON_EXTRACT())`): Returns raw unquoted text string/number.

```sql
CREATE TABLE `user_settings` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `data` JSON NOT NULL
) ENGINE=InnoDB;

INSERT INTO `user_settings` (`data`) VALUES
  ('{"theme": "dark", "notifications": true}'),
  ('{"theme": "light", "notifications": false}');

-- Using ->> to extract unquoted scalar value:
SELECT `id`, `data`->>'$.theme' AS `theme`
FROM `user_settings`
WHERE `data`->>'$.notifications' = 'true';
```

---

## Check Your Understanding

1. What is the difference between `data->'$.key'` and `data->>'$.key'` in MySQL?
2. What happens if you try to insert invalid JSON text into a MySQL column declared as `JSON`?
