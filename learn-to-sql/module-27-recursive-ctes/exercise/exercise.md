# Exercises: Walk Hierarchies with Recursive CTEs

## Exercise 1: Create a hierarchy

Fill the `employees` table from Module 15 with one leader, two direct reports, and two deeper reports. Query the whole organization with depth.

## Exercise 2: Start in the middle

Choose one manager as the anchor and return only that person's subtree. Add a text path showing names from the anchor to each row.

## Exercise 3: Reason about safety

Draw a two-row cycle. Explain why foreign keys allow it, how a write rule could reject it, and how a visited path protects the read.
