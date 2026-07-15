# Exercises: Keep Unmatched Rows with Outer Joins

## Exercise 1: Show empty categories

Insert one category with no products. Return every category and its product names. Confirm the new category appears with a `NULL` product.

## Exercise 2: Count actual children

Return one row per category with the count of products. Keep zero-product categories. Use the child primary key inside `COUNT`.

## Exercise 3: Compare filter placement

Run one left join with `p.active = 1` in `ON`, then one with it in `WHERE`. Explain which categories disappear and why.
