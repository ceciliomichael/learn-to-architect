# Exercise Solutions: Parameterized SQL, Roles, and Least Privilege

## Exercise 1

SQLite-style fixed statements are:

```sql
SELECT user_id FROM users WHERE email = ?;
SELECT product_id, name FROM products WHERE price_cents BETWEEN ? AND ?;
SELECT product_id, name FROM products WHERE name LIKE ?;
```

Bind the email, minimum and maximum cents, and an intentionally constructed pattern as data through the API.

## Exercise 2

Use a fixed mapping:

```text
name       -> ORDER BY name ASC, product_id ASC
price_low  -> ORDER BY price_cents ASC, product_id ASC
price_high -> ORDER BY price_cents DESC, product_id ASC
```

Only these complete trusted fragments can be selected. A parameter represents a value, not grammar such as a direction or identifier.

## Exercise 3

The migration owner can create and alter schema but is not used by the running app. The runtime can read products and create or update orders within policy but cannot drop tables or grant privileges. The analyst can select approved views but cannot change rows. Test with `SET ROLE` in a disposable PostgreSQL database and attempt both one allowed select and one forbidden drop.
