# Exercises: Parameterized SQL, Roles, and Least Privilege

## Exercise 1: Repair unsafe queries

For email lookup, price range, and product-name search, write fixed SQL with placeholders. List the separately bound values.

## Exercise 2: Allowlist sorting

Design a mapping for sort choices `name`, `price_low`, and `price_high`. Show why a placeholder cannot safely replace `ORDER BY` structure.

## Exercise 3: Design roles

Create a privilege table for migration owner, shop runtime, and read-only analyst. List required and forbidden operations. If PostgreSQL is available, create disposable roles and prove one forbidden operation fails.
