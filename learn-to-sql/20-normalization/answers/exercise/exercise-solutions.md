# Exercise Solutions: Design Relational Data and Normalize It

## Exercise 1

Use:

- `students(student_id PRIMARY KEY, name)`, one row per student
- `courses(course_id PRIMARY KEY, title)`, one row per course
- `enrollments(student_id, course_id, PRIMARY KEY(student_id, course_id))`, one row per student-course relationship

Both enrollment columns are foreign keys. Any number of courses now becomes any number of rows.

## Exercise 2

`quantity` belongs in order items because it depends on the whole order-product pair. `product_name` belongs in products because product identity determines it. `category_name` belongs in categories, reached from the product's category foreign key.

## Exercise 3

One correct review is:

- Category: one row per category, keyed by category ID; unique name prevents duplicates.
- Product: one row per product, keyed by product ID; category ID references categories; price check prevents negative values.
- Order: one row per order, keyed by order ID; status check prevents unsupported states.
- Order item: one row per order-product pair, keyed by both; its foreign keys prevent nonexistent orders and products; quantity check prevents zero or negative units.
