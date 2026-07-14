# Exercises: Use Subqueries and EXISTS

## Exercise 1: Compare with one value

Return books whose price is below the overall average. Show the average separately and explain why the inner query is scalar.

## Exercise 2: Test relationships

In `shop.db`, return categories with products using `EXISTS`, then categories without products using `NOT EXISTS`.

## Exercise 3: Use a selected set

Return products whose category belongs to a subquery selecting category names beginning with `B` or `S`. Compare the result with an equivalent inner join.
