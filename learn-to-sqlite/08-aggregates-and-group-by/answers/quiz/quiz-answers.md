# Module 08 Quiz Answers

1. **Answer: B**
   - **Reasoning**: `HAVING` filters group summaries calculated by `GROUP BY`. `WHERE` filters individual rows before grouping takes place.

2. **Answer: B**
   - **Reasoning**: SQL aggregate functions (except `COUNT(*)`) ignore `NULL` values completely. `AVG` sums `10+20+30 = 60` and divides by the 3 non-null entries to return `20`.
