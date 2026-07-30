# Module 11 Quiz Answers

1. **Answer: C**
   - **Reasoning**: MySQL InnoDB defaults to `REPEATABLE READ` isolation level, ensuring consistent non-repeatable read prevention within transactions.

2. **Answer: B**
   - **Reasoning**: InnoDB's fine-grained row-level locking locks only rows affected by a transaction, permitting concurrent writes to other rows.
