# Exercises: Protect Data with Constraints and Keys

## Exercise 1: Create the shop schema

Create `shop.db`, enable foreign keys, and create the lesson's `categories` and `products` tables. Inspect both schemas.

## Exercise 2: Prove each rule

1. Insert category 1 named `Books`.
2. Try another category named `Books`.
3. Insert a product with category 99.
4. Insert a product with a negative price.
5. Read each error and confirm failed rows were not added.

## Exercise 3: Use a default

Insert a valid product while omitting `active`. Select the row and explain why it contains 1.
