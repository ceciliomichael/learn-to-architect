# Module 03 Quiz Answers

1. **Answer: C**
   - **Reasoning**: In standard SQL and SQLite, `NULL` represents an unknown value. Comparing an unknown to an unknown yields an unknown truth state (`UNKNOWN`), which filters out the row in a `WHERE` clause.

2. **Answer: C**
   - **Reasoning**: `COALESCE(val1, val2, ...)` takes multiple arguments and evaluates to the first argument that is not `NULL`.
