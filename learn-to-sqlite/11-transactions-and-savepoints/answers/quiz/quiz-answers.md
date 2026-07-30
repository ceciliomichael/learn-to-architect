# Module 11 Quiz Answers

1. **Answer: B**
   - **Reasoning**: `COMMIT` finalizes an open transaction and writes all pending changes permanently to disk.

2. **Answer: B**
   - **Reasoning**: `PRAGMA journal_mode = WAL;` activates Write-Ahead Logging, allowing readers to proceed concurrently without blocking concurrent writers.
