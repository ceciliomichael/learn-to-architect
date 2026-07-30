# Module 12 Quiz Answers

1. **Answer: B**
   - **Reasoning**: `EXPLAIN QUERY PLAN` displays high-level information about how SQLite plans to execute a statement, including whether it uses `SCAN` or `SEARCH USING INDEX`.

2. **Answer: C**
   - **Reasoning**: While indexes accelerate read queries (`SELECT`), every `INSERT`, `UPDATE`, or `DELETE` must also update the index B-Tree, consuming extra disk space and write overhead.
