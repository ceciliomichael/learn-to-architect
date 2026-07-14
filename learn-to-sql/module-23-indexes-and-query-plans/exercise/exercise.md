# Exercises: Create Indexes and Read Query Plans

## Exercise 1: Compare a plan

1. Run the plan for filtering products by category before adding a new index.
2. Create `products_category_idx`.
3. Run the same plan again.
4. Record whether SQLite chose the index and why a small database may differ.

## Exercise 2: Test a composite query

Create an index on category, active, and price. Compare plans for:

1. Category plus active plus a price range.
2. Price alone.

Explain why the second query may not benefit equally.

## Exercise 3: Measure write cost conceptually

List every index on products with `.indexes products`. For an update to price, identify which index entries may need maintenance. Remove only indexes created for this disposable exercise.
