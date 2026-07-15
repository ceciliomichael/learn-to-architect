# Exercises: Design Relational Data and Normalize It

## Exercise 1: Repair repeating groups

Redesign `student(student_id, name, course_1, course_2, course_3)` using separate student, course, and enrollment tables. State every table's row meaning and key.

## Exercise 2: Find partial and indirect dependencies

Review `order_items(order_id, product_id, product_name, category_name, quantity)`. Decide where every column belongs and why.

## Exercise 3: Review the shop schema

For categories, products, orders, and order items, write:

1. One sentence for row grain.
2. The primary key.
3. The foreign keys.
4. One invalid state each constraint prevents.
