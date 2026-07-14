# Quiz answers

1. A virtual thread is a lightweight Java Thread designed for task-per-request blocking code.
2. Virtual threads improve the scale of waiting tasks but do not make CPU work faster.
3. Keep task handles or use an executor scope so completion and failure remain observable.
4. Ordinary blocking I/O is appropriate, while unbounded external work still needs limits and deadlines.
5. Virtual threads do not remove races and do not make mutable objects thread-safe.

