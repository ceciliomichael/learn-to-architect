# Module 12 Quiz Answers

1. **Answer: A**
   - **Reasoning**: `EXPLAIN FORMAT=TREE` prints a tree structure depicting iterator costs, rows, and execution operators in MySQL 8.0+.

2. **Answer: B**
   - **Reasoning**: The Leftmost Prefix Rule dictates that a composite index on `(colA, colB)` can optimize queries filtering on `colA` or `(colA, colB)`, but not queries filtering on `colB` alone.
