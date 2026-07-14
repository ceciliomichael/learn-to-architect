# Exercises: Calculate Across Rows with Window Functions

## Exercise 1: Compare each book with its author

Show title, author, price, and author average while preserving every book row.

## Exercise 2: Rank prices

Show row number, rank, and dense rank by descending price. Explain what happens if prices tie.

## Exercise 3: Top row per author

Use a CTE and `row_number` partitioned by author to return the most expensive book per author. Add deterministic tie breaking.
