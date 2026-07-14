# Exercises: Select Columns and Name Results

Use `library.db`.

## Exercise 1: Choose exact columns

1. Select only `title` and `price` from `books`.
2. Predict the result headings before running it.
3. Reverse the column order and observe the output.

## Exercise 2: Create friendly headings

Write a query that returns:

- `book_id` with heading `id`
- `title` with heading `book_title`
- `published_year` with heading `year_published`

Confirm that `.schema books` still shows the original names.

## Exercise 3: Reason about rows

1. Select only `author`.
2. Count the visible result rows by inspection.
3. Explain why repeated author names remain repeated.
4. State whether their visible order is guaranteed.
