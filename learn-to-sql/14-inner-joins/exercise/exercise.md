# Exercises: Join Matching Rows

Use `shop.db` with foreign keys enabled.

## Exercise 1: Name each category

Return product identifier, product name, category name, and price. Qualify every selected column and order by product identifier.

## Exercise 2: Filter a joined result

Return active products in one category chosen by its name. Keep the relationship in `ON` and ordinary requirements in `WHERE`.

## Exercise 3: Predict multiplication

1. Count products and categories separately.
2. Predict the row count of their `CROSS JOIN` by multiplication.
3. Run `COUNT(*)` over the cross join.
4. Explain why it differs from the proper key join count.
