# Module 02: Select Columns, Expressions, and Column Aliases

## What You Will Learn

In this module, you will learn how to read specific columns, use backticks (`` `col` ``) to quote identifiers, use MySQL's string concatenation function (`CONCAT()`), apply column aliases with `AS`, and perform dynamic mathematical calculations inside `SELECT` queries.

---

## Quoting Identifiers (Backticks vs Single Quotes)

In MySQL:
- **Backticks (`` `column_name` ``)**: Quote table and column names (identifiers). Required if an identifier matches a reserved keyword or contains special characters.
- **Single Quotes (`'text_value'`)**: Quote text string literals.

```sql
SELECT `product_name`, `price` FROM `inventory`;
```

---

## String Concatenation: `CONCAT()`

Unlike SQLite (which uses `||`), MySQL uses the `CONCAT()` function for string joining:

```sql
SELECT CONCAT(`first_name`, ' ', `last_name`) AS `full_name` FROM `employees`;
```

If any argument in `CONCAT()` is `NULL`, MySQL returns `NULL` unless handled with `CONCAT_WS()` (Concatenate With Separator) or `IFNULL()`.

---

## Practical Example

```sql
USE store_db;

CREATE TABLE `items` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `title` VARCHAR(100) NOT NULL,
  `unit_price` DECIMAL(10,2) NOT NULL,
  `qty` INT NOT NULL
);

INSERT INTO `items` (`title`, `unit_price`, `qty`) VALUES
  ('Ergonomic Keyboard', 129.99, 4),
  ('4K Monitor', 349.50, 2);

SELECT 
  CONCAT('Product: ', `title`) AS `item_label`,
  `unit_price`,
  `qty`,
  `unit_price` * `qty` AS `total_stock_value`
FROM `items`;
```

### Output

```text
+----------------------------+------------+-----+-------------------+
| item_label                 | unit_price | qty | total_stock_value |
+----------------------------+------------+-----+-------------------+
| Product: Ergonomic Keyboard|     129.99 |   4 |            519.96 |
| Product: 4K Monitor        |     349.50 |   2 |            699.00 |
+----------------------------+------------+-----+-------------------+
```

---

## Line-by-Line Breakdown

- `` CONCAT('Product: ', `title`) AS `item_label` ``: Concatenates text literal with `title` column, aliasing result header to `item_label`.
- `` `unit_price` * `qty` AS `total_stock_value` ``: Dynamically multiplies price by quantity for display.

---

## Check Your Understanding

1. Why does `SELECT 'a' + 'b';` in MySQL return `0` instead of `'ab'`?
2. What character is used in MySQL to enclose table and column names?
