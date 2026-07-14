# Exercises: Upsert, RETURNING, and Generated Values

## Exercise 1: Build inventory

Create strict `inventory(product_id INTEGER PRIMARY KEY, quantity INTEGER NOT NULL CHECK(quantity >= 0))` with a foreign key to products. Insert one row.

## Exercise 2: Upsert deliberately

Add stock to the existing row with an upsert and return the result. Upsert a new product and confirm it inserts. Try an invalid negative value and read which rule stops it.

## Exercise 3: Use a generated total

Create `invoice_lines` from the lesson. Insert three lines without total values. Query totals, update one quantity, and confirm its generated total follows.
