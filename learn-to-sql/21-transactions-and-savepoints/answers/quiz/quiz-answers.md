# Quiz Answers: Use Transactions and Savepoints

1. The whole intended unit commits or its work is rolled back.
2. No.
3. It undoes changes after the savepoint and leaves the transaction active.
4. No. Use savepoints.
5. Long transactions increase locking, contention, retained snapshots, and cleanup delays.
