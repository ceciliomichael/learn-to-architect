# Quiz Answers: Borrow with References

1. No. It grants temporary access.
2. Any number, while no conflicting mutable borrow is active.
3. Exclusive access for the active borrow.
4. At its last use when the compiler can prove it is no longer needed.
5. They could access a value after its owner dropped it.
